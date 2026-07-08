---
title: "Blog 1 - AWS Systems Manager"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS SYSTEMS MANAGER – CENTRALIZED MANAGEMENT SOLUTION FOR HYBRID CLOUD ENVIRONMENTS

When businesses operate infrastructure simultaneously on AWS and On-Premises systems, server management often becomes complex due to the need to use multiple different tools, open SSH or RDP ports for remote access, and perform many manual operational tasks.

To solve this problem, AWS provides **AWS Systems Manager (SSM)** – a service that helps centrally manage resources on AWS as well as servers outside AWS from a single platform.

## OVERALL ARCHITECTURE

In this architecture, AWS Systems Manager acts as the central orchestrator. Administrators can use AWS Console, AWS CLI, SDK, or PowerShell to manage EC2 Windows, Linux, macOS as well as physical servers or virtual machines in On-Premises environments.

![AWS Systems Manager Architecture](/images/blog1.jpg)

## SESSION MANAGER – SECURE SERVER ACCESS

One of the most prominent features of AWS Systems Manager is **Session Manager**. Instead of having to open SSH or RDP ports to access servers, users can connect directly through AWS Console or AWS CLI without needing to open any inbound ports on the system.

This solution brings many benefits:

* **Enhanced security** - No need to open SSH/RDP ports to the Internet
* **No Bastion Host needed** - Save costs and reduce complexity
* **No SSH Key management** - Simplify access management
* **Record access history** - Full audit trail with CloudTrail
* **Reduce risk of Internet attacks** - Don't expose management ports

## PATCH MANAGER – AUTOMATED SYSTEM UPDATES

In addition to Session Manager, AWS Systems Manager also provides **Patch Manager** to automate the operating system update process.

The service supports:

* Scanning for missing patches
* Automated system updates
* Scheduled periodic maintenance
* Update status monitoring

## PRACTICAL EXPERIENCE

During the learning process, I had the opportunity to deploy AWS Systems Manager on Windows EC2, perform SSM Agent configuration, assign IAM Role, connect using Session Manager, and set up Port Forwarding to access Remote Desktop.

Through hands-on practice, I found this to be a very useful solution that simplifies server administration while enhancing system security.

## CONCLUSION

AWS Systems Manager is a powerful service that helps businesses manage Hybrid Cloud environments in a centralized, secure, and efficient manner. With features like Session Manager, Patch Manager, and the ability to integrate with CloudWatch, CloudTrail, and Amazon S3, this is one of the notable services when deploying infrastructure on AWS.

**Original article link:** [Using AWS Systems Manager in Hybrid Cloud Environments](https://aws.amazon.com/blogs/architecture/using-aws-systems-manager-in-hybrid-cloud-environments/)