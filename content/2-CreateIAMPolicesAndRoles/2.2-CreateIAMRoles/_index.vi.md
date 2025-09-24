---
title: "Tạo IAM Roles"
weight: 2.2
chapter: false
pre: " <b> 2.2 </b> "
---

ℹ️ **Thông tin:** Vì AWS tuân thủ nguyên tắc **least privilege**, chúng tôi khuyến nghị chỉ cấp quyền truy cập dựa trên role cho những tài nguyên AWS thực sự cần thiết để thực hiện tác vụ. Trong bước này, bạn sẽ tạo **IAM Roles** và gắn các policy tương ứng.

---

### Tạo IAM Roles từng bước

1. **Tạo IAM Role cho Lambda (DynamoDB + SQS)**  
    - Trong bảng điều hướng của **IAM dashboard**, chọn **Roles**.  
    ![Roles](/images/2-CreateIAMPolicesAndRoles/01-policy.png)  
    - Chọn **Create role** và cấu hình như sau trong trang **Select trusted entity**:  
        - **Trusted entity type:** AWS service  
        - **Common use cases:** Lambda  
    ![Roles](/images/2-CreateIAMPolicesAndRoles/02-role.png)  
    - Chọn **Next**.  
    - Trong trang **Add permissions**, chọn:  
        - `Lambda-Write-DynamoDB`  
        - `Lambda-Read-SQS`  
    ![Roles](/images/2-CreateIAMPolicesAndRoles/03-roles.png)  
    - Chọn **Next**.  
    - Với **Role name**, nhập: `Lambda-SQS-DynamoDB`  
    - Chọn **Create role**.  
    ![Roles](/images/2-CreateIAMPolicesAndRoles/04-roles.jpg)  

---

2. **Tạo IAM Role cho Lambda (DynamoDB Streams + SNS)**  
    - Thực hiện các bước tương tự ở trên với cấu hình sau:  
        - **IAM role name:** `Lambda-DynamoDBStreams-SNS`  
        - **Trusted entity type:** AWS service  
        - **Common use cases:** Lambda  
        - **Attach policies:**  
            - `Lambda-SNS-Publish`  
            - `Lambda-DynamoDBStreams-Read`  

---

3. **Tạo IAM Role cho API Gateway (SQS + CloudWatch)**  
    - Thực hiện các bước tương tự ở trên với cấu hình sau:  
        - **IAM role name:** `APIGateway-SQS`  
        - **Trusted entity type:** AWS service  
        - **Common use cases:** API Gateway  
        - **Attach policies:**  
            - `AmazonAPIGatewayPushToCloudWatchLogs`  

---

🔒 **Ghi chú bảo mật:** Việc gắn các policy chỉ cho những role cần thiết giúp tuân thủ nguyên tắc **least privilege**, đảm bảo Lambda và API Gateway chỉ có đủ quyền để thực hiện nhiệm vụ mà không có thêm quyền dư thừa.
