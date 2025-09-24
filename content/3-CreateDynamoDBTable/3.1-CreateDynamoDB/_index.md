---
title: "Create DynamoDB Table"
weight: 3.1
chapter: false
pre: " <b> 3.1 </b> "
---

ℹ️ **Information:** In this task, you will create a **DynamoDB table** that ingests data passed on through **API Gateway**.

---

### Step by step DynamoDB Table Creation

1. In the search box of the **AWS Management Console**, enter **DynamoDB**.  
2. From the list, choose the **DynamoDB** service.
![image](/images/3-CreateDynamoDBTable/01-dynamo.png)  
3. On the **Get started** card, choose **Create table**. 
![image](/images/3-CreateDynamoDBTable/02-dynamo.png)   
4. Configure the following settings:  
    - **Table name:** `orders`  
    - **Partition key:** `orderID`  
    - **Data type:** String  
5. Keep the remaining settings at their default values.  
6. Choose **Create table**.  
![image](/images/3-CreateDynamoDBTable/03-dynamo.png)  

---

🔒 **Security Note:**  By using a specific partition key (`orderID`), the DynamoDB table will be optimized for querying and storing order-related data received from API Gateway.
