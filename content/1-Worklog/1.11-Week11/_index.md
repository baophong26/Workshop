---
title: "Week 11 Worklog"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}

### Week 11 Objectives:
* Build advanced web features (Mock Payment Gateway, Reviews/Ratings system) and optimize application performance.
* Package the application using Docker and configure deployment on EC2 server instances.
* Set up traffic distribution (ALB), auto-scaling (ASG), secure custom domain mapping (HTTPS), and integrate CI/CD automation.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Develop the Mock Payment Gateway and the review rating system for coaches | 26/06/2026 | 26/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Optimize application performance: index database tables on query-heavy columns and minimize Next.js build bundle size | 27/06/2026 | 27/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Write Dockerfiles and a docker-compose configuration to containerize the frontend and backend applications | 29/06/2026 | 29/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Deploy Docker containers to EC2 instances and set up Application Load Balancer (ALB) and Auto Scaling Group (ASG) | 30/06/2026 | 30/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Map custom domain via Route 53, configure HTTPS SSL/TLS certificates via ACM, and set up CI/CD pipeline using GitHub Actions | 01/07/2026 | 02/07/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 11 Achievements:
* **Advanced Web Features & Optimization:**
  - Completed the booking workflow, allowing students to pay through a mockup gateway and submit rating stars and text reviews for coaches.
  - Reduced API response time from ~400ms to ~80ms by adding indexes to the `skills` and `booking_date` columns in the PostgreSQL database.
* **Packaging & Cloud Deployment:**
  - Successfully containerized the application using Docker, ensuring consistent deployment behavior across local and cloud environments.
  - Deployed Docker containers onto EC2 instances protected by an Application Load Balancer (ALB) and managed under an Auto Scaling Group (ASG) for scale and reliability.
  - Connected the custom domain using Route 53 and enabled HTTPS traffic encryption using ACM SSL certificates.
  - Set up a CI/CD pipeline using GitHub Actions to automatically run tests, build Docker images, and push them to ECR/Docker Hub, triggering automated SSH deployment to EC2 upon branch updates.
