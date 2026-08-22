---
title : "Tạo IAM Role cho EC2"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---  
### Các bước thực hiện  
1. Vào IAM -> role -> creat role  
![IAM](/images/05/image_090.png)  
![IAM](/images/05/image_091.png)  
2. Select trusted entity:  
+ entity type: chọn AWS Service  
+ Service or use case: EC2  
+ Add permissions: Chọn use existing policy  
-> tìm Policy: AmazonSSMManagedInstanceCore và tích chọn -> next  
![IAM](/images/05/image_092.png)  
+ Tiếp theo sẽ đặt tên Role:  
  + Role name: MiniProject-EC2-Role  
  + Description: Allows EC2 instances to call AWS services on your behalf  
  + Chọn Create Role  
![IAM](/images/05/image_093.png)  
