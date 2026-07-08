---
title: "Week 3 Worklog"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
* Master the basics of EC2 virtual servers, storage management with EBS, and secure access configurations.
* Get familiar with managing resources via command-line operations using AWS CLI.
* Work in a cloud-integrated development environment (Cloud IDE) using AWS Cloud9.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Study theoretical concepts of Amazon EC2: Instance Types, AMI, Key Pairs, Security Groups | 01/05/2026 | 01/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Launch a Linux EC2 instance, configure EBS Volume, and connect via SSH | 02/05/2026 | 02/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Install AWS CLI locally and configure IAM Credentials (Access/Secret Key) | 04/05/2026 | 04/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Practice querying EC2 info and creating/deleting resources via AWS CLI | 05/05/2026 | 05/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Launch AWS Cloud9 IDE, integrate Git, and write code directly in the environment | 06/05/2026 | 07/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 3 Achievements:
* **Amazon EC2 & EBS:**
  - Successfully launched a Linux EC2 instance (Amazon Linux 2 / Ubuntu), configured Security Groups to allow SSH (port 22) from my personal IP address only.
  - Created, attached, and mounted an EBS Volume to the EC2 instance for persistent storage independent of the instance life cycle.
* **AWS CLI:**
  - Configured AWS CLI profiles.
  - Used common CLI commands such as `aws ec2 describe-instances`, `aws s3 ls`, `aws iam list-users` to manage system resources from the terminal.
* **AWS Cloud9:**
  - Created an AWS Cloud9 Development Environment to write, run, and debug code directly through a web browser without complex local environments.
