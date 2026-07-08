---
title: "Setting up CloudFront"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

#### Introduction to CloudFront

Amazon CloudFront is a Content Delivery Network (CDN) that distributes content with low latency. In ITCoach, CloudFront will:
- Distribute React + TypeScript frontend globally
- Cache static assets (HTML, CSS, JS)
- Provide HTTPS
- Handle React Router (SPA routing)

#### Steps

**1. Access CloudFront Console**

- Search for **CloudFront**
- Click on **CloudFront**

**2. Create Distribution**

- Click **Create distribution**

**Origin Settings:**
- Origin domain: Select S3 bucket `itcoach-static-assets` or paste S3 website endpoint
- Origin path: *(leave empty)*
- Name: `itcoach-s3-origin`

**Default Cache Behavior:**
- Viewer protocol policy: **Redirect HTTP to HTTPS**
- Allowed HTTP methods: **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE**
- Cache policy: **CachingOptimized**

**Distribution Settings:**
- Price class: **Use all edge locations (best performance)**
- Alternate domain name (CNAME): *(leave empty if no custom domain yet)*
- Default root object: `index.html`

![CloudFront Config](/images/5-Workshop/5.10-cloudfront/001-cloudfront-config.png)

- Click **Create distribution**

**3. Wait for CloudFront Deployment**

Deployment process takes **5-15 minutes**. Status will change from **Deploying** → **Deployed**.

**4. Configure Error Pages (React Router)**

For React Router to work (SPA routing):

- Click on distribution
- **Error pages** tab → **Create custom error response**

Create 2 error responses:

| HTTP error code | Response page path | HTTP response code |
|----------------|-------------------|-------------------|
| `403` | `/index.html` | `200` |
| `404` | `/index.html` | `200` |

![Error Pages](/images/5-Workshop/5.10-cloudfront/002-domain-error-pages.png)

**5. Save CloudFront Domain**

- Copy **Distribution domain name**
- Format: `https://xxxxxxxxxxxx.cloudfront.net`

**6. Update Cognito Return URL (IMPORTANT)**

Go back to Cognito User Pool:

- **App integration** tab → Edit callback URL
- Replace `http://localhost:3000` with CloudFront domain
- **Save changes**

#### Result

✅ CloudFront distribution ready to distribute frontend

#### Information to Save

```
Distribution Name: itcoach-distribution
Domain: https://xxxxxxxxxxxx.cloudfront.net
Origin: itcoach-static-assets (S3 website endpoint)
Default Root: index.html
Error Pages: 403→200, 404→200 (React Router)
```

#### Test CloudFront

Access CloudFront domain in browser:
```
https://xxxxxxxxxxxx.cloudfront.net
```

Currently will show error because React + TypeScript hasn't been uploaded yet. After developing frontend and uploading to S3, the website will work.

#### Next Steps

Move to the next step to set up Monitoring with CloudWatch and SNS.
