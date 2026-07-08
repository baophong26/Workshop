---
title: "Week 2 Worklog"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:
* Learn the fundamental concepts of networking on AWS (VPC, Subnet, Route Table, etc.).
* Set up a multi-availability zone network architecture (Multi-AZ VPC) to ensure reliability and fault tolerance.
* Practice creating, connecting, and routing between multiple VPC networks.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Study theoretical concepts of Amazon VPC, CIDR block, Subnets (Public/Private) | 24/04/2026 | 24/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Manually create a VPC, configure Internet Gateway, Route Tables | 25/04/2026 | 25/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Deploy NAT Gateway, set up routing for Private Subnet to access Internet | 27/04/2026 | 27/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Participate in AWS Networking Workshop: create Multi-VPC and connect via VPC Peering | 28/04/2026 | 28/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Configure routing for VPC Peering and verify network connectivity | 29/04/2026 | 30/04/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 2 Achievements:
* **Amazon VPC:**
  - Successfully designed and created a custom VPC with an appropriate CIDR block (e.g., `10.0.0.0/16`).
  - Segmented the VPC into Public Subnets (direct connection to the Internet via Internet Gateway) and Private Subnets (internal communication or indirect outbound access).
  - Created and configured Route Tables to direct network traffic via Internet Gateway or NAT Gateway.
  - Installed NAT Gateway in the Public Subnet to allow resources in Private Subnets to pull updates from the Internet while preventing direct inbound connections.
* **AWS Network Workshop:**
  - Built a Multi-VPC model with at least 2 distinct VPCs to simulate isolated system segments.
  - Established a VPC Peering connection between the two VPCs, allowing resources to communicate securely using private IP addresses with low latency.
  - Configured Route Tables in both VPCs to direct peering-destined traffic through the peering connection.
