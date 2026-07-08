---
title: "Week 8 Worklog"
date: 2026-06-05
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:
* Learn to administer Windows Server instances on AWS EC2.
* Understand centralized directory services using AWS Managed Microsoft Active Directory.
* Architect and build a high availability, fault-tolerant web infrastructure based on AWS best practices.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Deploy Windows Server EC2, decrypt Administrator password via Key Pair | 05/06/2026 | 05/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Connect via RDP (Remote Desktop) and configure IIS (Internet Information Services) | 06/06/2026 | 06/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Explore AWS Managed Microsoft AD: Initialize Active Directory on AWS | 08/06/2026 | 08/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Join the Windows EC2 instance to the domain, manage users/groups | 09/06/2026 | 09/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Build High Availability Web architecture: ALB, ASG (2 AZs), and Multi-AZ RDS | 10/06/2026 | 11/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Simulate AZ failure or terminate instances to verify system failover | 11/06/2026 | 11/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 8 Achievements:
* **Windows Applications on AWS:**
  - Successfully launched a Windows Server instance, decrypted Administrator credentials, and connected via Remote Desktop. Configured IIS to host a sample ASP.NET site.
* **AWS Managed Microsoft AD:**
  - Deployed a fully managed Active Directory domain. Joined a Windows machine to the domain and successfully authenticated using centralized AD accounts.
* **High Availability Web App:**
  - Built a production-grade infrastructure: Application Load Balancer -> Auto Scaling Group (multi-AZ web instances) -> RDS Multi-AZ DB.
  - Confirmed failover: when an instance was terminated, the ALB immediately routed traffic to healthy servers, and the ASG launched a replacement instance automatically.
