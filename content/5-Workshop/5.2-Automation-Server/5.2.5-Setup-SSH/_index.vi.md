---
title : "Thiết lập SSH kết nối tới Managed Nodes"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.2.5 </b> "
---

### Các bước thực hiện

Sau khi hoàn thành hạ tầng AWS, Automation Server cần có khả năng kết nối SSH tới `Managed-Node-01` và `Managed-Node-02`.

Trong project, SSH được sử dụng làm phương thức kết nối giữa **Automation Server** và **Managed Nodes** để Ansible có thể quản lý các máy chủ này. 

## 1. Kiểm tra kết nối mạng

Trước khi xử lý SSH authentication, cần kiểm tra khả năng kết nối tới các Managed Nodes và port SSH.

Managed Nodes nằm trong Private Subnet và Security Group `Managed-Node-SG` cho phép TCP port 22 từ `Automation-SG`. 

![ATSV](/images/01/image_086.png)

## 2. Tạo SSH key cho Automation Server

Trên **Automation Server**, tạo một SSH key riêng:

```bash
ssh-keygen -t ed25519 -C "automation-ansible"
```

Lệnh trên tạo một cặp SSH key sử dụng thuật toán **Ed25519**.

Sau khi tạo, Automation Server sẽ có:

```text
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

Trong đó:

- `id_ed25519` là **private key**.
- `id_ed25519.pub` là **public key**.

Private key được giữ trên Automation Server và không đưa vào Managed Nodes. fileciteturn17file7

![ATSV](/images/01/image_081.png)

## 3. Đưa Public Key vào Managed Nodes

Mục tiêu là đưa:

```text
~/.ssh/id_ed25519.pub
```

vào file:

```text
~/.ssh/authorized_keys
```

trên Managed Nodes.

Cơ chế xác thực:

```text
Automation Server
       |
       | Private Key
       ↓
Managed Node
       |
       | Public Key
       ↓
~/.ssh/authorized_keys
```

Managed Node lưu public key trong `authorized_keys`, trong khi Automation Server giữ private key. 

## 4. Sử dụng SSH Agent Forwarding

Trước tiên, kiểm tra SSH Agent trên máy Windows.

Sau đó SSH vào Automation Server với **Agent Forwarding**.

Sau khi đăng nhập vào Automation Server, kiểm tra:

```bash
ssh-add -l
```

Nếu hiển thị fingerprint của key, Automation Server có thể sử dụng key thông qua SSH Agent trong khi private key thực tế vẫn nằm trên máy Windows. fileciteturn18file6



## 5. Kết nối tới Managed Node

Từ Automation Server, SSH tới Managed Node.

Ví dụ:

```bash
ssh ubuntu@10.0.2.171
```

Sau khi đăng nhập vào Managed Node, tạo thư mục SSH:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

Sau đó mở file:

```bash
nano ~/.ssh/authorized_keys
```

Đưa public key của Automation Server vào file `authorized_keys` và thiết lập quyền:

```bash
chmod 600 ~/.ssh/authorized_keys
```
![ATSV](/images/01/image_091.png)
![ATSV](/images/01/image_092.png)
![ATSV](/images/01/image_093.png)

Các bước này được thực hiện để Managed Node có thể xác thực Automation Server bằng public key. 

![ATSV](/images/01/image_086.png)
![ATSV](/images/01/image_087.png)

## 6. Kiểm tra SSH bằng SSH Key

Sau khi public key đã được cấu hình, từ Automation Server kiểm tra kết nối:

```bash
ssh -i ~/.ssh/id_ed25519 ubuntu@10.0.2.171
```

Nếu kết nối thành công, Automation Server đã có thể SSH tới Managed Node bằng SSH key. 
![ATSV](/images/01/image_089.png)

Thực hiện tương tự với `Managed-Node-02`.

## 7. Tạo SSH Config

Để không phải nhập đầy đủ địa chỉ IP và SSH key mỗi lần kết nối, tạo file:

```bash
nano ~/.ssh/config
```

Cấu hình:

```text
Host managed-01
    HostName 10.0.2.171
    User ubuntu
    IdentityFile ~/.ssh/id_ed25519

Host managed-02
    HostName 10.0.2.102
    User ubuntu
    IdentityFile ~/.ssh/id_ed25519
```
![ATSV](/images/01/image_095.png)

Trong đó:

- `managed-01` và `managed-02` là hostname dùng để kết nối.
- `HostName` là địa chỉ IP private của Managed Node.
- `User` là user `ubuntu`.
- `IdentityFile` chỉ định SSH private key được sử dụng.

Đây là cấu hình được sử dụng trong project để đơn giản hóa việc kết nối tới hai Managed Nodes. 

Sau đó thiết lập quyền:

```bash
chmod 600 ~/.ssh/config
```

![ATSV](/images/01/image_096.png)

## 8. Kiểm tra kết nối bằng hostname

Sau khi tạo SSH Config, có thể kết nối trực tiếp bằng:

```bash
ssh managed-01
```

và:

```bash
ssh managed-02
```

Nếu cả hai kết nối thành công, SSH giữa Automation Server và Managed Nodes đã được thiết lập.

```text
Automation Server
       |
       +── ssh managed-01
       |
       └── ssh managed-02
```

![ATSV](/images/01/image_097.png)
![ATSV](/images/01/image_098.png)

## Kết quả

Sau khi hoàn thành, hệ thống có mô hình kết nối:

```text
                     Automation Server
                            |
                     SSH Authentication
                            |
              +-------------+-------------+
              |                           |
         managed-01                  managed-02
              |                           |
      Managed-Node-01              Managed-Node-02
        Private EC2                  Private EC2
```

Automation Server hiện đã có thể SSH tới hai Managed Nodes bằng SSH key. Đây là nền tảng để bước tiếp theo cấu hình **Ansible Inventory** và để Ansible bắt đầu quản lý các Managed Nodes. fileciteturn18file5
