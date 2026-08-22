---
title : "Tổng quan về AWS Systems Manager và SSM Agent"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.6.1 </b> "
---

## 1. AWS Systems Manager là gì?

**AWS Systems Manager (SSM)** là dịch vụ của AWS giúp quản lý và vận hành các máy chủ EC2 từ xa. SSM cho phép người quản trị thực hiện các tác vụ quản trị mà không cần kết nối trực tiếp đến máy chủ thông qua SSH.

Trong bài này, AWS Systems Manager được sử dụng để quản trị các EC2, đặc biệt là **EC2 nằm trong Private Subnet**, thông qua **Session Manager**.

## 2. SSM Agent là gì?

**SSM Agent** là phần mềm được cài đặt và chạy trên EC2, giúp máy chủ giao tiếp với AWS Systems Manager. Agent chịu trách nhiệm nhận và thực hiện các yêu cầu quản trị được gửi từ Systems Manager.

Mô hình hoạt động:

**AWS Systems Manager → SSM Agent → EC2**

Khi SSM Agent hoạt động và EC2 được cấp **IAM Role** phù hợp, máy chủ có thể kết nối với Systems Manager và nhận các lệnh từ người quản trị.

## 3. Vai trò trong mini project

Trong mini project, AWS Systems Manager và SSM Agent được sử dụng kết hợp với **IAM Role** để quản trị EC2.

Các thành phần hoạt động như sau:

+ **IAM Role:** Cung cấp quyền cho EC2 giao tiếp với Systems Manager.
+ **SSM Agent:** Chạy trên EC2 và tiếp nhận các yêu cầu từ Systems Manager.
+ **AWS Systems Manager:** Cung cấp công cụ để quản trị và thực hiện lệnh trên EC2.
+ **Session Manager:** Cho phép người quản trị truy cập EC2 mà không cần mở cổng SSH.

Việc sử dụng SSM giúp tăng tính bảo mật và thuận tiện trong quá trình quản trị máy chủ, đặc biệt đối với các EC2 không có **Public IP**.