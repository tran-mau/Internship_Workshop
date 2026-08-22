---
title : "Tạo Public EC2"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---
### Các bước thực hiện  

1. Trong AWS Console chúng ta chọn EC2 sau đó chọn Instances → Launch instance  
![Subnet](/images/05/image_034.png)  
![Subnet](/images/05/image_035.png)  

2. Tiếp đến chúng ta sẽ đặt tên cho instance là mini-company-web-01  
![Subnet](/images/05/image_036.png)  
3. Tiếp theo:  
  + AMI: Ubuntu Server 24.04 LTS (64-bit ARM / x86)  
  + Instance type: t3.micro  
![Subnet](/images/05/image_037.png)  
4. Ở phần key pair chúng ta sẽ tạo 1 key mới:  
  
  + Key pair name: mini-company-key  
  + Key pair type: RSA  
  + Private key file format: Để định dạng .pem  
  + Sau đó chọn save key về máy tính  
![Subnet](/images/05/image_038.png)  
5. Tiếp đến sẽ là phần Network settings  
![Subnet](/images/05/image_039.png)  
  + VPC: Chọn VPC mà chúng ta đã tạo ở bài trước (mini-company-vpc)  
  + Subnet: chọn public-subnet-a  
  + Auto-assign public IP: Chọn Enable  
  + Firewall (security groups) thì chúng ta sẽ phải tạo vì chúng ta chưa tạo security group trước đây  
  ![Subnet](/images/05/image_040.png)  
  + Ở đây sẽ có các trường thông tin như: 
    + Security group name: web-sg  
    + Description: Security Group for web server
    + Inbound Security Group Rules: Tạo 3 Inbound security là: 
      + SSH/TCP/22 từ My Ip
      + Inbound security thứ 2 là ALL ICMP-IPv4/ICMP/all từ Anywhere (0.0.0.0/0)  
      + Inbound security thứ 3 là HTTP/TCP/80 cũng từ Anywhete (0.0.0.0/0)  
    
    ![Subnet](/images/05/image_041.png)  
  + Về phần Configure storage chỉ cấp 8 GB gp3  
  ![Subnet](/images/05/image_042.png)  
  + Sau đó chọn Launch instance  
  ![Subnet](/images/05/image_043.png)  
  + Đây chính là EC2 chúng ta vừa tạo  
6. Bây giờ chúng ta sẽ kiểm tra kiến trúc mạng có thực sự hoạt động đúng hay không  
  + ![Subnet](/images/05/image_044.png)  
  + ![Subnet](/images/05/image_045.png)  
  + ![Subnet](/images/05/image_046.png)  
  + Kiểm tra IP:  
  ![Subnet](/images/05/image_047.png)  
  + Kiểm tra Route Table:  
  ![Subnet](/images/05/image_048.png)  
  + Kiểm tra kết nối Internet:  
  ![Subnet](/images/05/image_050.png)
7. Cách test ssh public ec2 thứ 2: dùng MobaXterm  
  ![Subnet](/images/05/image_060.png)  
  + Ở đây chúng ta sẽ nhập thông tin để ssh đến ec2 public  
  + Remote host: 54.169.82.121 đây là địa chỉ ip public của ec2 public  
  + Username: ubuntu tên mặc định của Ubuntu Server 24.04 LTS  
  + Tích chọn Use private key và dùng key .pem mà chúng ta đã tạo  
  + Chọn ok để kết nối tới ec2  
  ![Subnet](/images/05/image_061.png)  
  + Đây là kết quả sau khi kết nối thành công  
  ![Subnet](/images/05/image_062.png)  