---
title: "Week 5 Worklog"
date: 2026-05-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:
* Learn and deploy relational database management systems on AWS using Amazon RDS.
* Familiarize with high-performance, highly scalable NoSQL databases using Amazon DynamoDB.
* Understand database query caching solutions using Amazon ElastiCache to optimize latency.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Explore Amazon RDS: DB Engines, Multi-AZ deployments, Read Replicas | 15/05/2026 | 15/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Launch RDS MySQL/PostgreSQL in a Private Subnet and test connection from EC2 | 16/05/2026 | 16/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Study DynamoDB NoSQL: Tables, Partition Key, Sort Key | 18/05/2026 | 18/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Practice creating DynamoDB Table, loading items, Query and Scan | 19/05/2026 | 19/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Learn about Amazon ElastiCache: Launch a Redis/Memcached cluster | 20/05/2026 | 21/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Connect application on EC2 to ElastiCache for caching to reduce RDS workload | 21/05/2026 | 21/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 5 Achievements:
* **Amazon RDS:**
  - Configured and launched an RDS instance inside Private Subnets.
  - Set up Security Groups to restrict access only to the EC2 security group.
  - Learned about high availability with Multi-AZ deployments and read optimization using Read Replicas.
* **Amazon DynamoDB:**
  - Created a DynamoDB Table, understanding the performance differences between Query (efficient, targeted by keys) and Scan (scans entire table, resource-intensive).
* **Amazon ElastiCache:**
  - Deployed a Redis cluster. Understood the cache-aside pattern to reduce backend database workloads.
