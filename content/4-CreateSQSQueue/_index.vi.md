---
title: "Tạo Amazon SQS Queue"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ tạo một **Amazon SQS queue**.  
Trong kiến trúc của bài tập này, **Amazon SQS** sẽ nhận các bản ghi dữ liệu từ **API Gateway**, lưu trữ chúng và sau đó gửi đến cơ sở dữ liệu.

---

### Tạo Queue

1. Trong ô tìm kiếm của **AWS Management Console**, nhập **SQS** và từ danh sách, chọn **Simple Queue Service**.  
2. Trên thẻ **Get started**, chọn **Create queue**.  
![image](/images/4-CreateSQSQueue/01-sqs.png)  
3. Trang **Create queue** sẽ xuất hiện.  
4. Cấu hình các thiết lập sau:  
   - **Name:** `POC-Queue`  
   - **Access Policy:** Basic  
![image](/images/4-CreateSQSQueue/02-sqs.png) 

---

### Cấu hình Quyền truy cập

- **Xác định ai có thể gửi message đến queue**  
  - Chọn **Only the specified AWS accounts, IAM users and roles**.  
  - Trong ô nhập, dán Amazon Resource Name (ARN) của **APIGateway-SQS IAM role**.  
    - Ví dụ:  
      ```
      arn:aws:iam::<account ID>:role/APIGateway-SQS
      ```

- **Xác định ai có thể nhận message từ queue**  
  - Chọn **Only the specified AWS accounts, IAM users and roles**.  
  - Trong ô nhập, dán ARN của **Lambda-SQS-DynamoDB IAM role**.  
    - Ví dụ:  
      ```
      arn:aws:iam::<account ID>:role/Lambda-SQS-DynamoDB
      ```
![image](/images/4-CreateSQSQueue/03-sqs.png) 

---

### Hoàn tất

- Chọn **Create queue**.  

---

🔒 **Ghi chú bảo mật:** Bằng cách giới hạn quyền **gửi** cho API Gateway và quyền **nhận** cho Lambda function, bạn đảm bảo rằng queue chỉ được sử dụng bởi các dịch vụ được định sẵn, tuân thủ nguyên tắc **least privilege**.
