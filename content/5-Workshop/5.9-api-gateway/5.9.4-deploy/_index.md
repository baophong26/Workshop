---
title: "Deploy API"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.9.4. </b> "
---

#### Deploy API to Stage

**1. Deploy API**

- Click **Deploy API** button (top right corner)

**2. Stage Settings**

- Deployment stage: **New stage**
- Stage name: `prod`
- Stage description: `Production stage`

- Click **Deploy**

**3. Save Invoke URL**

After deployment:
- Copy **Invoke URL**
- Format: `https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod`

![Invoke URL](/images/5-Workshop/5.9-api/004-invoke-url.png)


#### Result

✅ API deployed successfully

#### Information to Save

```
API Name: itcoach-api
Stage: prod
Invoke URL: https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod
Endpoints: 8 (1 public, 7 protected)
```

#### Test Endpoint (optional)

Test `/auth` endpoint using cURL:

```bash
curl -X POST https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/auth
```

Expected result:
```json
{
  "message": "itcoach-auth-handler placeholder"
}
```

**4. Configure Throttling (anti-spam)**

To protect API from spam/abuse:

- Left menu → **Stages** → click **`prod`**
- Click **Edit** (top right of Stage details section)
- Throttle settings:
  - Rate: `100` requests/second
  - Burst: `200`
- **Save**


#### API Gateway Summary

Completed API Gateway configuration! 🎉

- ✅ REST API created
- ✅ Cognito Authorizer configured
- ✅ 8 resources with methods
- ✅ CORS enabled
- ✅ Deployed to `prod` stage
- ✅ Throttling configured (100/s, burst 200)
