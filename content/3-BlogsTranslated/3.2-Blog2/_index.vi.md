AWS Compute Blog
Thiết Kế Các Mô Hình Tích Hợp Serverless Cho Mô Hình Ngôn Ngữ Lớn (LLMs)
Tác giả: Chris McPeek
 Ngày đăng: 04 tháng 10, 2024
 Danh mục: Amazon Bedrock, AWS Lambda, AWS Step Functions, Serverless
Bài viết này được viết bởi Josh Hart, Kiến Trúc Sư Giải Pháp Cấp Cao (Principal Solutions Architect) và Thomas Moore, Kiến Trúc Sư Giải Pháp Cấp Cao (Senior Solutions Architect).

Bài viết này khám phá các mô hình tích hợp theo thực tiễn tốt nhất để sử dụng các mô hình ngôn ngữ lớn (LLMs) trong các ứng dụng serverless. Những phương pháp tiếp cận này giúp tối ưu hiệu suất, sử dụng tài nguyên và khả năng phục hồi khi tích hợp các tính năng AI tạo sinh vào kiến trúc serverless của bạn.
Tổng quan về serverless, LLMs và ví dụ minh họa
Các tổ chức ở mọi quy mô đang khai thác các mô hình ngôn ngữ lớn (LLMs) để xây dựng các ứng dụng AI tạo sinh nhằm mang lại trải nghiệm khách hàng mới.
Các công nghệ serverless như AWS Lambda, AWS Step Functions và Amazon API Gateway cho phép bạn chuyển từ ý tưởng đến sản phẩm nhanh hơn mà không cần lo lắng về việc quản lý máy chủ.Mô hình tính phí theo mức sử dụng (pay-for-use) cũng giúp tăng tính linh hoạt với chi phí tối ưu.
Các ví dụ trong bài viết này sử dụng Amazon Bedrock, một dịch vụ được quản lý toàn phần cho phép truy cập các mô hình nền tảng foundation models Nguyên tắc tương tự cũng áp dụng cho các LLM được lưu trữ trên các nền tảng khác như Amazon SageMaker.
( FMs).Amazon Bedrock cho phép các nhà phát triển sử dụng LLM thông qua API mà không cần phải xử lý sự phức tạp của việc quản lý hạ tầng.Amazon SageMaker là một dịch vụ được quản lý toàn phần để xây dựng, huấn luyện và triển khai các mô hình học máy.

Trường hợp ví dụ trong bài viết này là sử dụng LLM để tạo ra nội dung marketing hấp dẫn cho việc ra mắt một dòng xe SUV gia đình mới.Các hình ảnh của phương tiện này được tạo sẵn bằng Amazon Titan Image Generator trong Amazon Bedrock, được minh họa bên dưới.


Hình ảnh ví dụ được tạo bằng Titan Image Generator
Khi các tổ chức áp dụng LLMs để cung cấp năng lực cho các ứng dụng AI tạo sinh (generative AI), kiến trúc serverless mang đến một phương pháp hấp dẫn cho phát triển nhanh và mở rộng quy mô tiết kiệm chi phí.Các phần tiếp theo sẽ trình bày một số mô hình tích hợp serverless nhằm xây dựng các ứng dụng AI tạo sinh có hiệu suất cao, chi phí tối ưu, và khả năng chịu lỗi tốt.

Gọi trực tiếp AWS Lambda

Gọi trực tiếp đến Amazon Bedrock từ AWS Lambda
Mô hình tích hợp serverless đơn giản nhất là gọi trực tiếp Bedrock trong Lambda bằng cách sử dụng AWS SDK. Dưới đây là ví dụ về một hàm Lambda sử dụng Python SDK (boto3), gọi đến API Bedrock InvokeModel.


python
import json
import boto3
brt = boto3.client(service_name='bedrock-runtime')

def lambda_handler(event, context):
    body = json.dumps({
        "anthropic_version": "bedrock-2023-05-31",
        "max_tokens": 1000,
        "messages": [{
            "role": "user",
            "content": [{
                "type": "text",
                "text":"Create a 500 word car advert given these images and the following specification: \n {}".format(event['spec'])
            },
            {
                "type": "image",
                "source": {
                    "type": "base64",
                    "media_type": "image/jpeg",
                    "data": event['image']
                }
            }]
        }]
    })

    modelId = 'anthropic.claude-3-sonnet-20240229-v1:0'
    accept = 'application/json'
    contentType = 'application/json'
    response = brt.invoke_model(body=body, modelId=modelId, accept=accept, contentType=contentType)
    response_body = json.loads(response.get('body').read())

    return {
        'statusCode': 200,
        'body': response_body["content"][0]["text"]
    }
Đoạn mã trên yêu cầu vai trò thực thi của hàm Lambda phải có quyền AWS Identity and Access Management (IAM) permissions to Amazon Bedrock, cụ thể là quyền hành động bedrock:InvokeModel.
Ví dụ này sử dụng mô hình ngôn ngữ lớn Anthropic Claude 3 Sonnet và Anthropic Claude Messages API cho phần payload.Lệnh gọi InvokeModel là đồng bộ, do đó nó sẽ chờ phản hồi từ LLM. Tùy thuộc vào mô hình và đoạn prompt, lệnh gọi có thể mất vài giây để hoàn thành. Hãy đảm bảo rằng thời gian chờ (timeout) của hàm Lambda được thiết lập phù hợp. Trong hầu hết các trường hợp, giá trị này cần được tăng lên so với mặc định là 3 giây. 
Thư viện boto3 có thời gian chờ mặc định là 60 giây. Tùy vào trường hợp sử dụng, bạn có thể cần tăng thời gian chờ của client boto3, như được minh họa trong đoạn mã ví dụ bên dưới.
 from botocore.config import Config
# Set the read timeout to 600 seconds (10 minutes)
config = Config(read_timeout=600)
# Create the Bedrock client with the custom read timeout configuration
boto3_bedrock = boto3.client(service_name='bedrock-runtime', config=config)
Khi làm việc với các mô hình ngôn ngữ lớn (LLMs), văn bản được tạo ra thường có dung lượng lớn, dẫn đến thời gian phản hồi tăng hoặc thậm chí bị hết thời gian chờ.Amazon Bedrock cung cấp khả năng truyền dữ liệu phản hồi theo luồng (streaming responses) bằng phương thức InvokeModelWithResponseStream, cho phép bạn xử lý và tiêu thụ phần văn bản được tạo ra theo từng khối (chunk) ngay khi nó sẵn sàng.Điều này giúp phản hồi nhanh hơn đến phía client và cho phép nhận được ít nhất một phần kết quả ngay cả khi xảy ra timeout.
Khi sử dụng phương thức truyền phản hồi theo luồng (response streaming) với các hàm Lambda, bạn nên đặt giá trị boto3 read_timeout thấp hơn thời gian chờ thực thi (execution timeout) của hàm. Điều này có nghĩa là bạn sẽ có tùy chọn trả về ít nhất một phần nội dung, trong một số trường hợp điều này vẫn tốt hơn là không có phản hồi nào cả.
Ví dụ, bạn có thể đặt thời gian chờ của hàm Lambda là 2 phút và thời gian chờ đọc của boto3 là 90 giây. Điều này cho phép bạn có thêm 30 giây để thực hiện các hành động bổ sung.
Tùy thuộc vào tình huống lỗi, bạn có thể thực hiện các hành động khác nhau:
Lỗi tạm thời như giới hạn tần suất (rate limiting) hoặc giới hạn dịch vụ (service quotas): Hãy xem xét việc giảm tần suất và thử lại yêu cầu, hoặc phân phối tải (load balancing) các yêu cầu sang khu vực khác bằng suy luận chéo vùng (cross-region inference).


Lỗi hết thời gian chờ (timeout) khi vượt quá giới hạn boto3 read_timeout: Quyết định xem có nên thử lại yêu cầu với prompt đơn giản hơn (hoặc rút ngắn độ dài phản hồi) hay chỉ trả về phản hồi một phần.
Liên kết chuỗi prompt với AWS Step Functions
Mô hình Lambda trực tiếp hoạt động hiệu quả đối với các trường hợp suy luận (inference) đơn giản chỉ có một prompt. Tuy nhiên, để thực hiện các tác vụ phức tạp hơn với LLM, cần sử dụng một kỹ thuật gọi là prompt chaining (liên kết chuỗi prompt), trong đó các tác vụ được chia nhỏ thành những prompt con có định nghĩa rõ ràng, và mỗi prompt sẽ được đưa vào LLM theo một trình tự xác định.
Việc thực hiện prompt chaining bên trong một hàm Lambda duy nhất có thể tốn nhiều thời gian và trong một số trường hợp có thể vượt quá giới hạn thời gian tối đa của Lambda là 15 phút. AWS Step Functions có thể được sử dụng để giải quyết vấn đề này bằng cách điều phối (orchestrate) các lệnh gọi đến LLM.Bedrock có tích hợp được tối ưu hóa(optimized intergration) cho Step Functions, cho phép bạn sử dụng chế độ Run as Job (.sync). Mô hình tích hợp này có nghĩa là Step Functions sẽ chờ cho đến khi yêu cầu InvokeModel hoàn tất trước khi chuyển sang trạng thái tiếp theo.Với Step Functions Standard Workflows, bạn chỉ phải trả phí cho mỗi lần chuyển trạng thái (state transition), điều này giúp giảm chi phí so với việc Lambda phải chờ trong trạng thái không hoạt động.
Ví dụ dưới đây minh họa cách liên kết chuỗi prompt với Step Functions chỉ bằng các tích hợp trực tiếp. Ví dụ này loại bỏ nhu cầu sử dụng mã tùy chỉnh trong Lambda.



Liên kết chuỗi prompt bằng AWS Step Functions
1.Dữ liệu đầu vào của người dùng (mô tả phương tiện) được truyền đến Amazon Bedrock thông qua tích hợp tối ưu (optimized intergration) của Step Functions.
2.Kết quả được tạo ra từ lệnh gọi API InvokeModel được truyền qua ResultPath đến bước kế tiếp.
3.Máy trạng thái (state machine) thiết lập đầu vào cho bước tiếp theo dựa trên đầu ra của bước trước đó bằng cách sử dụng Pass state.
4.Đầu ra của mỗi yêu cầu suy luận (inference request) tiếp tục được truyền giữa các bước trong quy trình làm việc (workflow). 
5.Bước cuối cùng thực hiện một yêu cầu suy luận và kết quả cuối cùng được trả về như đầu ra của máy trạng thái.
Một lợi thế khác khi sử dụng AWS Step Functions để gọi LLM là cơ chế xử lý lỗi tích hợp sẵn. Step Functions có thể được thiết lập để tự động thử lại khi retry on error và cho phép bạn cấu hình tỷ lệ backoff cũng như thêm jitter để giúp kiểm soát việc giới hạn tần suất (throttling). Không cần viết mã tùy chỉnh nào.


Các tùy chọn xử lý lỗi tích hợp sẵn cho một hành động trong quy trình làm việc AWS Step Functions
Việc xử lý giới hạn tần suất (throttling) đặc biệt quan trọng khi bạn đang tiến gần đến các giới hạn dịch vụ (service quota) của Bedrock, chẳng hạn như số lượng yêu cầu được xử lý mỗi phút đối với một mô hình cụ thể.Hãy lưu ý rằng một số giới hạn là giới hạn cố định (hard limits) và không thể điều chỉnh.Tham khảo service quotas documation của Bedrock để biết thông tin mới nhất.
Chạy song song các prompt với AWS Step Functions
Hiệu suất của ứng dụng có thể được cải thiện bằng cách chia nhỏ các tác vụ thành các tác vụ con và chạy chúng song song.Điều này có thể làm giảm đáng kể tổng thời gian phản hồi, đặc biệt đối với các mô hình lớn và các prompt phức tạp.Trong ví dụ sau, việc xử lý song song đã giúp giảm tổng thời gian thực thi của máy trạng thái (state machine) từ 30,8 giây xuống còn 19,2 giây — tức là cải thiện 37,7% so với khi thực hiện các bước đó theo tuần tự.
Ví dụ bên dưới sử dụng trạng thái song song (parallel state) trong Step Functions để thực hiện các hành động InvokeModel của Bedrock đồng thời.


Ví dụ liên kết chuỗi prompt sử dụng trạng thái song song trong AWS Step Functions
1.Dữ liệu đầu vào của người dùng (mô tả phương tiện) được truyền đến Amazon Bedrock thông qua tích hợp tối ưu (optimized intergration) của Step Functions. 
2.Trạng thái song song (parallel state) trong Step Functions cho phép sử dụng logic rẽ nhánh để thực hiện nhiều bước cùng lúc.
3.Các tác vụ suy luận (inference tasks) phức tạp được chạy song song nhằm giảm thời gian thực thi tổng thể từ đầu đến cuối.
4.Các tác vụ ngắn hơn có thể được kết hợp để cân bằng thời gian thực thi giữa các nhánh với những tác vụ có thời gian chạy dài hơn.
5.Kết quả được tạo ra được hợp nhất và phản hồi cuối cùng được trả về.
Ngoài trạng thái song song, Step Functions còn có trạng thái map (map state) cho phép chạy cùng một hành động nhiều lần song song với các đầu vào khác nhau.Ví dụ, nếu bạn muốn tạo tài liệu marketing cho 100 mẫu xe với dữ liệu được lưu trữ trong Amazon S3, bạn có thể chạy quy trình làm việc ở trên được lồng trong một trạng thái bản đồ phân tán (distributed map state).
Bộ nhớ đệm kết quả
Việc tạo văn bản bằng các mô hình ngôn ngữ lớn (LLMs) có thể tiêu tốn nhiều tài nguyên tính toán và thời gian, đặc biệt là đối với các prompt phức tạp hoặc các tác vụ tạo nội dung dài.Để cải thiện hiệu suất và giảm độ trễ, nên sử dụng cơ chế bộ nhớ đệm (caching) khi có thể bằng cách lưu trữ và tái sử dụng các phản hồi đã được tạo trước đó.hái niệm này được trình bày chi tiết trong bài viết Mastering LLM Caching for Next-Generation AI.
Bộ nhớ đệm có thể được triển khai ở nhiều cấp độ khác nhau trong kiến trúc ứng dụng của bạn, mỗi cấp độ đều có những ưu điểm và hạn chế riêng. Dưới đây là một số ví dụ:
1.Bộ nhớ đệm bên trong môi trường thực thi Lambda: nếu hàm Lambda của bạn nhận được các prompt hoặc đầu vào lặp lại, bạn có thể lưu trữ kết quả này trong bộ nhớ hoặc trong thư mục /tmp của môi trường thực thi đã được kích hoạt (warmed execution environment).
2.Dịch vụ bộ nhớ đệm bên ngoài: để vượt qua các giới hạn của bộ nhớ đệm trong bộ nhớ và tận dụng các giải pháp lưu trữ mạnh mẽ hơn, bạn có thể tích hợp với các dịch vụ bên ngoài để lưu trữ kết quả trước đó, chẳng hạn như Amazon ElastiCache (dành cho Redis hoặc Memcached) hoặc Amazon DynamoDB.
Ví dụ bên dưới sử dụng một quy trình làm việc Step Functions để kiểm tra phản hồi đã được lưu trong bộ nhớ đệm (cache) của DynamoDB trước khi gọi mô hình.Khóa bộ nhớ đệm (cache key) trong trường hợp này có thể là prompt được gửi đến LLM.Cách tiếp cận này giúp giảm chi phí đồng thời cải thiện hiệu suất.Ví dụ minh họa việc tạo ra các mô tả phương tiện tùy chỉnh dựa trên một nhóm đối tượng cụ thể (persona), chẳng hạn như tập trung vào các tính năng an toàn và không gian hành lý cho gia đình, hoặc các thông số hiệu suất dành cho người yêu thích thể thao tốc độ.


Ví dụ về AWS Step Functions sử dụng Amazon DynamoDB để lưu bộ nhớ đệm (cache) các phản hồi của LLM
Khi triển khai bộ nhớ đệm, điều quan trọng là phải xem xét các yếu tố như chiến lược làm mới bộ nhớ đệm (cache invalidation), giới hạn dung lượng bộ nhớ đệm, và yêu cầu về tính nhất quán của dữ liệu.Ví dụ, nếu mô hình LLM của bạn tạo ra nội dung động hoặc được cá nhân hóa, việc sử dụng bộ nhớ đệm có thể không phù hợp, vì các phản hồi có thể bị cũ hoặc không chính xác đối với những người dùng hoặc ngữ cảnh khác nhau.
Kết luận
Bài viết này đã khám phá các mô hình tích hợp để sử dụng LLM trong các ứng dụng serverless, nhằm mang lại trải nghiệm hiệu quả và đáng tin cậy cho thế hệ ứng dụng tiếp theo dành cho khách hàng.
Việc suy luận với một prompt duy nhất có thể được thực hiện bằng AWS Lambda thông qua AWS SDK.

Phản hồi từ các mô hình LLM có thể rất lớn và thường dẫn đến việc xử lý các đoạn văn bản lớn trong bộ nhớ, đặc biệt trong các trường hợp sử dụng 
Retrieval-Augmented Generation (RAG).Do đó, việc lựa chọn cấu hình bộ nhớ tối ưu cho hàm Lambda là rất quan trọng, và cách được khuyến nghị để thực hiện điều này là sử dụng công cụ AWS Lambda Power Tuning.
Khi cần thực hiện các chuỗi prompt phức tạp hơn, thực tiễn tốt nhất là sử dụng Step Functions như một giải pháp để giảm thời gian chờ không hoạt động và tránh giới hạn thời gian tối đa 15 phút của Lambda.Step Functions cũng mang lại lợi ích của việc tích hợp được tối ưu hóa cho Bedrock, cũng như khả năng xử lý lỗi và chạy song song các tác vụ.
Hãy nhớ rằng việc lựa chọn mô hình (model choice) cũng là một yếu tố quan trọng cần cân nhắc để cân bằng giữa chi phí, hiệu suất và khả năng đầu ra.Chủ đề này được thảo luận chi tiết hơn trong bài viết Choose the best foundational model for your AI applications.
Để tìm hiểu thêm các mô hình serverless khác sử dụng Amazon Bedrock, hãy tham khảo Serverless Land.
