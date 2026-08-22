---
title : "Tạo Subnet"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

1. Vào giao diện Console của AWS, tìm subnet -> chọn Subnet  
   ![Subnet](/images/05/image_010.png)  
2. Sau khi vào giao diện subnet thì chọn create subnet  
   ![Subnet](/images/05/image_011.png)  
   + Đầu tiên chúng ta sẽ chọn VPC mà chúng ta vừa tạo ở trên cho subnet này
   ![Subnet](/images/05/image_012.png)  
   + Tiếp theo chúng ta sẽ điền các trường tin cho phần subnet settings  
     + Subnet name: Public-subnet-a (chỉ để định danh cho subnet)  
     + AZ: chọn az Asia Pacific (Singapore) / apse1-az2 (ap-southeast-1a)  
     + IPv4 VPC CIDR block: 10.10.0.0/16 (là ip của VPC)  
     + IPv4 subnet CIDR block: chọn dải địa chỉ cho subnet a là 10.10.1.0/24
   ![Subnet](/images/05/image_013.png)  
3. Đây là giao diện sau khi chúng ta tạo thành công public subnet của VPC mini – company  


4. Tiếp tục làm như vậy để tạo ra private subnet của VPC này:  
   ![Subnet](/images/05/image_014.png)  
   + Đây sẽ là các thuộc tính cho private subnet  
     + Subnet name: private-subnet-a  
     + AZ: Asia Pacific (Singapore) / apse1-az2 (ap-southeast-1a)  
     + Ipv4 Subnet: 10.10.2.0/24  
   ![Subnet](/images/05/image_015.png)
5. Đây là 2 subnet mà chúng ta vừa tạo  
