---
title: "Configuring Amazon Cognito"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Introduction to Amazon Cognito

Amazon Cognito provides authentication, authorization, and user management for web and mobile applications. In ITCoach, Cognito will:
- Manage user registration/login
- Create JWT tokens for authentication
- Protect API Gateway endpoints

#### Steps

**1. Access Cognito Console**

- Search for **Cognito** in the AWS Console search bar
- Click on **Amazon Cognito**

**2. Create User Pool**

- Click the **Create user pool** button

![Cognito Config](/images/5-Workshop/5.6-cognito/001-cognito-config.png)


**3. Configure User Pool on 1 page**

**Application type:**
- Select **Single-page application (SPA)**

**Name your application:**
- Application name: `itcoach-web-client`

**Sign-in options:**
- Check ✅ **Email**
- Uncheck Username and Phone number

**Self-registration:**
- ✅ **Enable self-registration** (keep default - allows users to self-register)

**Required attributes:**
- Click **Select attributes**
- Check: **name** (User's full name)
- Email is already selected automatically

**Password policy:**
- Keep default (Cognito defaults)

**Multi-factor authentication (MFA):**
- Select **No MFA** (to keep workshop simple)

**Return URL:**
- Enter: `http://localhost:3000`
- (Will update to CloudFront URL later)

**Email provider:**
- Keep default: **Send email with Amazon SES**

- Click **Create user directory** button (orange button)

**4. Wait for User Pool Creation**

Creation process takes about 10-20 seconds.

**5. Save User Pool ID**

- After creation, you'll see the **User pool ID** (format: `ap-southeast-1_xxxxxxxx`)
- Copy and save it

![User Pool ID](/images/5-Workshop/5.6-cognito/002-user-pool-id.png)

**6. Save App Client ID**

- Click on the **App clients** tab (or **App integration**)
- Find client `itcoach-web-client`
- Copy **Client ID** (format: 26-character string)

![App Client ID](/images/5-Workshop/5.6-cognito/003-app-client-id.png)

#### Result

✅ Amazon Cognito User Pool configured successfully

#### Information to Save

```
User Pool ID: ap-southeast-1_xxxxxxxx
App Client ID: xxxxxxxxxxxxxxxxxxxxxxxxxxxx
Region: ap-southeast-1
Application Name: itcoach-web-client
Sign-in: Email
Return URL: http://localhost:3000 (temporary)
```


#### How It Works

1. **User registers**: Frontend calls Cognito API → Cognito sends confirmation email
2. **User logs in**: Cognito returns **JWT token** (ID token, Access token)
3. **User calls API**: Frontend sends token in header `Authorization: Bearer <token>`
4. **API Gateway**: Validates token with Cognito before passing to Lambda

#### Next Steps

Move to the next step to create Amazon SQS.
