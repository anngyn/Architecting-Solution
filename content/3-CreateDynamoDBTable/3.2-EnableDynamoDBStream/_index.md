---
title: "Enable DynamoDB Streams"
weight: 3.2
chapter: false
pre: " <b> 3.2 </b> "
---

ℹ️ **Information:** In this task, you will enable **DynamoDB Streams**.  
A DynamoDB Stream captures information about every modification to data items in the table.

---

### Step by step DynamoDB Streams Configuration

1. Open the **DynamoDB console**.  
2. In the **Tables** section of the navigation pane, choose **Update settings**.  
![image](/images/3-CreateDynamoDBTable/04-dynamo.png)  
3. In the **Tables** card, make sure that the `orders` table is selected.  
4. Choose the **Exports and streams** tab.  
5. In the **DynamoDB stream details** section, choose **Enable**.  
![image](/images/3-CreateDynamoDBTable/05-dynamo.png)  
6. For **View type**, select **New image**.  
7. Choose **Enable stream**.  
![image](/images/3-CreateDynamoDBTable/06-dynamo.png)  

---

🔒 **Note:**  After the Lambda function reads messages from the **SQS queue** and writes an order record to the **DynamoDB table**, **DynamoDB Streams** captures the primary key attributes from the record.  
This allows downstream services (such as Lambda) to process changes in near real-time.
