---
title: "Week 9 Worklog"
date: 2026-06-12
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}

### Week 9 Objectives:
* Analyze business requirements and define core features for the Web IT Coach project.
* Design the overall system architecture and the secure network infrastructure topology (VPC).
* Design the relational database schema (ERD) for managing users, coaches, and booking sessions.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Research business requirements and define the core features of the Web IT Coach platform | 12/06/2026 | 12/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Design the overall system architecture: Next.js (Frontend), Node.js/Express (Backend), S3 (Media), RDS PostgreSQL (Database) | 13/06/2026 | 13/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Design secure network infrastructure (AWS VPC) with Public and Private Subnets | 15/06/2026 | 15/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Design the Entity-Relationship Diagram (ERD) and define tables and relationships | 16/06/2026 | 16/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Review security solutions (Security Groups, IAM Roles) and initialize project template repository on Git | 17/06/2026 | 18/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 9 Achievements:
* **System Design:**
  - Completed the requirements analysis document for Web IT Coach, featuring user authentication, coach listings, filter by skills, booking sessions, and a review system.
  - Aligned on the system architecture: Client -> Application Load Balancer -> Web Server (EC2) -> Database Server (RDS PostgreSQL).
* **Network Infrastructure Design:**
  - Designed the AWS VPC network topology spanning 2 Availability Zones to ensure high availability.
  - Divided the network into Public Subnets (hosting ALB, NAT Gateway) and Private Subnets (hosting Backend EC2 and RDS Database) to block direct internet access to backend services.
* **Database & Project Setup:**
  - Completed the ERD schema with primary entities: `Users`, `Coaches`, `Bookings`, `Reviews`, `Transactions`.
  - Initialized the Git repository and organized codebase structure for both Frontend and Backend.
