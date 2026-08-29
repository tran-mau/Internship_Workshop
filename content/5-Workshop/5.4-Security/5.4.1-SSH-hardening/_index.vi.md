---
title : "SSH Hardening"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

### Tổng quan

Sau khi hoàn thành phần Ansible Automation và thiết lập kết nối SSH, project chuyển sang **Security**.

SSH Hardening là một trong những chức năng bảo mật được triển khai bằng Ansible. Mục tiêu của phần này là áp dụng các cấu hình bảo mật cho dịch vụ SSH trên các Managed Nodes.

Trong project, chức năng SSH Hardening được tổ chức thông qua:

```text
ansible/
├── playbooks/
│   └── ssh_hardening.yml
│
└── roles/
    └── ssh_hardening/
        ├── defaults/
        │   └── main.yml
        ├── handlers/
        │   └── main.yml
        └── tasks/
            └── main.yml
```


### 1. Playbook ssh_hardening.yml

File:

```text
ansible/playbooks/ssh_hardening.yml
```

đóng vai trò điều phối quá trình SSH Hardening.

Playbook xác định các Managed Nodes là đối tượng được áp dụng cấu hình và gọi Role `ssh_hardening`.

Luồng xử lý:

```text
ssh_hardening.yml
        |
        ↓
ssh_hardening Role
        |
        ↓
SSH configuration
        |
        ↓
Managed Nodes
```

![ASAU](/images/01/image_223.png)

### 2. Role ssh_hardening

Role:

```text
ansible/roles/ssh_hardening/
```

được sử dụng để tổ chức các task liên quan đến SSH Hardening.

Role được chia thành các thành phần:

```text
ssh_hardening/
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
└── tasks/
    └── main.yml
```

Cách tổ chức này giúp tách phần cấu hình mặc định, task thực thi và handler thành các thành phần riêng biệt.

### 3. Tasks

File:

```text
roles/ssh_hardening/tasks/main.yml
```

là nơi chứa các task thực hiện SSH Hardening.

Khi Role được gọi từ Playbook, Ansible thực thi các task trong file này trên các Managed Nodes.

![ASAU](/images/01/image_224.png)

**Cách hoạt động:**

```text
Playbook
   ↓
Role ssh_hardening
   ↓
tasks/main.yml
   ↓
Managed Node
   ↓
SSH configuration changed
```



### 4. Defaults

File:

```text
roles/ssh_hardening/defaults/main.yml
```

chứa các giá trị mặc định được Role sử dụng.

Việc đặt các giá trị có thể thay đổi trong `defaults` giúp tách cấu hình khỏi phần task thực thi.

![ASAU](/images/01/image_225.png)

### 5. Handlers

File:

```text
roles/ssh_hardening/handlers/main.yml
```

chứa các Handler được sử dụng khi một thay đổi trong SSH configuration yêu cầu thực hiện thêm một hành động.

Luồng cơ bản:

```text
Task
  |
  | thay đổi cấu hình
  ↓
notify
  |
  ↓
Handler
```

![ASAU](/images/01/image_226.png)

### 6. Luồng hoạt động tổng thể

SSH Hardening được triển khai theo mô hình:

```text
                 Automation Server
                        |
                     Ansible
                        |
               ssh_hardening.yml
                        |
                 ssh_hardening
                     Role
                        |
              +---------+---------+
              |                   |
              ↓                   ↓
       Managed-Node-01     Managed-Node-02
              |                   |
              ↓                   ↓
        SSH Hardening       SSH Hardening
```

Ansible lấy các host mục tiêu từ Inventory, gọi Playbook `ssh_hardening.yml`, sau đó Role `ssh_hardening` thực hiện các task trên Managed Nodes.

### 7. Kiểm tra kết quả

Sau khi thực hiện SSH Hardening, cần kiểm tra kết quả trên Managed Nodes để xác nhận cấu hình đã được áp dụng.


![ASAU](/images/01/image_227.png)

### Kết quả

Sau khi hoàn thành, SSH Hardening được tổ chức theo:

```text
ssh_hardening.yml
        ↓
ssh_hardening Role
        ↓
tasks / defaults / handlers
        ↓
Managed Nodes
```

Cách tổ chức này giúp tách phần điều phối Playbook khỏi phần triển khai SSH Hardening, đồng thời tạo cấu trúc rõ ràng để bảo trì và mở rộng.


