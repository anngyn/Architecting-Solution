---
title: "Create API with Amazon API Gateway"
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

ℹ️ **Information:** In this task, you will create a **REST API** in **Amazon API Gateway**.  
The API serves as a communication gateway between your application and AWS services.

---

### Creating the REST API

1. In the **AWS Management Console**, search for and open **API Gateway**.  
![image](/images/7-CreateAPIGateway/1-search.png) 
2. On the **REST API** card (with public authentication), choose **Build** and configure the following settings:  
   - **Choose the protocol:** REST  
   - **Create new API:** New API  
   - **API name:** `POC-API`  
   - **Endpoint Type:** Regional  
3. Choose **Create API**.  
![image](/images/7-CreateAPIGateway/2-create.png)
---

### Configuring the POST Method

1. On the **Actions** menu, choose **Create Method**.  
![image](/images/7-CreateAPIGateway/3-createmethod.png)
2. Open the method menu by selecting the down arrow and choose **POST**.  
3. Save your changes by selecting the check mark.  
4. In the **POST - Setup** pane, configure the following settings:  
   - **Integration type:** AWS Service  
![image](/images/7-CreateAPIGateway/4-config.png)
   - **AWS Region:** ap-southeast-1  
   - **AWS Service:** Simple Queue Service (SQS)  
   - **AWS Subdomain:** *leave empty*  
   - **HTTP method:** POST  
   - **Action Type:** Use path override  
   - **Path override:** `<account ID>/POC-Queue`  
     - ⚠️ Example: If `POC-Queue` is the SQS queue name, the entry might look like:  
       ```
       /123456789012/POC-Queue
       ```
   - **Execution role:** Paste the ARN of the `APIGateway-SQS` role  
     - Example:  
       ```
       arn:aws:iam::<account ID>:role/APIGateway-SQS
       ```
   - **Content Handling:** Passthrough  
![image](/images/7-CreateAPIGateway/5-config.png)
5. For **Request body passthrough**, choose **Never**. 
6. Scroll to the bottom of the page and expand **HTTP Headers**.  
7. Choose **Add header**.  
   - **Name:** Content-Type  
   - **Mapped from:** `'application/x-www-form-urlencoded'`   
 
8. Choose **Add mapping template**.  
   - **Content-Type:** `application/json`  
9. For **Generate template**, do not choose a default template.  
   - Instead, enter the following command in the box:  `Action=SendMessage&MessageBody=$input.body`
10. Save your changes by selecting the check mark. 
![image](/images/7-CreateAPIGateway/7-add.png)