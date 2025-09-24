---
title: "Tạo Bảng DynamoDB"
weight: 3.1
chapter: false
pre: " <b> 3.1 </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ tạo một **bảng DynamoDB** để tiếp nhận dữ liệu được truyền qua **API Gateway**.

---

### Các bước tạo bảng DynamoDB

1. Trong ô tìm kiếm của **AWS Management Console**, nhập **DynamoDB**.  
2. Từ danh sách, chọn dịch vụ **DynamoDB**.  
![image](/images/3-CreateDynamoDBTable/01-dynamo.png)  
3. Trên thẻ **Get started**, chọn **Create table**.  
![image](/images/3-CreateDynamoDBTable/02-dynamo.png)  
4. Cấu hình các thiết lập sau:  
   - **Table name (Tên bảng):** `orders`  
   - **Partition key (Khóa phân vùng):** `orderID`  
   - **Data type (Kiểu dữ liệu):** String  
5. Giữ nguyên các thiết lập còn lại ở giá trị mặc định.  
6. Chọn **Create table**.  
![image](/images/3-CreateDynamoDBTable/03-dynamo.png)  

---

🔒 **Ghi chú bảo mật:** Bằng cách sử dụng một **partition key** cụ thể (`orderID`), bảng DynamoDB sẽ được tối ưu cho việc truy vấn và lưu trữ dữ liệu liên quan đến đơn hàng được gửi từ API Gateway.
