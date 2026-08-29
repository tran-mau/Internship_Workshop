---
title : "Cài đặt Ansible"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

### Các bước thực hiện

Trong project, **Ansible** là thành phần chịu trách nhiệm chính cho **configuration management và automation**. Automation Server sẽ sử dụng Ansible để quản lý các Managed Nodes trong các bước tiếp theo.

## 1. Cài đặt Ansible

Trên Automation Server, cập nhật package:

```bash
sudo apt update
```

Sau đó cài đặt Ansible:

```bash
sudo apt install -y ansible
```

![ATSV](/images/01/image_077.png)

## 2. Kiểm tra phiên bản Ansible

Sau khi cài đặt, kiểm tra Ansible:

```bash
ansible --version
```

Lệnh này giúp xác nhận Ansible đã được cài đặt thành công và hiển thị thông tin phiên bản cùng môi trường Python mà Ansible đang sử dụng.

![ATSV](/images/01/image_078.png)

## 3. Kiểm tra các command của Ansible

Kiểm tra vị trí của Ansible:

```bash
which ansible
```

Tiếp tục kiểm tra các command quan trọng:

```bash
which ansible-playbook
```

```bash
which ansible-inventory
```

```bash
which ansible-galaxy
```

Các command này sẽ được sử dụng trong quá trình xây dựng hệ thống automation.

![ATSV](/images/01/image_079.png)

## 4. Kiểm tra ansible-galaxy

Trong project, chúng ta sẽ sử dụng **Ansible Roles** và **Collections**.

`ansible-galaxy` là command được sử dụng để tạo và quản lý Roles/Collections.


## Kết quả

Sau khi hoàn thành, Automation Server đã có Ansible và các command cần thiết:

```text
Automation-Server
│
├── Python
├── Virtual Environment
├── Ansible
│   ├── ansible
│   ├── ansible-playbook
│   ├── ansible-inventory
│   └── ansible-galaxy
└── Git
```

Automation Server đã sẵn sàng để chuyển sang bước **thiết lập SSH kết nối với Managed Nodes** và sau đó xây dựng Ansible Inventory, Playbooks và Roles.
