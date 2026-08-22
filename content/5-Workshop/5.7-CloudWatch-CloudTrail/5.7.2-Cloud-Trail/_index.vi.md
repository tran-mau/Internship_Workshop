---
title : "Thiết lập Cloud Trail"   
date : "`r Sys.Date()`"   
weight : 2   
chapter : false   
pre : " <b> 5.7.2 </b> "   
---

Trong phần này, chúng ta sẽ sử dụng **AWS CloudTrail** để ghi nhận và theo dõi các hoạt động xảy ra trong tài khoản AWS. CloudTrail giúp người quản trị biết được **ai đã thực hiện thao tác gì, thực hiện trên tài nguyên nào và vào thời điểm nào**.

### 1. Truy cập CloudTrail Event history

Truy cập:

**AWS Console → CloudTrail → Event history**

![Role](/images/05/image_112.png)

**Event history** là nơi hiển thị lịch sử các hoạt động API đã xảy ra trong tài khoản AWS.

Tại đây, chúng ta có thể xem các thông tin liên quan đến từng sự kiện như:

+ **Event name:** Tên thao tác được thực hiện.
+ **Event time:** Thời gian thao tác xảy ra.
+ **Username:** Người hoặc thành phần thực hiện thao tác.
+ **Event source:** Dịch vụ AWS mà thao tác được thực hiện trên đó.
+ **Resource:** Tài nguyên liên quan đến sự kiện.
+ **Source IP address:** Địa chỉ IP thực hiện yêu cầu.

### 2. Kiểm tra lịch sử hoạt động

CloudTrail tự động ghi nhận các hoạt động quản trị và các yêu cầu API được thực hiện thông qua AWS Console, AWS CLI hoặc các dịch vụ AWS.

Ví dụ, khi người quản trị thực hiện các thao tác như tạo, sửa hoặc xóa tài nguyên EC2, VPC, Security Group hoặc IAM, các hoạt động tương ứng có thể được tìm kiếm trong **Event history**.

Người quản trị có thể sử dụng bộ lọc để tìm kiếm một sự kiện cụ thể dựa trên **Event name, User name, Resource type, Resource name** hoặc khoảng thời gian.

### 3. Kết quả

Thông qua **AWS CloudTrail**, các hoạt động quản trị trong hệ thống được ghi nhận và có thể tra cứu lại khi cần.

CloudTrail giúp tăng khả năng **kiểm tra, truy vết và xác định nguyên nhân sự cố**, từ đó hỗ trợ người quản trị giám sát và bảo mật hệ thống AWS hiệu quả hơn.