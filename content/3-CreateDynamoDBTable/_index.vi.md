---
title: "Create DynamoDB Table and Enable Streams"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### Overview
ℹ️ **Thông tin:** Trong phần này, chúng ta sẽ thiết lập **DynamoDB** để lưu trữ dữ liệu và bật **DynamoDB Streams** nhằm ghi nhận các thay đổi trong bảng.  
Điều này cho phép xây dựng quy trình **event-driven** (theo sự kiện), giúp các dịch vụ khác như Lambda có thể xử lý dữ liệu theo thời gian thực.

---

### Required Resources
Để cấu hình đúng môi trường, chúng ta sẽ tạo và thiết lập các tài nguyên sau:

- **DynamoDB Table:** Bảng `orders` dùng để lưu dữ liệu đầu vào từ API Gateway.  
- **DynamoDB Streams:** Dòng sự kiện ghi lại các thay đổi (INSERT, UPDATE, DELETE) trong bảng, dùng để kích hoạt Lambda function.

⚠️ **Cảnh báo:** Việc cấu hình không đúng có thể dẫn đến:  
- Dữ liệu không được ghi nhận đúng cách trong DynamoDB.  
- Các sự kiện thay đổi không được phản ánh tới các dịch vụ downstream (ví dụ Lambda, SNS).  

---

### Workshop Modules
Thực hiện các bước sau để chuẩn bị DynamoDB cho workshop:

1. [Tạo bảng **DynamoDB**.](3.1-CreateDynamoDBTable/)  
2. [Bật **DynamoDB Streams** cho bảng.](3.2-EnableDynamoDBStreams/)  

---

### 🔒 Ghi chú bảo mật
Khi thiết kế bảng **DynamoDB**, hãy sử dụng **Partition Key** phù hợp (ở đây là `orderID`) để tối ưu cho việc truy vấn và phân vùng dữ liệu.  
Ngoài ra, chỉ bật **Streams** khi thực sự cần thiết nhằm giảm chi phí và hạn chế rủi ro về hiệu năng.
