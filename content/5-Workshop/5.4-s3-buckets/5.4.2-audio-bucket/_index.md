---
title: "Create S3 Bucket for Audio Upload"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

#### Purpose

This bucket will store:
- Audio recordings from users (uploaded via Presigned URL)
- Audio feedback files from Amazon Polly

This bucket will be kept **private** and only Lambda has access.

#### Steps to Perform

**1. Create New Bucket**

- In S3 Console, click **Create bucket**

**2. Configure Bucket**

**General configuration:**
- Bucket name: `itcoach-audio-upload`
- AWS Region: `ap-southeast-1` (Singapore)

**Block Public Access settings:**
- **KEEP** "Block all public access" checked
- This bucket must be private to secure audio files

![Private Bucket](/images/5-Workshop/5.4-s3-buckets/003-audio-bucket-private.png)

**Other settings:**
- Keep all defaults
- Click **Create bucket**

**3. Configure CORS**

After bucket is created:

- Click on bucket name `itcoach-audio-upload`
- Select **Permissions** tab
- Scroll to **Cross-origin resource sharing (CORS)** section
- Click **Edit**

Paste the following JSON content:

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": ["ETag"]
  }
]
```

![CORS Config](/images/5-Workshop/5.4-s3-buckets/004-cors-config.png)

- Click **Save changes**


#### Result

✅ Bucket `itcoach-audio-upload` has been created with CORS configuration

#### Information to Save

```
Bucket Name: itcoach-audio-upload
Region: ap-southeast-1
Access: Private (Block public access enabled)
CORS: Configured for direct browser upload
```

#### Explanation of Presigned URL

Lambda function will create **Presigned URL** - a temporary URL that allows uploading files to this private S3 bucket without credentials. This URL:
- Has expiration time (e.g.: 5 minutes)
- Only has PUT permission for one specific object
- More secure than allowing public upload

#### Next Step

Move to the next step to create DynamoDB Tables.

