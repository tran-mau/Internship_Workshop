---
title : "Chuẩn bị Automation Server"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

### Các bước thực hiện

Sau khi hoàn thành việc triển khai EC2, chúng ta tiến hành chuẩn bị **Automation Server** để sử dụng làm máy chủ điều khiển cho hệ thống automation.

## 1. SSH vào Automation Server

Từ máy Windows, sử dụng SSH để kết nối tới EC2 `Automation-Server`.

Private key của EC2 được sử dụng để xác thực khi kết nối.

![ATSV](/images/01/image_062.png)

## 2. Kiểm tra hệ điều hành

Sau khi đăng nhập, kiểm tra thông tin hệ điều hành:

```bash
cat /etc/os-release
```

Automation Server sử dụng **Ubuntu Server 24.04 LTS**.

![ATSV](/images/01/image_063.png)


## 3. Đổi hostname

Kiểm tra hostname hiện tại:

```bash
hostname
```

Sau đó đổi hostname để dễ nhận biết:

```bash
sudo hostnamectl set-hostname automation-server
```

Hostname mới:

```text
automation-server
```

![ATSV](/images/01/image_064.png)


## 4. Kiểm tra kết nối Internet

Automation Server nằm trong **Public Subnet**, vì vậy cần kiểm tra khả năng kết nối Internet.

Kiểm tra kết nối IP:

```bash
ping -c 4 8.8.8.8
```

Kiểm tra DNS:

```bash
ping -c 4 google.com
```

Nếu các lệnh trên hoạt động bình thường, Automation Server đã có kết nối Internet thông qua cấu hình mạng AWS đã triển khai.

![ATSV](/images/01/image_065.png)


## 5. Cập nhật package

Cập nhật danh sách package:

```bash
sudo apt update
```

Sau đó nâng cấp các package hiện có:

```bash
sudo apt upgrade -y
```

![ATSV](/images/01/image_067.png)


## Kết quả

Sau khi hoàn thành, Automation Server đã được chuẩn bị với:

```text
Automation-Server
│
├── Ubuntu Server 24.04 LTS
├── Hostname: automation-server
├── Public Subnet
└── Internet connectivity
```

Automation Server đã sẵn sàng để cài đặt **Python và Ansible** trong các bước tiếp theo.
