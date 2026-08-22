---
title : "Tạo Amazon S3"   
date : "`r Sys.Date()`"   
weight : 1   
chapter : false   
pre : " <b> 5.8.1 </b> "   
---

### Các bước thực hiện:  

1. Vào AWS Console → S3 → Create bucket  
![Role](/images/05/image_113.png)  
2. Chọn các trường thông tin cho S3:  
+ AWS Region: Asia Pacific (Singapore) ap-southeast-1  
+ Bucket type: General purpose  
+ Bucket namespace: Global namespace  
+ Bucket name: mini-company-storage-1  
![Role](/images/05/image_114.png)  
+ Object Ownership: ACLs disabled (recommended)
![Role](/images/05/image_115.png)  
+ Encryption type: Server-side encryption with Amazon S3 managed keys (SSE-S3)  
+ Bucket Key: Disable  
![Role](/images/05/image_116.png)  
3. Create bucket  
![Role](/images/05/image_117.png)  
4. Upload một file thử nghiệm  
+ Chọn: Upload → Add files  
![Role](/images/05/image_118.png)  
+ Để Private EC2 có thể truy cập S3 mà không cần Access Key hay Secret Key thì chúng ta sẽ dùng IAM Role mà chúng ta tạo trước đó.  
+ Thêm quyền S3 cho EC2 Role  
  + Vào: IAM → Policies → Create policy  
  ![Role](/images/05/image_119.png)  
  + Chọn: JSON -> Nhập policy
  ![Role](/images/05/image_120.png)  
  -> Policy này cho phép EC2: List bucket; Download object; Upload object và không được Delete object  
  + Đặt tên và mô tả cho Policy  
  ![Role](/images/05/image_122.png)  
+ Attach Policy vào Role  
  + IAM → Roles → MiniProject-EC2-Role  
  ![Role](/images/05/image_123.png) 
  + Chọn Add permissions → Attach policies  
  ![Role](/images/05/image_124.png)  
  + Chọn MiniProject-S3-Access  
  ![Role](/images/05/image_125.png)  
  + Đây là những Policy đã tạo  
5. Kiểm tra S3 từ Private EC2  
+ Mở SSM Session vào Private EC2.  
+ Cài aws cli cho private EC2  
+ Kiểm tra IAM Role  
![Role](/images/05/image_126.png)  
+ Private EC2 đang sử dụng IAM Role, chứ không dùng Access Key cá nhân.  
+ Test S3 dùng lệnh aws s3 ls s3://mini-company-storage-1    
![Role](/images/05/image_127.png)  
(lệnh này dùng để liệt kê danh sách các tệp (files) và thư mục con bên trong S3)  
+ Test Upload  
![Role](/images/05/image_128.png)  
  + $ echo "Hello from Private EC2" > test.txt  
  + $ aws s3 cp test.txt s3://mini-company-storage-1  
  -> 2 lệnh dùng để tạo ra 1 file văn bản và tải file đó lên S3
  + Sau đó chạy lệnh aws s3 ls s3://mini-company-storage-1  và đã thấy file text đã được upload thành công lên s3
  + Thử xóa file test vừa tạo với lệnh: aws s3 rm s3://mini-company-storage-1/test.txt  
  ![Role](/images/05/image_129.png)  
  -> kết quả failed đúng với policy đã thiết lập



