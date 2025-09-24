---
title: "Bật DynamoDB Streams"
weight: 3.2
chapter: false
pre: " <b> 3.2 </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ bật **DynamoDB Streams**.  
DynamoDB Streams ghi lại thông tin về mọi thay đổi trên các mục dữ liệu trong bảng.

---

### Các bước cấu hình DynamoDB Streams

1. Mở **DynamoDB console**.  
2. Trong phần **Tables** của thanh điều hướng, chọn **Update settings**.  
![image](/images/3-CreateDynamoDBTable/04-dynamo.png)  
3. Trong thẻ **Tables**, đảm bảo rằng bảng `orders` đã được chọn.  
4. Chọn tab **Exports and streams**.  
5. Trong phần **DynamoDB stream details**, chọn **Enable**.  
![image](/images/3-CreateDynamoDBTable/05-dynamo.png)  
6. Với tùy chọn **View type**, chọn **New image**.  
7. Chọn **Enable stream**.  
![image](/images/3-CreateDynamoDBTable/06-dynamo.png)  

---

🔒 **Ghi chú:** Sau khi hàm **Lambda** đọc các tin nhắn từ **SQS queue** và ghi bản ghi đơn hàng vào **DynamoDB table**, **DynamoDB Streams** sẽ ghi lại các thuộc tính khóa chính từ bản ghi đó.  
Điều này cho phép các dịch vụ downstream (chẳng hạn như Lambda) xử lý thay đổi gần như theo thời gian thực.
