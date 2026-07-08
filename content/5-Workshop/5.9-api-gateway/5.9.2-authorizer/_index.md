---
title: "Create Cognito Authorizer"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.9.2. </b> "
---

#### Purpose

Cognito Authorizer validates JWT token from Cognito before allowing requests to Lambda. Only `/auth` endpoint is public, the other 7 endpoints require auth.

#### Steps

**1. Create Authorizer**

- In API `itcoach-api`, left menu → **Authorizers**
- Click **Create authorizer**

**2. Configure Authorizer**

- Authorizer name: `itcoach-cognito-auth`
- Type: **Cognito**
- Cognito user pool: select region `ap-southeast-1` → select User Pool created earlier
- Token source: `Authorization` (keep prefix `method.request.header.`)

![Cognito Authorizer](/images/5-Workshop/5.9-api/002-cognito-authorizer.png)

- Click **Create authorizer**

#### Result

✅ Cognito Authorizer `itcoach-cognito-auth` created
