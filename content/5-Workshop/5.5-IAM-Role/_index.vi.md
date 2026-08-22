---
title : "IAM Role"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---
+ Trong chương này, chúng ta sẽ triển khai IAM Role và gán Role cho các máy chủ EC2 trong hệ thống. IAM Role cho phép EC2 sử dụng các dịch vụ AWS thông qua quyền được cấp mà không cần lưu trữ Access Key và Secret Access Key trực tiếp trên máy chủ.  
+ IAM Role được sử dụng để cấp quyền cho EC2 thực hiện các tác vụ cần thiết như truy cập Amazon S3, sử dụng AWS Systems Manager (SSM) và gửi dữ liệu giám sát lên Amazon CloudWatch. Việc sử dụng IAM Role giúp tăng tính bảo mật và thuận tiện trong quá trình quản trị hệ thống.  


### Danh sách các bài học chi tiết:  
+ [5.5.1 Tạo IAM Role cho EC2]({{< relref "5.5.1-Create-IAM-Role">}})  
+ [5.5.2 Gán IAM Role cho EC2]({{< relref "5.5.2-Attach-Role-EC2">}})  
 