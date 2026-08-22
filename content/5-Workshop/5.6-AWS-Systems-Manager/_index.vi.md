---
title : "AWS Systems Manager" 
date : "`r Sys.Date()`" 
weight : 6
chapter : false 
pre : " <b> 5.6 </b> " 
---

+ Trong chương này, chúng ta sẽ triển khai **AWS Systems Manager (SSM)** để quản lý và giám sát các máy chủ EC2 trong hệ thống mà không cần phải kết nối trực tiếp thông qua SSH. AWS Systems Manager cung cấp các công cụ hỗ trợ quản trị máy chủ, thực hiện lệnh từ xa và kiểm tra trạng thái của các EC2 instance.
+ Trong mini project, **AWS Systems Manager** được sử dụng kết hợp với **IAM Role**. EC2 được gán IAM Role phù hợp để có thể kết nối với Systems Manager. Thông qua SSM, người quản trị có thể truy cập và thực hiện các lệnh trên EC2 một cách an toàn mà không cần mở cổng SSH cho toàn bộ Internet.
+ Việc sử dụng AWS Systems Manager giúp giảm sự phụ thuộc vào SSH, hạn chế việc phải quản lý SSH Key và tăng mức độ bảo mật khi quản trị các máy chủ nằm trong **Private Subnet**.

### Danh sách các bài học chi tiết:

+ [5.6.1 Tổng quan về AWS Systems Manager]({{< relref "5.6.1-Overview-Systems-Manager">}})
+ [5.6.2 Thiết lập AWS Systems Manager (SSM)]({{< relref "5.6.2-Setup-Systems-Manager">}})


### Mục tiêu của chương

Sau khi hoàn thành chương này, người thực hiện có thể:

+ Hiểu được chức năng và vai trò của **AWS Systems Manager** trong quản trị máy chủ.
+ Hiểu mối quan hệ giữa **EC2, IAM Role và SSM Agent**.
+ Cấu hình IAM Role để EC2 có thể sử dụng AWS Systems Manager.
+ Kiểm tra trạng thái hoạt động của **SSM Agent** trên EC2.
+ Kết nối đến EC2 bằng **Session Manager** mà không cần sử dụng SSH.
+ Thực hiện các câu lệnh quản trị trên EC2 thông qua Systems Manager.
+ Quản lý và kiểm tra các EC2 nằm trong **Private Subnet**.
+ Kiểm tra và xử lý các lỗi khiến EC2 không xuất hiện trong Systems Manager.

### AWS Systems Manager trong mini project

Trong kiến trúc của mini project, AWS Systems Manager đóng vai trò là công cụ hỗ trợ quản trị các EC2 instance.

Mô hình hoạt động có thể được mô tả như sau:

**EC2 → IAM Role → SSM Agent → AWS Systems Manager**

Trong đó:

+ **EC2** là máy chủ cần được quản trị.
+ **IAM Role** cung cấp quyền cần thiết để EC2 giao tiếp với các dịch vụ AWS.
+ **SSM Agent** được cài đặt và chạy trên EC2 để nhận các yêu cầu quản trị từ Systems Manager.
+ **AWS Systems Manager** cung cấp giao diện và các công cụ để người quản trị kết nối, thực hiện lệnh và quản lý EC2.

Đối với **Private EC2**, việc sử dụng Systems Manager đặc biệt hữu ích vì máy chủ không cần Public IP và không nhất thiết phải mở cổng SSH từ Internet. Khi EC2 có thể giao tiếp với các endpoint cần thiết của AWS Systems Manager, người quản trị có thể sử dụng **Session Manager** để truy cập máy chủ.

### Vai trò của Systems Manager trong bảo mật hệ thống

Việc sử dụng AWS Systems Manager giúp tăng cường bảo mật cho kiến trúc hệ thống thông qua việc:

+ Hạn chế việc mở cổng **TCP/22 (SSH)** trên Security Group.
+ Không cần sử dụng Public IP để quản trị EC2.
+ Không cần lưu trữ SSH Private Key trên máy tính quản trị để sử dụng Session Manager.
+ Có thể kiểm soát quyền truy cập thông qua **IAM**.
+ Có thể quản lý cả các EC2 nằm trong Private Subnet.
+ Hỗ trợ tập trung trong việc quản trị và vận hành các máy chủ trên AWS.

Trong mini project, Systems Manager được sử dụng kết hợp với **IAM Role, VPC, Private Subnet và EC2** để xây dựng mô hình quản trị máy chủ an toàn hơn.