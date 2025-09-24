---
title: "Test the Architecture using API Gateway"
weight: 8
chapter: false
pre: " <b> 8. </b> "
---

ℹ️ **Information:** In this task, you will use **API Gateway** to send mock data to **Amazon SQS** as a proof of concept for the serverless solution.

---

### Sending a Test Request

1. In the **API Gateway console**, return to the **POST - Method Execution** page and choose **Test**.  
2. In the **Request Body** box, enter:  

    ```json
    {  
      "item": "latex gloves",
      "customerID": "12345"
    }
    ```

3. Choose **Test**.  
![image](/images/8-TestingtheArchitecture/8.test.png)
---

### Verifying the Results

- If you see the **“Successfully completed execution”** message with a **200 response** in the logs on the right, you should also receive an **email notification** with the new entry.  
![image](/images/8-TestingtheArchitecture/9.result.png)
- If you don’t receive an email but the new item appears in the **DynamoDB table**, review and troubleshoot the exercise steps starting after you set up **DynamoDB**.  
- Ensure that all resources are deployed in the **us-east-1 Region**.  
![image](/images/8-TestingtheArchitecture/10.result.png)
---

### End-to-End Flow

After **API Gateway** successfully processes the request:  

1. API Gateway places the request in the **SQS queue**.  
2. Because you set up Amazon SQS as a trigger in the first Lambda function, **SQS invokes the Lambda function**.  
3. The first Lambda function writes the new entry into the **DynamoDB table**.  
4. **DynamoDB Streams** captures this database change and triggers the second Lambda function.  
5. The second Lambda function gets the new record from **DynamoDB Streams** and sends it to **Amazon SNS**.  
6. **Amazon SNS** delivers an **email notification** to the subscribed endpoint.  

---

🔒 **Security Note:**  
This end-to-end test confirms that the entire **serverless pipeline** (API Gateway → SQS → Lambda → DynamoDB → DynamoDB Streams → Lambda → SNS → Email) works securely and as expected.
