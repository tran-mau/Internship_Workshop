---
title : "Thiết lập AWS Systems Manager (SSM)" 
date : "`r Sys.Date()`" 
weight : 2 
chapter : false 
pre : " <b> 5.6.2 </b> " 
---

Trong phần này, chúng ta sẽ sử dụng **AWS Systems Manager (SSM)** để kết nối và quản lý **Private EC2** mà không cần thực hiện SSH thông qua Public EC2.

### 1. Kiểm tra Private EC2 trên Systems Manager

Truy cập:

**AWS Systems Manager → Fleet Manager → Managed nodes**

![Role](/images/05/image_097.png)

Tại đây, chúng ta có thể kiểm tra danh sách các máy chủ đang được AWS Systems Manager quản lý.

**Private EC2** xuất hiện trong danh sách **Managed nodes** với trạng thái hoạt động, điều đó cho thấy EC2 đã kết nối thành công với Systems Manager.

Để EC2 xuất hiện trong danh sách này, máy chủ cần có **SSM Agent đang hoạt động** và được gán **IAM Role phù hợp** để giao tiếp với Systems Manager.

### 2. Truy cập Session Manager

Tiếp theo, truy cập:

**AWS Systems Manager → Session Manager → Sessions**

![SMM](/images/05/image_098.png)

**Session Manager** là chức năng cho phép người quản trị thiết lập một phiên làm việc trực tiếp với EC2 thông qua trình duyệt AWS.

Ưu điểm của phương pháp này là không cần sử dụng SSH và không cần cung cấp SSH Private Key để truy cập máy chủ.

### 3. Tạo phiên kết nối với Private EC2

Chọn **Start session**.

Sau đó chọn **Private EC2** cần quản lý và nhấn **Start session**.

![SMM](/images/05/image_099.png)

AWS Systems Manager sẽ sử dụng **SSM Agent** trên EC2 để thiết lập kết nối. Sau khi kết nối thành công, hệ thống sẽ mở một phiên terminal trực tiếp trên trình duyệt.

### 4. Quản lý Private EC2 thông qua terminal

Sau khi phiên làm việc được khởi tạo, chúng ta sẽ thấy giao diện terminal được AWS cung cấp ngay trên trình duyệt.

![SMM](/images/05/image_100.png)

Tại đây, có thể thực hiện các lệnh quản trị trên Private EC2 tương tự như khi sử dụng SSH