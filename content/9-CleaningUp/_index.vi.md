---
title: "Dọn dẹp Tài nguyên"
weight: 9
chapter: false
pre: " <b> 9. </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ xóa tất cả các **tài nguyên AWS** đã tạo trong quá trình thực hành để tránh phát sinh chi phí không cần thiết.

---

### Xóa DynamoDB Table

1. Mở **DynamoDB console**.  
2. Trong bảng điều hướng, chọn **Tables**.  
3. Chọn bảng `orders`.  
4. Chọn **Delete** và xác nhận hành động.  

---

### Xóa Lambda Functions

1. Mở **Lambda console**.  
2. Chọn các Lambda function đã tạo trong bài thực hành:  
   - `POC-Lambda-1`  
   - `POC-Lambda-2`  
3. Chọn **Actions → Delete**.  
4. Xác nhận hành động và đóng hộp thoại.  

---

### Xóa SQS Queue

1. Mở **Amazon SQS console**.  
2. Chọn queue đã tạo trong bài thực hành:  
   - `POC-Queue`  
3. Chọn **Delete** và xác nhận hành động.  

---

### Xóa SNS Topic và Subscriptions

1. Mở **Amazon SNS console**.  
2. Trong bảng điều hướng, chọn **Topics**.  
3. Chọn `POC-Topic`.  
4. Chọn **Delete** và xác nhận hành động.  
5. Trong bảng điều hướng, chọn **Subscriptions**.  
6. Chọn subscription đã tạo trong bài thực hành và chọn **Delete**.  
7. Xác nhận hành động.  

---

### Xóa API

1. Mở **API Gateway console**.  
2. Chọn `POC-API`.  
3. Chọn **Actions → Delete**.  
4. Xác nhận hành động.  

---

### Xóa IAM Roles và Policies

1. Mở **IAM console**.  
2. Trong bảng điều hướng, chọn **Roles**.  
3. Xóa các role sau và xác nhận hành động:  
   - `APIGateway-SQS`  
   - `Lambda-SQS-DynamoDB`  
   - `Lambda-DynamoDBStreams-SNS`  

4. Trong bảng điều hướng, chọn **Policies**.  
5. Xóa các policy tùy chỉnh sau và xác nhận hành động:  
   - `Lambda-DynamoDBStreams-Read`  
   - `Lambda-SNS-Publish`  
   - `Lambda-Write-DynamoDB`  
   - `Lambda-Read-SQS`  

---

🎉 **Chúc mừng!**  
Bạn đã hoàn thành bài thực hành và dọn dẹp toàn bộ tài nguyên AWS.
