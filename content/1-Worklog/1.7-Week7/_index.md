---
title: "Week 7 Worklog"
date: 2026-05-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:
* Understand the automatic scaling mechanism for virtual servers via EC2 Auto Scaling.
* Set up a resource monitoring system, gather logs, and trigger automated alerts using Amazon CloudWatch.
* Explore the Amazon Route 53 Domain Name System (DNS) and smart routing policies.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Learn Auto Scaling concepts: Launch Templates, Auto Scaling Groups (ASG), Scaling Policies | 29/05/2026 | 29/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Create Launch Template, configure ASG to scale up/down based on CPU usage | 30/05/2026 | 30/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Study Amazon CloudWatch: Monitor Metrics and set up Alarms | 01/06/2026 | 01/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Install CloudWatch Agent on EC2 to push OS logs to CloudWatch Logs | 02/06/2026 | 02/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Learn Route 53: Register domain, create Hosted Zone, manage records (A, CNAME) | 03/06/2026 | 04/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Configure DNS Routing Policies (Weighted, Failover) with Route 53 Health Checks | 04/06/2026 | 04/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 7 Achievements:
* **EC2 Auto Scaling:**
  - Configured an Auto Scaling Group (ASG) with bounds (Min: 1, Max: 3).
  - Simulated high CPU loads using the `stress` utility and verified that the group successfully spawned extra EC2 instances (Scale Out) and terminated them when idle (Scale In).
* **Amazon CloudWatch:**
  - Created a CloudWatch Alarm to send email notifications via Amazon SNS when CPU exceeds 80% for 5 minutes.
  - Utilized CloudWatch Logs to collect and inspect operating system logs from the web console.
* **Amazon Route 53:**
  - Set up active Health Checks to monitor endpoint health.
  - Configured a Failover Routing Policy to redirect users to a standby backup site when the primary server fails a health check.
