---
title : "Tại sao cần dùng Nat Gateway"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
--- 

## NAT Gateway là gì?

**NAT Gateway (Network Address Translation Gateway)** là một dịch vụ của AWS cho phép các tài nguyên nằm trong **Private Subnet** có thể truy cập Internet bên ngoài, nhưng Internet không thể chủ động khởi tạo kết nối trực tiếp đến các tài nguyên này.

Trong mô hình mạng của chúng ta, Private EC2 không được gán Public IP. Vì vậy, nếu muốn Private EC2 truy cập Internet để cập nhật hệ thống, cài đặt phần mềm hoặc tải các gói cần thiết, chúng ta cần sử dụng NAT Gateway.

## Tại sao cần sử dụng NAT Gateway?

1. Cho phép Private EC2 truy cập Internet  
+ Private EC2 có thể truy cập Internet để:  
  + Cập nhật hệ điều hành.  
  + Cài đặt các package cần thiết.  
  + Tải phần mềm và thư viện.  
  + Kết nối đến các dịch vụ bên ngoài.  
2. Không cần cấp Public IP cho Private EC2  
+ Private EC2 vẫn có thể truy cập Internet mà không cần gán Public IPv4.  
+ Điều này giúp hạn chế việc đưa Application Server trực tiếp ra Internet.  
3. Tăng tính bảo mật  
+ Private EC2 chỉ có thể chủ động gửi kết nối ra ngoài thông qua NAT Gateway.  
+ Internet bên ngoài không thể sử dụng NAT Gateway để chủ động kết nối trực tiếp vào Private EC2.  

