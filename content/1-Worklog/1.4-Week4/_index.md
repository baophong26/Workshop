---
title: "Week 4 Worklog"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
* Learn secure authorization patterns using IAM Roles for EC2 instances.
* Practice creating, managing, and hosting a static website using Amazon S3.
* Configure Amazon CloudFront CDN to optimize performance, reduce latency, and integrate Lambda@Edge serverless computing.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Learn about IAM Roles for EC2; create a role to read S3 and assign to EC2 | 08/05/2026 | 08/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Test calling S3 APIs from inside the EC2 instance using the IAM Role | 09/05/2026 | 09/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Learn about S3: create a bucket and upload static files (HTML/CSS/JS) | 11/05/2026 | 11/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Enable Static Website Hosting on S3, set public read policy | 12/05/2026 | 12/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Set up CloudFront CDN distribution pointing to the S3 Origin with OAI/OAC | 13/05/2026 | 14/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Write a Lambda@Edge function to modify security response headers at edge locations | 14/05/2026 | 14/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 4 Achievements:
* **IAM Roles for EC2:**
  - Assigned an IAM Role to the EC2 instance successfully. Removed the need to hardcode AWS credentials in the application, adhering to security best practices.
* **Amazon S3 Static Website Hosting:**
  - Configured S3 static website hosting and accessed the site using the endpoint `http://<bucket-name>.s3-website-<region>.amazonaws.com`.
* **Amazon CloudFront & Lambda@Edge:**
  - Deployed a CloudFront CDN distribution.
  - Used Origin Access Control (OAC) to restrict access to the S3 bucket directly, forcing all requests to go through CloudFront.
  - Integrated Lambda@Edge to append custom HTTP security headers to responses directly from the nearest edge locations.
