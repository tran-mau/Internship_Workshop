---
title : "Tạo Private EC2"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---
### Các bước thực hiện  

1. Vào EC2 → Instances → Launch instance giống như đã làm với public EC2  
![Subnet](/images/05/image_052.png)  
2. Điền các trường thông tin cho Private EC2  
+ Name : mini-company-private-01  
![Subnet](/images/05/image_053.png)  
+ AMI: Ubuntu Server 24.04 LTS (64-bit ARM / x86)  
+ Instance type: t3.micro  
+ Ở phần key pair chúng ta sẽ dùng key pair đã tạo ở phần trước  
![Subnet](/images/05/image_054.png)  
+ Network settings: 
  + Vpc: mini-company-vpc  
  + Subnet: chọn private-subnet-a  
  + Auto-assign public IP: sẽ chọn Disable vì nó nằm trong private subnet, nên nó sẽ không có public ip mà chỉ có private ip  
![Subnet](/images/05/image_055.png)  
+ Phần security groups thì chúng ta cũng tạo 1 SG mới cho Private EC2 này  
![Subnet](/images/05/image_056.png)  
  + SG Name: private-ec2-sg  
  + Description: Security group for private ec2  
  + Inbound SG Rules: SSH/TCP/22 (Source type: Custom, Source: sg web)  
  -> Điều này có nghĩa là mình sẽ chỉ cho ssh từ SG từ public subnet vào private subnet chứ không để private subnet kết nối trực tiếp với internet
+ Về phần Configure storage thì chúng ta cũng chỉ cấp 8 GB gp3 -> Launch instance  
![Subnet](/images/05/image_057.png)  
+  Đây chính là private EC2 của chúng ta, nó sẽ không có public Ipv4 Adress, mà chỉ có Private Ipv4 address: 10.10.2.155  
![Subnet](/images/05/image_058.png) 
3. Chú ý: Bây giờ muốn vào ssh vào private ec2 của chúng ta thì chúng ta phải ssh vào public ec2 đã tạo trước đó. Nhưng key pair đang được lưu ở laptop của chúng ta chứ không phải ở public ec2 nên nó không thể vào private ec2 được, mặc dù không đáp ứng được yêu cầu bảo mật nếu ta đưa key pair lên public ec2 nhưng đối với bài lab này chúng ta sẽ sử dụng cách này để dễ dàng test hơn  


