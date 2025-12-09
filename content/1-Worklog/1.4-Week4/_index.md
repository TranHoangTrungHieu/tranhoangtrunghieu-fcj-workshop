---
title: "Week 4 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives

* Gain hands-on experience with advanced AWS Networking topics, including Hybrid DNS and Route 53 Resolver.
* Understand how hybrid environments connect on-prem networks and AWS using DNS forwarding and Transit Gateway.
* Strengthen security awareness through proper configuration of Security Groups and least-privilege network policies.

---

### Tasks Completed This Week

| Day | Task | Start Date | Completion Date | Reference |
|-----|------|-------------|-----------------|-----------|
| **Mon** | - Studied Hybrid DNS concepts using Route 53 Resolver: inbound/outbound endpoints, forwarding rules, hybrid DNS between on-prem and AWS.<br>- Reviewed common enterprise use cases for hybrid DNS. | 06/10/2025 | 06/10/2025 | https://www.youtube.com/watch?v=FGicpWOmMDI |
| **Tue** | - Followed the Hybrid DNS lab: created required VPCs, subnets, and initial Route 53 Resolver setup.<br>- Drew an architecture diagram showing on-prem DNS, Resolver endpoints, and VPC structure. | 07/10/2025 | 07/10/2025 | https://000010.awsstudygroup.com/vi/ |
| **Wed** | - Configured Security Groups for the Hybrid DNS environment: allowed only ICMP (ping) and RDP for testing, removed unused ports for least-privilege design.<br>- Tested connectivity to confirm that Security Group rules were correctly applied. | 08/10/2025 | 08/10/2025 | https://www.youtube.com/watch?v=kE_krznNBFU |
| **Thu** | - Completed Route 53 Resolver setup: created inbound and outbound endpoints and forwarding rules.<br>- Verified DNS resolution bidirectionally (on-prem → AWS and AWS → on-prem). | 09/10/2025 | 09/10/2025 | https://www.youtube.com/watch?v=L-2YfZceoAU |
| **Fri** | - Learned AWS Transit Gateway fundamentals: attachments, routing domains, pricing model.<br>- Created a Transit Gateway, attached VPCs to it, updated VPC route tables, and validated cross-VPC communication. | 10/10/2025 | 10/10/2025 | https://www.youtube.com/watch?v=W1m_OFPDui0 |

---

### Week 4 Achievements

* Developed a strong understanding of how **Hybrid DNS** works in enterprise cloud architectures.
* Successfully configured **Route 53 Resolver inbound/outbound endpoints** and forwarding rules for DNS queries between AWS and “on-prem” environments.
* Improved understanding of network-level security by designing **least-privilege Security Groups**.
* Built a working **Transit Gateway** environment and enabled routing between multiple VPCs.
* Practiced analyzing and troubleshooting DNS and network connectivity issues.
* Strengthened knowledge of AWS advanced networking concepts, preparing for future labs such as Site-to-Site VPN and Direct Connect.

---
