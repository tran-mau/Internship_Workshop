---
title : "Tạo Nat Gateway"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---  
### Các bước thực hiện  
1. Đầu tiên chúng ta phải tạo Elastic IP vì NAT Gateway yêu cầu bắt buộc phải có một địa chỉ IP công cộng tĩnh ngay tại thời điểm khởi tạo, và hệ thống AWS không tự động cấp phát Public IP ngẫu nhiên cho NAT Gateway như đối với máy chủ EC2.  
+ Vào VPC -> Elastic IPs -> Allocate Elastic IP address  
![NATGW](/images/05/image_079.png)  

2. Chọn Amazon's pool of IPv4 addresses trong trường Public IPv4 address pool -> chọn allocate  
![NATGW](/images/05/image_080.png)  
3. Đây là Elastic IP mà chúng ta đã tạo  
![NATGW](/images/05/image_081.png)  
4. Tiếp theo chúng ta sẽ tạo Nat Gateway  
+ Trong AWS Console: Chọn VPC → NAT Gateways → Create NAT gateway  
![NATGW](/images/05/image_082.png)  
5. Cấu hình NAT Gateway:  
+ Name: mini-company-nat-gateway  
+ Subnet: Chọn Public subnet 2  
+ Availability mode: chọn Zonal rồi chọn public subnet a  
+ Connectivity type : chọn Public  
+ Elastic IP allocation ID: Chọn Elastic IP vừa tạo  
![NATGW](/images/05/image_084.png)  
![NATGW](/images/05/image_085.png)  
6. Đây là giao diện sau khi tạo xong nat-gateway  
![NATGW](/images/05/image_086.png)  




