---
title : "Amazon S3"
date : "`r Sys.Date()`"
weight : 8
chapter : false
pre : " <b> 5.8 </b> "
---

+ Trong chương này, chúng ta sẽ triển khai **Amazon S3** để lưu trữ và quản lý dữ liệu trên AWS. S3 cung cấp khả năng lưu trữ đối tượng với độ bền cao, có thể sử dụng để lưu trữ các tệp tin, dữ liệu ứng dụng, bản sao lưu và các tài nguyên cần thiết cho hệ thống.
+ **Amazon S3** được sử dụng làm dịch vụ lưu trữ dữ liệu và kết hợp với **IAM Role** để kiểm soát quyền truy cập từ EC2. Việc sử dụng IAM Role giúp EC2 có thể tương tác với S3 mà không cần lưu trữ Access Key và Secret Access Key trực tiếp trên máy chủ.
+ Thông qua S3, người quản trị có thể tạo **Bucket**, tải lên và quản lý các đối tượng, đồng thời kiểm tra quyền truy cập giữa EC2 và S3.

### Danh sách các bài học chi tiết:


+ [5.8.1 Tạo Amazon S3 Bucket]()
