---
title : "Tạo VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

1. Vào giao diện Console của AWS, trên thanh tìm kiếm gõ VPC, chọn biểu tượng VPC   
![VPC](/images/05/image_003.png)  
  
![VPC](/images/05/image_004.png)  
2. Sau khi truy cập vào VPC, Chúng ta chọn Create VPC  
   ![VPC](/images/05/image_005.png)  
   
3. Sau khi chọn Create VPC chúng ta sẽ có giao diện để nhập các trường thông tin VPC của chúng ta:  
   + Ở mục Resources to create: chọn VPC only vì ở đây mình muốn tự thiết lập các thành phần khác trong mạng  
   + Ở mục Name tag – optional: đặt tên là mini-company-vpc ( đây chỉ là tên định danh cho VPC )  
   + IPv4 CIDR block có 2 lựa chọn là IPv4 CIDR manual input  và IPAM-allocated IPv4 CIDR block  
     + IPv4 CIDR manual input có nghĩa là mình tự tay nhập một dải IP cố định theo chuẩn CIDR (ví dụ: 10.0.0.0/16 hoặc 172.16.0.0/16)  
     + IPAM-allocated IPv4 CIDR block nghĩa là mình chọn một dải IP được quản lý và cấp phát tự động từ AWS VPC IPAM
     -> Nên ở đây chọn IPv4 CIDR manual input  
   + Ở mục IPv4 CIDR chúng ta sẽ viết dải địa chỉ cho VPC: 10.10.0.0/16
   + IPv6 CIDR block chọn No IPv6 CIDR block vì chúng ta không dùng Ipv6 trong bài này  
   + Tenancy:  
     + default có nghĩa là Server vật lý sẽ được chia sẻ với nhiều khách hàng.  
     + Dedicated thì AWS dành riêng Server vật lý cho bạn và chi phí sẽ rất cao  
        -> Nên ở đây mình chỉ dùng default thôi
   + Sau đó chọn Creat VPC  
  
  ![VPC](/images/05/image_008.png)   
  ![VPC](/images/05/image_009.png)  

Đây là giao diện chúng ta sẽ thấy sau khi tạo thành công VPC  

