---
title: "Create Users Table"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

#### Purpose

The `itcoach-users` table stores user information and profiles.

#### Steps

**1. Access DynamoDB Console**

- Search for **DynamoDB** in the AWS Console search bar
- Click on **DynamoDB**

**2. Create New Table**

- Click the **Create table** button

![Create Table](/images/5-Workshop/5.5-dynamodb/001-create-table.png)

**3. Configure Table**

**Table details:**
- Table name: `itcoach-users`
- Partition key: `userId` - Type: **String**
- Sort key: *(leave empty - not needed)*

**Table settings:**
- Select **Customize settings**

**Read/write capacity settings:**
- Capacity mode: select **On-demand**

**Secondary indexes:**
- No need to create (leave empty)

**Encryption at rest:**
- Keep default: **Owned by Amazon DynamoDB**

![Table Users](/images/5-Workshop/5.5-dynamodb/002-table-users.png)

- Click **Create table**

**4. Wait for Table Creation**

The table creation process takes about 10-30 seconds. Status will change from **Creating** to **Active**.

#### Result

✅ Table `itcoach-users` created successfully

#### Sample Data Structure

```json
{
  "userId": "user-123456",
  "email": "student@example.com",
  "name": "Nguyen Van A",
  "specialty": "frontend",
  "level": "fresher",
  "createdAt": "2026-04-17T10:00:00Z",
  "lastLogin": "2026-07-05T08:30:00Z"
}
```

#### Information to Save

```
Table Name: itcoach-users
Partition Key: userId (String)
Sort Key: None
Capacity Mode: On-demand
```

#### Next Steps

Move to the next step to create the Questions table.
