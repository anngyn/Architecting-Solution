---
title: "Tạo Lambda Function"
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

### Tổng quan
ℹ️ **Thông tin:** Trong phần này, chúng ta sẽ tạo **AWS Lambda functions** để xử lý quy trình serverless.  
Lambda sẽ đóng vai trò là tầng xử lý, nhận dữ liệu từ **Amazon SQS**, ghi bản ghi vào **DynamoDB**, và chuyển tiếp thay đổi từ cơ sở dữ liệu đến **Amazon SNS** thông qua **DynamoDB Streams**.

---

### Tài nguyên cần thiết
Để cấu hình môi trường một cách chính xác, chúng ta sẽ xây dựng các Lambda function sau:

- **POC-Lambda-1:** Đọc tin nhắn từ hàng đợi SQS và ghi bản ghi vào bảng DynamoDB.  
- **POC-Lambda-2:** Sử dụng DynamoDB Streams làm trigger và xuất bản bản ghi mới đến chủ đề SNS.  

⚠️ **Cảnh báo:** Lambda functions cần được gán đúng **IAM execution roles**.  
Nếu cấu hình sai, có thể dẫn đến:  
- Không thể đọc tin nhắn từ SQS  
- Không thể ghi dữ liệu vào DynamoDB  
- Không thể gửi sự kiện đến SNS  

---

### Các bước thực hiện
Thực hiện lần lượt các bước sau để chuẩn bị Lambda:

1. [Tạo **Lambda function** xử lý tin nhắn từ SQS và ghi vào DynamoDB.](6.1-SQSLambdaDynamoDB/)  
2. [Tạo **Lambda function** xuất bản bản ghi DynamoDB Streams lên SNS.](6.2-DynamoDBStreamstoSNS/)  

---

### 🔒 Ghi chú bảo mật
Luôn tuân thủ **nguyên tắc đặc quyền tối thiểu** khi gán IAM roles cho Lambda.  
Mỗi function chỉ nên có quyền cần thiết cho nhiệm vụ riêng của nó:
- **POC-Lambda-1:** Quyền đọc từ SQS và ghi vào DynamoDB  
- **POC-Lambda-2:** Quyền đọc từ DynamoDB Streams và gửi thông báo đến SNS  
