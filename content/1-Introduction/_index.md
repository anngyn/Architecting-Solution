---
title: "Introduction"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

### Use case

Imagine a customer in the cleaning supply business who experiences significant spikes in website traffic. They require a highly scalable architecture that can automatically adjust to fluctuating demand while ensuring that its application components are loosely coupled for greater resilience and maintainability.

### Architectural Overview

The solution you will build is illustrated in the architectural diagram below. It demonstrates a fully event-driven, serverless data processing workflow:

![Architecture diagram for exercise 1](/images/exercise-1.png)

The process flow is as follows:

1.  A request is sent to a **REST API** (Amazon API Gateway) to submit a new data entry.
2.  The API Gateway places the entry as a message into an **Amazon SQS** queue.
3.  The SQS queue triggers a **Lambda function**, which processes the message and inserts the data into a **DynamoDB** table.
4.  **DynamoDB Streams** captures this new database entry as a change event.
5.  This event stream invokes a second **Lambda function**.
6.  The second Lambda function forwards the entry to an **Amazon SNS** topic.
7.  Finally, Amazon SNS sends an email notification to a subscribed address, confirming the data has been processed.

### What You'll Learn

By completing this exercise, you will gain hands-on experience with:

- Creating **IAM policies and roles** to adhere to the principle of least privilege.
- Setting up a **DynamoDB table** for data persistence.
- Configuring an **Amazon SQS queue** for message decoupling.
- Developing **Lambda functions** and configuring triggers to orchestrate workflows between AWS services.
- Enabling **DynamoDB Streams** to capture real-time data modifications.
- Configuring **Amazon SNS** for push notifications.
- Deploying a **REST API** using Amazon API Gateway to serve as the application's entry point.

### Important Notes:

{{% notice note %}}
Please ensure you are operating in the **US East (N. Virginia) `us-east-1`** Region in the AWS Management Console for all steps in this exercise.
{{% /notice %}}

{{% notice note %}}
When prompted for your account ID, use the 12-digit number found in the top-right corner of the AWS Management Console. Make sure to remove any hyphens.
{{% /notice %}}




