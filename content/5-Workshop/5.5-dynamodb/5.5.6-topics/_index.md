---
title: "Create Topics Table"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.5.6. </b> "
---

#### Purpose

The `itcoach-topics` table stores topic lists by specialty (Frontend → JavaScript, React, CSS; Backend → Node.js, Python, Database; etc.)

#### Table Configuration

- Table name: `itcoach-topics`
- Partition key: `specialty` - **String**
- Sort key: `topicId` - **String**
- Capacity mode: **On-demand**

![Topics Composite](/images/5-Workshop/5.5-dynamodb/005-table-topics-composite.png)


#### No Global Secondary Index Needed

No GSI needed because `specialty` is already the Partition Key.

#### Sample Data Structure

```json
{
  "specialty": "frontend",
  "topicId": "topic-fe-js",
  "topicName": "JavaScript Fundamentals",
  "description": "Variables, functions, scope, closure, etc.",
  "order": 1,
  "totalQuestions": 45
}
```

```json
{
  "specialty": "frontend",
  "topicId": "topic-fe-react",
  "topicName": "React Basics",
  "description": "Component, Props, State, Hooks",
  "order": 2,
  "totalQuestions": 38
}
```

#### Result

✅ Table `itcoach-topics` with Composite Key
