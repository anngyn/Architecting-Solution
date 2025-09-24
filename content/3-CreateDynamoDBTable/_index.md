---
title: "Create DynamoDB Table and Enable Streams"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### Overview
ℹ️ **Information:** In this section, we will set up **Amazon DynamoDB** to store data and enable **DynamoDB Streams** to capture item changes in the table.  
This enables building an **event-driven workflow**, allowing other AWS services such as Lambda to process data in real time.

---

### Required Resources
To properly configure the environment, we will create and configure the following AWS resources:

- **DynamoDB Table:** The `orders` table will be used to store incoming data from API Gateway.  
- **DynamoDB Streams:** A change data capture feature that records modifications (INSERT, UPDATE, DELETE) in the table and triggers downstream services such as Lambda.

⚠️ **Warning:** Incorrect configuration may lead to:  
- Data not being recorded properly in DynamoDB.  
- Change events not being propagated to downstream services (e.g., Lambda, SNS).  

---

### Workshop Modules
Follow these steps to prepare DynamoDB for the workshop:

1. [Create a **DynamoDB Table**.](3.1-CreateDynamoDBTable/)  
2. [Enable **DynamoDB Streams** on the table.](3.2-EnableDynamoDBStreams/)  

---

### 🔒 Security Note
When designing a **DynamoDB table**, always choose an appropriate **Partition Key** (in this case `orderID`) to optimize queries and partitioning.  
Additionally, enable **Streams** only when necessary to reduce costs and avoid performance overhead.
