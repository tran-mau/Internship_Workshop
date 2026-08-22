---
title : "Cấu hình Route Table cho Private Subnet"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.4.3 </b> "
---

### Các bước thực hiện

Sau khi tạo **NAT Gateway**, cần cấu hình **Route Table** của Private Subnet để định tuyến lưu lượng Internet đi qua NAT Gateway.

### 1. Liên kết Route Table với Private Subnet

Truy cập:

**VPC → Subnets → Private subnet a → Route table → Edit route table association**

![RTB](/images/05/image_087.png)

Tại đây, kiểm tra Route Table đang được liên kết với **Private Subnet**.

Route Table này sẽ quyết định cách các gói tin từ Private EC2 được định tuyến đến các tài nguyên khác trong VPC hoặc ra Internet.

### 2. Thêm Route đến NAT Gateway

Trong Route Table của Private Subnet, chọn **Edit routes** và thêm một route:

+ **Destination:** `0.0.0.0/0`
+ **Target:** NAT Gateway đã tạo (`mini company nat gateway`)

![RTB](/images/05/image_088.png)

Route `0.0.0.0/0` đại diện cho tất cả lưu lượng IPv4 không thuộc các mạng cụ thể trong Route Table.

Khi cấu hình Target là **NAT Gateway**, các yêu cầu từ Private EC2 đi ra Internet sẽ được định tuyến theo đường:

**Private EC2 → Private Subnet → Route Table → NAT Gateway → Internet Gateway → Internet**

NAT Gateway sẽ thay mặt cho Private EC2 thực hiện kết nối ra Internet. Nhờ đó, Private EC2 không cần Public IP nhưng vẫn có thể truy cập Internet.


### 3. Kiểm tra kết nối Internet từ Private EC2

Sau khi hoàn tất cấu hình NAT Gateway và Route Table, chúng ta tiến hành kiểm tra khả năng kết nối Internet của Private EC2.

![RTB](/images/05/image_089.png)
