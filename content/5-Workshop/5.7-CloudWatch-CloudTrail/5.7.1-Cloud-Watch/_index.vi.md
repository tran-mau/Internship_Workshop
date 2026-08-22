---
title : "Thiết lập Cloud Watch"  
date : "`r Sys.Date()`"  
weight : 1  
chapter : false  
pre : " <b> 5.7.1 </b> "  
--- 

Trong phần này, chúng ta sẽ sử dụng **Amazon CloudWatch** để theo dõi các chỉ số hoạt động của EC2 và thiết lập **CloudWatch Alarm** nhằm cảnh báo khi mức sử dụng CPU vượt quá ngưỡng cho phép.

### 1. Truy cập CloudWatch Metrics

Truy cập:

**AWS Console → CloudWatch → Metrics**

![Role](/images/05/image_101.png)

**CloudWatch Metrics** cung cấp các số liệu theo dõi hoạt động của các tài nguyên AWS. Đối với EC2, CloudWatch có thể thu thập các chỉ số như CPU, Network, Disk và các thông tin liên quan đến hoạt động của máy chủ.

Thông qua Metrics, người quản trị có thể theo dõi tình trạng hoạt động của EC2 và phát hiện những bất thường trong quá trình vận hành.

### 2. Kiểm tra các chỉ số của EC2

Chọn:

**EC2 → Per-Instance Metrics**

![Role](/images/05/image_102.png)

Tại **Per-Instance Metrics**, CloudWatch hiển thị các chỉ số được thu thập riêng cho từng EC2 Instance.

Trong bài này, chúng ta tập trung theo dõi chỉ số: **CPUUtilization**  

Đây là chỉ số thể hiện **phần trăm CPU đang được sử dụng trên EC2**.

### 3. Theo dõi CPUUtilization

Từ Per-Instance Metrics, chúng ta có thể lựa chọn EC2 cần theo dõi và xem biểu đồ **CPUUtilization** theo thời gian.

![Role](/images/05/image_102.png)

Thông qua biểu đồ này, người quản trị có thể quan sát mức sử dụng CPU của EC2 và xác định những thời điểm máy chủ có mức tải cao.

Ví dụ, nếu CPU thường xuyên duy trì ở mức cao, điều này có thể cho thấy EC2 đang phải xử lý nhiều tác vụ hoặc tài nguyên hiện tại không đáp ứng đủ nhu cầu sử dụng.

### 4. Tạo CloudWatch Alarm

Để hệ thống tự động cảnh báo khi CPU của EC2 vượt quá mức cho phép, chúng ta tạo một **CloudWatch Alarm**.

Truy cập:

**CloudWatch → Alarms → Create Alarm**

![Role](/images/05/image_103.png)

CloudWatch Alarm cho phép thiết lập một điều kiện dựa trên Metric. Khi Metric đạt đến điều kiện đã cấu hình, Alarm sẽ chuyển sang trạng thái cảnh báo và có thể gửi thông báo đến người quản trị.

### 5. Lựa chọn Metric cần giám sát

Chọn:

**Select metric → EC2 → Per-Instance Metrics → CPUUtilization**

![Role](/images/05/image_104.png)

Sau đó lựa chọn đúng **EC2 Instance** cần theo dõi.

Việc lựa chọn CPUUtilization giúp CloudWatch giám sát mức sử dụng CPU của EC2 và sử dụng giá trị này làm cơ sở để kích hoạt cảnh báo.

### 6. Cấu hình điều kiện cảnh báo

Chúng ta cấu hình điều kiện:

+ **Statistic:** Average
+ **Period:** 5 minutes
+ **Condition:** Greater than 80%

![Role](/images/05/image_105.png)

Các thông số trên có ý nghĩa:

+ **Average:** CloudWatch sử dụng giá trị CPU trung bình trong khoảng thời gian được chọn.
+ **Period 5 minutes:** Dữ liệu CPU được đánh giá theo từng khoảng thời gian 5 phút.
+ **Greater than 80%:** Alarm sẽ được kích hoạt khi giá trị CPU trung bình vượt quá 80% theo điều kiện đã thiết lập.

Có thể hiểu đơn giản:

**CPUUtilization > 80% → CloudWatch Alarm**

Việc đặt ngưỡng 80% giúp phát hiện tình trạng EC2 có mức sử dụng CPU cao và cho phép người quản trị kịp thời kiểm tra nguyên nhân.

### 7. Cấu hình thông báo qua Email

Tiếp theo, chúng ta cấu hình phương thức nhận thông báo khi Alarm được kích hoạt.

Chọn gửi thông báo đến **Email** và nhập địa chỉ email cần nhận cảnh báo.

![Role](/images/05/image_106.png)

Khi Alarm chuyển sang trạng thái **In alarm**, CloudWatch sẽ gửi thông báo đến địa chỉ email đã cấu hình thông qua **Amazon SNS**.

### 8. Đặt tên và tạo Alarm

Đặt tên và mô tả cho Alarm để thuận tiện cho việc quản lý.

![Role](/images/05/image_107.png)

Sau khi hoàn tất cấu hình, chọn **Create alarm** để tạo CloudWatch Alarm.

Sau khi được tạo, Alarm sẽ bắt đầu theo dõi Metric **CPUUtilization** của EC2 theo các điều kiện đã thiết lập.

### 9. Kết quả

Sau khi hoàn thành cấu hình, hệ thống có mô hình giám sát:

**EC2 → CloudWatch Metrics → CPUUtilization → CloudWatch Alarm → Email**

Khi CPU của EC2 hoạt động bình thường, Alarm duy trì trạng thái **OK**.

Khi CPU trung bình vượt quá ngưỡng **80%** theo điều kiện đã cấu hình, Alarm sẽ chuyển sang trạng thái **In alarm** và gửi thông báo đến email của người quản trị.

Việc kết hợp **CloudWatch Metrics** và **CloudWatch Alarm** giúp hệ thống chủ động phát hiện tình trạng tài nguyên bất thường, hỗ trợ người quản trị giám sát EC2 và xử lý sự cố kịp thời.