---
title: "Create Questions Table"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

#### Purpose

The `itcoach-questions` table stores the question bank used for both **Quiz** and **Essay**. Differentiated by the `type` field: `"QUIZ"` or `"ESSAY"`.

#### Table Configuration

- Table name: `itcoach-questions`
- Partition key: `questionId` - **String**
- Sort key: *(none)*
- Capacity mode: **On-demand**

![Table Questions GSI](/images/5-Workshop/5.5-dynamodb/004-table-questions-gsi.png)

#### Create Global Secondary Index

After table is created (Status = Active):

1. Click on table name `itcoach-questions`
2. Select **Indexes** tab
3. Click **Create index**

**Index configuration:**
- Partition key: `category` - **String**
- Sort key: *(none)*
- Index name: `category-index`
- Attribute projections: **All**

![Create GSI](/images/5-Workshop/5.5-dynamodb/003-create-gsi.png)

4. Click **Create index**


#### Sample Data Structure

**Quiz Question:**
```json
{
  "questionId": "q_fe_001",
  "type": "QUIZ",
  "category": "frontend",
  "topicId": "topic-fe-js",
  "level": "fresher",
  "question": "How is Virtual DOM different from Real DOM?",
  "options": ["Faster", "Slower", "Same", "Not related"],
  "correctAnswers": [0],
  "multiSelect": false
}
```

**Essay Question:**
```json
{
  "questionId": "e_be_001",
  "type": "ESSAY",
  "category": "backend",
  "topicId": "topic-be-api",
  "level": "junior",
  "question": "Explain the difference between REST and GraphQL?",
  "sampleAnswer": "REST is..., GraphQL is..."
}
```

#### Result

✅ Table `itcoach-questions` with GSI `category-index`
