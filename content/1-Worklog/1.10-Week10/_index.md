---
title: "Week 10 Worklog"
date: 2026-06-19
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}

### Week 10 Objectives:
* Design and develop the web user interface (Next.js) and backend service APIs (Node.js/Express or NestJS).
* Implement a secure user authentication system using JWT and configure role-based access control (User, Coach).
* Integrate connections to the Amazon RDS PostgreSQL database and store files on Amazon S3 from the application.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Thu | - Develop the frontend interface (Landing Page, Coach search dashboard) using Next.js and Tailwind CSS | 19/06/2026 | 19/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Fri | - Build backend RESTful APIs: Signup/Login with bcrypt password hashing and JWT authentication | 20/06/2026 | 20/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Mon | - Configure backend connectivity to the RDS PostgreSQL database and execute migrations to create tables | 22/06/2026 | 22/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | - Implement core business APIs: Fetch coach listings, filter by skills, and book sessions | 23/06/2026 | 23/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | - Integrate AWS SDK into the backend to enable uploading coach avatars and certificates directly to Amazon S3 | 24/06/2026 | 25/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Week 10 Achievements:
* **Web & API Development:**
  - Completed the Landing Page interface showing dynamic coach listings and filtering options by expertise.
  - Implemented a complete JWT-based Authentication flow, distinguishing role access between students and coaches.
  - Created core RESTful APIs for Coach CRUD operations and Booking Session creation.
* **Software-Infrastructure Connectivity:**
  - Successfully connected the backend application to the RDS PostgreSQL instance using an ORM (Prisma/TypeORM) with an optimized connection pool.
  - Integrated media storage capabilities via the AWS SDK, enabling secure file uploads to S3 using IAM roles instead of hardcoding API keys in the codebase.
