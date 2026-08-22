---
title : "Tạo Internet Gateway"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---
### Các bước thực hiện

1. Trong console của VPC chọn tab internet gateways và chọn Create internet gateway  

![Subnet](/images/05/image_016.png)  

+ Ở đây chúng ta chỉ điền tên cho IGW rồi chọn create internet gateway  
  
![Subnet](/images/05/image_017.png)  

+ Đây là giao diện mà chúng ta sẽ nhìn thấy khi tạo xong IGW  
  
![Subnet](/images/05/image_018.png)  

+ Sau khi tạo thì trạng thái (State) của internet gateway đang là detach – điều này có nghĩa là IGW chưa được gán vào VPC mini-company của chúng ta nên chúng ta phải Attach Internet Gateway vào VPC:  
  + Chọn Actions và chọn Attach to VPC  
  ![Subnet](/images/05/image_020.png)  
  + Chọn vpc của mình rồi nhấn Attach internet gateway  
  ![Subnet](/images/05/image_021.png)  
  + State bây giờ đã là attached (IGW đã được gán cho mini-company VPC)  
  ![Subnet](/images/05/image_022.png)  


