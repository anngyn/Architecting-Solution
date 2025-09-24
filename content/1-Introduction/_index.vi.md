---
title: "Giới thiệu"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

### Tình huống sử dụng (Use case)

Hãy tưởng tượng một khách hàng trong lĩnh vực cung cấp dụng cụ vệ sinh đang gặp phải tình trạng lưu lượng truy cập website tăng đột biến. Họ cần một kiến trúc có khả năng **tự động mở rộng (scalable)** để thích ứng với nhu cầu biến động, đồng thời đảm bảo rằng các thành phần ứng dụng được **liên kết lỏng lẻo (loosely coupled)** nhằm nâng cao khả năng chịu lỗi (resilience) và khả năng bảo trì.

### Tổng quan Kiến trúc

Giải pháp bạn sẽ xây dựng được minh họa trong sơ đồ kiến trúc bên dưới. Nó cho thấy một **quy trình xử lý dữ liệu hoàn toàn sự kiện (event-driven), serverless**:

![Architecture diagram for exercise 1](/images/exercise-1.png)

Quy trình hoạt động như sau:

1. Một yêu cầu được gửi đến **REST API** (Amazon API Gateway) để gửi dữ liệu mới.  
2. API Gateway đưa dữ liệu này vào **Amazon SQS** queue dưới dạng message.  
3. SQS queue kích hoạt một **Lambda function**, hàm này xử lý message và ghi dữ liệu vào bảng **DynamoDB**.  
4. **DynamoDB Streams** ghi nhận entry mới trong bảng dưới dạng một sự kiện thay đổi.  
5. Dòng sự kiện này kích hoạt một **Lambda function** thứ hai.  
6. Lambda function thứ hai gửi bản ghi đến **Amazon SNS** topic.  
7. Cuối cùng, Amazon SNS gửi một email thông báo đến địa chỉ đã đăng ký, xác nhận dữ liệu đã được xử lý.  

### Bạn sẽ học được gì

Sau khi hoàn thành bài thực hành, bạn sẽ có trải nghiệm thực tế với:  

- Tạo **IAM policies và roles** để tuân thủ nguyên tắc *least privilege*.  
- Thiết lập **DynamoDB table** để lưu trữ dữ liệu.  
- Cấu hình **Amazon SQS queue** để tách biệt (decouple) luồng message.  
- Xây dựng **Lambda functions** và thiết lập triggers để điều phối workflow giữa các dịch vụ AWS.  
- Bật **DynamoDB Streams** để ghi nhận thay đổi dữ liệu theo thời gian thực.  
- Cấu hình **Amazon SNS** để gửi thông báo.  
- Triển khai **REST API** bằng Amazon API Gateway để làm điểm truy cập cho ứng dụng.  

### Ghi chú quan trọng:

{{% notice note %}}
Hãy đảm bảo rằng bạn đang thao tác trong Region **US East (N. Virginia) `us-east-1`** trên AWS Management Console cho tất cả các bước trong bài thực hành này.  
{{% /notice %}}

{{% notice note %}}
Khi được yêu cầu nhập **account ID**, hãy sử dụng số 12 chữ số hiển thị ở góc trên bên phải của AWS Management Console.  
Lưu ý: hãy bỏ tất cả dấu gạch ngang.  
{{% /notice %}}
