---
title: "Blog 3 - AWS Security Analytics"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AWS SECURITY ANALYTICS – BUILDING CLOUD SIEM SYSTEM WITH AMAZON OPENSEARCH AND SECURITY LAKE

In modern cloud computing environments, collecting, standardizing, and analyzing security logs from multiple sources (VPC Flow Logs, CloudTrail, DNS Logs) has always been a challenging problem. Setting up and maintaining traditional SIEM (Security Information and Event Management) systems often requires complex server configuration and is very difficult to scale when network log volumes surge.

In mid-2024, AWS introduced an optimal approach: combining **Amazon Security Lake** with **Amazon OpenSearch** clusters. This architecture provides a fully cloud-based Security Analytics solution that automatically standardizes data to a common format and analyzes threats in real-time without the need to maintain physical infrastructure.

## OVERALL ARCHITECTURE

In this architecture, the security event processing workflow is automated end-to-end from collection to alerting.

All logs from the network infrastructure will be pushed to Amazon Security Lake. Instead of using complex data transformation tools, the system leverages **OpenSearch Ingestion Pipeline** to push data directly into the Amazon OpenSearch Service cluster. This cluster is securely placed in a VPC, spanning 3 Availability Zones to ensure High Availability. All network infrastructure and automation settings are automatically deployed through CloudFormation combined with AWS Lambda.

![AWS Security Analytics Architecture](/images/blog3.jpg)

## AMAZON OPENSEARCH SECURITY ANALYTICS – CLOUD SOC CENTER

The core component of the solution is **OpenSearch Security Analytics**.

Going beyond the capabilities of a simple log search tool, this service provides industry-standard security rules and visual monitoring dashboards out of the box.

The solution brings many outstanding benefits:

* **No manual ETL** - No effort needed to build or maintain ETL pipelines
* **Automatic standardization** - Standardize all log formats to OCSF (Open Cybersecurity Schema Framework)
* **Real-time detection** - Detect network risks and anomalous activities almost instantly (Near Real-time)
* **Zero-ETL** - Query historical data stored in Security Lake directly without copying data
* **Easy alerting** - Route incident alerts via Amazon SQS or SNS

## PRACTICAL EXPERIENCE

Having directly set up a centralized SIEM firewall monitoring system with the **pfSense, Suricata, and ELK Stack** trio, I deeply understand the hardships in configuring pipelines to analyze each log line or having to continuously optimize resources for Elasticsearch nodes.

Approaching the Security Analytics architecture that AWS has promoted since 2024 brings a valuable upgrade. Essentially, OpenSearch is a direct successor from the familiar ELK ecosystem, so management concepts are very familiar. However, the combination with Security Lake and AWS Lambda has turned it into a fully automated processing flow.

No more worries about virtual servers being bottlenecked when the amount of alerts from IDS/IPS systems becomes too large; instead, this cloud-native architecture automatically scales, allowing operations teams to focus maximum effort on analyzing and responding to network threats.

## CONCLUSION

Building a centralized security monitoring system is no longer synonymous with "assembling" individual open-source components and maintaining servers manually. With the combination of Amazon OpenSearch and Security Lake, large-scale network systems possess a solid SIEM platform capable of processing Terabytes of logs daily.

By fully leveraging AWS's scalability, setting up a comprehensive security analytics center can now be completed more quickly and efficiently than ever before.

**Original article link:** [How to Deploy an Amazon OpenSearch Cluster to Ingest Logs from Amazon Security Lake](https://aws.amazon.com/blogs/security/how-to-deploy-an-amazon-opensearch-cluster-to-ingest-logs-from-amazon-security-lake/)
