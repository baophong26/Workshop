---
title: "Create S3 Bucket for Static Assets"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

#### Purpose

This bucket will store the built React + TypeScript frontend (HTML, CSS, JavaScript) and be configured as Static Website Hosting for CloudFront distribution.

#### Steps to Perform

**1. Access S3 Console**

- Search for **S3** in AWS Console search bar
- Click on **S3** to open S3 Dashboard

**2. Create New Bucket**

- Click **Create bucket** button

**3. Configure Bucket**

**General configuration:**
- Bucket name: `itcoach-static-assets`
- AWS Region: `ap-southeast-1` (Singapore)

**Object Ownership:**
- Keep default: **ACLs disabled**

**Block Public Access settings:**
- **UNCHECK** "Block all public access"
- Check the acknowledgment box: "I acknowledge that the current settings might result in this bucket and the objects within becoming public"

**Bucket Versioning:**
- Keep default: **Disable**

**Encryption:**
- Keep default: **Server-side encryption with Amazon S3 managed keys (SSE-S3)**

![Static Bucket Config](/images/5-Workshop/5.4-s3-buckets/001-static-bucket-config.png)

- Click **Create bucket**

**4. Enable Static Website Hosting**

After bucket is created:

- Click on bucket name `itcoach-static-assets`
- Select **Properties** tab
- Scroll to bottom, find **Static website hosting** section
- Click **Edit**

Configuration:
- Static website hosting: select **Enable**
- Hosting type: **Host a static website**
- Index document: `index.html`
- Error document: `index.html` (for React Router)

- Click **Save changes**

**5. Save Website Endpoint**

After saving, scroll back to **Static website hosting** section, you will see **Bucket website endpoint**.

Copy this URL (format: `http://itcoach-static-assets.s3-website-ap-southeast-1.amazonaws.com`)

![Website Endpoint](/images/5-Workshop/5.4-s3-buckets/002-website-endpoint.png)

#### Result

✅ Bucket `itcoach-static-assets` has been created and configured for Static Website Hosting

#### Information to Save

```
Bucket Name: itcoach-static-assets
Region: ap-southeast-1
Website Endpoint: http://itcoach-static-assets.s3-website-ap-southeast-1.amazonaws.com
```


#### Next Step

Move to the next step to create S3 Bucket for Audio Upload.

