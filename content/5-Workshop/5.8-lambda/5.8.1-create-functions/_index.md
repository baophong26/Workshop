---
title: "Create 8 Lambda Functions"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.8.1. </b> "
---

#### Process to Create 1 Lambda (repeat 8 times)

I'll provide detailed instructions for the first function, repeat similarly for the remaining ones.

#### Create Function 1: itcoach-auth-handler

**1. Access Lambda Console**

- Search for **Lambda** in search bar
- Click on **AWS Lambda**

**2. Create Function**

- Click **Create function**

**3. Configure Function**

- Select **Author from scratch**
- Function name: `itcoach-auth-handler`
- Runtime: **Python 3.12**

**4. Permissions - IMPORTANT**

- Scroll down to **Permissions** section
- Click **▶ Additional settings** to expand
- Execution role: select **Use an existing role**
- Existing role: select **`itcoach-lambda-role`** (created in step 5.3)

![Create Function](/images/5-Workshop/5.8-lambda/001-create-function.png)

- Click **Create function**

**5. Deploy Placeholder Code**

After function is created:

- **Code** tab → Delete default code
- Paste the following placeholder code:

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Headers': 'Content-Type,Authorization',
            'Access-Control-Allow-Methods': 'GET,POST,PUT,DELETE,OPTIONS'
        },
        'body': json.dumps({'message': 'itcoach-auth-handler placeholder'})
    }
```

![Placeholder Code](/images/5-Workshop/5.8-lambda/002-placeholder-code.png)

- Click **Deploy**

**6. Configuration - Timeout and Memory**

- **Configuration** tab → **General configuration** → **Edit**
- Timeout: `30` seconds
- Memory: `256` MB
- Click **Save**

#### Repeat for 7 Remaining Functions

Follow the same steps above for 7 functions:

| # | Function Name | Code placeholder message |
|---|--------------|--------------------------|
| 2 | `itcoach-question-handler` | 'itcoach-question-handler placeholder' |
| 3 | `itcoach-session-handler` | 'itcoach-session-handler placeholder' |
| 4 | `itcoach-answer-handler` | 'itcoach-answer-handler placeholder' |
| 5 | `itcoach-ai-processor` | 'itcoach-ai-processor placeholder' |
| 6 | `itcoach-result-handler` | 'itcoach-result-handler placeholder' |
| 7 | `itcoach-quiz-handler` | 'itcoach-quiz-handler placeholder' |
| 8 | `itcoach-gamification-handler` | 'itcoach-gamification-handler placeholder' |


#### Verify 8 Functions Created

Back on Lambda Dashboard, you'll see 8 functions.

#### Result

✅ Created 8 Lambda functions with:
- Runtime: Python 3.12
- Role: itcoach-lambda-role
- Timeout: 30s
- Memory: 256 MB
- Placeholder code with CORS headers

#### Next Steps

Move to the next step to configure Environment Variables for each function.
