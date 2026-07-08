---
title: "Blog 2 - AWS Agentic AI"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS AGENTIC AI – INTELLIGENT AI APPLICATION IN SAP ERP SYSTEMS

During my internship and exploration of AI services on the AWS platform, **Agentic AI** is one of the prominent topics related to applying Generative AI to enterprise business systems.

According to the article "Transforming ERP with Agentic AI" published by AWS and Accenture, Agentic AI is built to support Exception Management in SAP ERP systems, helping to simplify the data analysis process, identify root causes of incidents, and support providing appropriate solutions.

## OVERALL ARCHITECTURE

In this solution, Agentic AI operates as an intelligent assistant capable of analyzing data and supporting problem resolution in ERP processes.

Users can interact with the system through a natural conversation interface. The AI Agent will retrieve data from SAP S/4HANA, combine it with SOP documents, business data, and previous processing history to identify the cause of the incident as well as suggest appropriate solutions.

![AWS Agentic AI Architecture](/images/blog2.jpg)

The architecture is built on AWS services such as:

* **Amazon Bedrock** - AI/ML platform
* **Bedrock AgentCore** - Orchestration and reasoning
* **AWS Lambda** - Serverless compute
* **Amazon RDS** - Database management
* **AWS Step Functions** - Workflow orchestration

The combination of these services allows Agentic AI to perform data retrieval, reasoning, and support users in solving complex business problems.

## DIGITAL ASSISTANT – AI ASSISTANT IN ERP

One of the notable components of the architecture is the **Digital Assistant**.

Instead of having to look up multiple documentation sources or rely entirely on the experience of the operations team, users can use natural language to interact with the system.

Digital Assistant capabilities:

* Retrieve information related to incidents
* Search for processing guides
* Aggregate data from multiple sources
* Support explaining root causes of errors
* Suggest appropriate processing steps

This model helps simplify the information access process and support improving business processing efficiency.

## AGENTIC AI – FROM CHATBOT TO REASONING SYSTEM

The difference of Agentic AI lies in its ability to perform multiple reasoning steps to solve a specific goal.

Unlike traditional chatbots that only provide answers based on queried content, Agentic AI can:

* Analyze business data
* Identify root causes of errors
* Link data from different systems
* Propose solutions
* Support users in decision-making processes

This is one of the important development directions of Generative AI when AI not only generates content but also participates in supporting the solution of real operational problems.

## SIGNIFICANCE FOR AWS TECHNOLOGY LEARNING

In the AWS internship and learning environment, Agentic AI is a typical example of combining AI services, business data, and enterprise operational processes.

Through this architecture, we can see the role of services like Amazon Bedrock and Bedrock AgentCore not only stops at deploying large language models but also supports building AI Agents capable of handling complex tasks in real environments.

This is also a typical example of the development trend of Generative AI in ERP systems and Business Applications today.

## CONCLUSION

Agentic AI is opening up a new approach to applying artificial intelligence to ERP systems. Through its ability to analyze data, reason, and support exception handling, this solution shows great potential in improving operational efficiency and optimizing business processes.

In addition, the Agentic AI architecture also shows how AWS is combining Amazon Bedrock, Bedrock AgentCore, and related services to build AI systems capable of supporting real problem-solving instead of just stopping at traditional chatbot applications.

**Original article link:** [Transforming ERP with Agentic AI](https://aws.amazon.com/vi/blogs/awsforsap/transforming-erp-with-agentic-ai/)