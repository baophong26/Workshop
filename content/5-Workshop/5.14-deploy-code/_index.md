---
title: "Deploy Code"
date: 2024-01-01
weight: 14
chapter: false
pre: " <b> 5.14. </b> "
---

#### Introduction

After setting up the complete AWS infrastructure, the next step is to deploy actual code to make the system operational. This section guides you through deploying Frontend (React + TypeScript) and Backend (Lambda functions).

---

## 1. Deploy Frontend (React + TypeScript)

### Step 1: Build Frontend

On your local machine, run the build command:

```bash
npm run build
```

After building, you will have a `/dist` or `/build` folder containing optimized HTML, CSS, JS files.

### Step 2: Upload to S3

1. Go to **S3** → Buckets → select `itcoach-static-assets`
2. Click **Upload**
3. Drag and drop **all contents** from `/dist` folder (not the folder itself, but files inside)
4. Click **Upload**

### Step 3: Invalidate CloudFront Cache

To ensure users see the latest version, you need to clear CloudFront cache:

1. Go to **CloudFront** → Distributions
2. Select `itcoach-distribution`
3. Tab **Invalidations** → **Create invalidation**
4. Object paths: `/*`
5. **Create invalidation**

Invalidation process takes about 1-3 minutes.

### Step 4: Verify

Visit `https://itcoach24h.xyz` (or CloudFront domain) to verify frontend displays correctly.

---

## 2. Deploy Backend (Lambda Functions)

### Step 1: Package Lambda Functions

Each Lambda function needs to be packaged as a `.zip` file including:
- Python code
- Dependencies (third-party libraries)

Example structure:
```
itcoach-auth-handler.zip
├── lambda_function.py
└── (libraries if any)
```

### Step 2: Upload Code to Lambda

Repeat for all 8 functions:

1. Go to **Lambda** → Functions
2. Select function (e.g., `itcoach-auth-handler`)
3. Tab **Code** → **Upload from** → **.zip file**
4. Choose corresponding `.zip` file
5. **Save**
6. Wait for Lambda to deploy (screen shows "Successfully updated")

### Step 3: Test Lambda

1. Tab **Test** → **Create test event**
2. Event name: `test-event`
3. Paste sample test event JSON
4. **Save** → **Test**
5. Check **Execution result** returns correctly

---

## 3. Overall Verification

### Test API Endpoints

Use Postman or curl to test:

```bash
# Test public endpoint
curl -X POST https://your-api-url/prod/auth \
  -H "Content-Type: application/json" \
  -d '{"action":"register","email":"test@example.com"}'

# Test protected endpoint (requires token)
curl -X GET https://your-api-url/prod/questions \
  -H "Authorization: Bearer YOUR_COGNITO_TOKEN"
```

### Test Frontend

1. Open `https://itcoach24h.xyz`
2. Register new account
3. Login
4. Try features:
   - Quiz multiple choice
   - Voice essay
   - Dashboard
   - Leaderboard

---

## 4. Monitoring After Deploy

### Check CloudWatch Logs

1. **CloudWatch** → Log groups
2. Find `/aws/lambda/itcoach-*`
3. View logs of Lambda functions
4. Check for errors

### Check CloudWatch Alarms

If alarms were created in section 5.12:
- Alarms will change from "Insufficient data" to "OK" after real traffic
- If errors occur, alarms will change to "In alarm" and send email via SNS

---

## 5. Update Cognito Callback URL

After having real domain, update Cognito:

1. **Cognito** → User pools → select pool
2. Tab **App integration** → select App client
3. **Edit Hosted UI settings**
4. Allowed callback URLs:
   - Add: `https://itcoach24h.xyz/callback`
   - Remove: `http://localhost:3000` (if no longer needed)
5. **Save changes**

---

## Results

- Frontend deployed and displaying on domain
- Backend Lambda functions have real code
- API endpoints working correctly
- Monitoring system is tracking

**ITCoach system is ready to operate!**

#### Next Steps

Continue to [Cleaning up Resources](../5.14-cleanup/) if you want to delete the entire system.
