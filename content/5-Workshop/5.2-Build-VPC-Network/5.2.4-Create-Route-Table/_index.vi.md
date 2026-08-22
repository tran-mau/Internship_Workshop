---
title : "Tạo Route Table"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---
### Các bước thực hiện  
1. Vào tab router table chọn Create route table  
![Subnet](/images/05/image_023.png)  
2. Đặt tên cho route table và chọn mini-company VPC của mình sau đó create route table  
![Subnet](/images/05/image_024.png)  
3. Đây sẽ là giao diện khi chúng ta tạo xong public route table  
![Subnet](/images/05/image_025.png)  
4. Tiếp theo chúng ta sẽ tạo thêm route internet  
![Subnet](/images/05/image_026.png)  
5. Chọn Edit routes, chọn Add route  
![Subnet](/images/05/image_027.png)  
6. Chọn dải Destination là 0.0.0.0/0 và target là Internet Gateway, điều này có nghĩa là gói tin tới bất kỳ mạng nào khác → gửi tới Internet Gateway. Sau đó chọn save changes
![Subnet](/images/05/image_028.png)  
7. Tiếp theo chúng ta sẽ Associate route table với public subnet  
![Subnet](/images/05/image_029.png)  
8. Trong public-route-table chúng ta chọn subnet associations sau đó chọn Edit subnet associations  
![Subnet](/images/05/image_030.png)  
9. Ở đây chúng ta sẽ chọn public-subnet-a (cái mà sẽ kết nối đến với IGW để đi ra ngoài internet) sau đó chọn save associations  
![Subnet](/images/05/image_031.png)  
10. Đây là kết quả sau khi chúng ta đã Associate route table với public subnet  
![Subnet](/images/05/image_032.png)  
![Subnet](/images/05/image_033.png) 

