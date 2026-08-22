---
title : "SSH tới Private EC2"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---
# SSH tới Private EC2 thông qua Public EC2  

### Các bước thực hiện  

1. Mở powerShell nhấn ssh -V  
2. 2.Bật SSH Agent của Windows  
![SSH](/images/05/image_071.png)  
3. Di chuyển tới thư mục chứa key và add file private key pem vào ssh của laptop  
![SSH](/images/05/image_072.png)  
4. SSH vào Public EC2  
![SSH](/images/05/image_073.png)  
5. SSH sang Private EC2 bằng câu lệnh ssh ubuntu@ 10.10.2.155  
![SSH](/images/05/image_074.png)  
![SSH](/images/05/image_075.png)  
6. Nhập các lệnh kiểm tra private EC2: Hostname; Ip addr; Ip route  
![SSH](/images/05/image_077.png)  
7. Kiểm tra kết nối của private EC2 khi chưa có Nat gateway bằng lệnh: curl -I https://www.google .com  
![SSH](/images/05/image_078.png)  
=> Vì chưa có Nat Gateway nên private EC2 chưa thể vào được internet nên ở bài sau chúng ta sẽ tiếp tục với việc tạo Nat Gateway  




