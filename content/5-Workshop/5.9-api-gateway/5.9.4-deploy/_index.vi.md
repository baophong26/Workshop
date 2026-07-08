---
title: "Deploy API"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.9.4. </b> "
---

#### Deploy API to Stage

**1. Deploy API**

- Click nút **Deploy API** (góc trên phải)

**2. Stage Settings**

- Deployment stage: **New stage**
- Stage name: `prod`
- Stage description: `Production stage`

- Click **Deploy**

**3. Lưu Invoke URL**

Sau khi deploy:
- Copy **Invoke URL**
- Dạng: `https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod`

![Invoke URL](/images/5-Workshop/5.9-api/004-invoke-url.png)


#### Kết quả

✅ API đã được deploy thành công

#### Thông tin cần lưu

```
API Name: itcoach-api
Stage: prod
Invoke URL: https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod
Endpoints: 8 (1 public, 7 protected)
```

#### Test endpoint (optional)

Test endpoint `/auth` bằng cURL:

```bash
curl -X POST https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/auth
```

Kết quả mong đợi:
```json
{
  "message": "itcoach-auth-handler placeholder"
}
```

**4. Cấu hình Throttling (chống spam)**

Để bảo vệ API khỏi spam/abuse:

- Menu trái → **Stages** → click **`prod`**
- Click **Edit** (góc phải mục Stage details)
- Throttle settings:
  - Rate: `100` requests/second
  - Burst: `200`
- **Save**


#### Tổng kết API Gateway

Đã hoàn thành cấu hình API Gateway! 🎉

- ✅ REST API created
- ✅ Cognito Authorizer configured
- ✅ 8 resources with methods
- ✅ CORS enabled
- ✅ Deployed to `prod` stage
- ✅ Throttling configured (100/s, burst 200)

