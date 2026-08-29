---
title : "Thiết lập Project"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

### Các bước thực hiện

Sau khi đã chuẩn bị Python và Ansible, chúng ta tiến hành tạo cấu trúc project trên **Automation Server**.

Project sử dụng thư mục chính:

```text
~/enterprise-infrastructure-automation
```

## 1. Tạo cấu trúc thư mục Ansible

Di chuyển vào thư mục project:

```bash
cd ~/enterprise-infrastructure-automation
```

Tạo các thư mục chính:

```bash
mkdir -p ansible/inventory
mkdir -p ansible/playbooks
mkdir -p ansible/roles
```

Cấu trúc ban đầu:

```text
enterprise-infrastructure-automation/
│
├── .venv/
├── ansible/
│   ├── inventory/
│   ├── playbooks/
│   └── roles/
│
└── .gitignore
```

Đây là cấu trúc nền tảng để tổ chức các thành phần Ansible của project.

![ATSV](/images/01/image_100.png)

## 2. Tạo file .gitignore

Tạo hoặc chỉnh sửa file `.gitignore`:

```bash
nano .gitignore
```

File này được sử dụng để yêu cầu Git bỏ qua những file và thư mục không cần đưa vào source code của project.

Một số nội dung được sử dụng trong project:

```text
.venv/
__pycache__/
*.pyc
*.pem
*.key
.env
*.log
reports/*.tmp
```

Trong đó, `.venv/` được bỏ qua vì đây là môi trường Python ảo, còn các file như `*.pem`, `*.key` và `.env` được bỏ qua để tránh đưa thông tin nhạy cảm vào repository.


## 3. Kiểm tra cấu trúc Project

Sau khi tạo các thư mục, kiểm tra lại:

```bash
tree -L 3
```

Cấu trúc lúc này sẽ là nền tảng để tiếp tục xây dựng:

```text
enterprise-infrastructure-automation/
│
├── ansible/
│   ├── inventory/
│   ├── playbooks/
│   └── roles/
│
├── .venv/
└── .gitignore
```

Các thư mục `inventory`, `playbooks` và `roles` sẽ lần lượt được sử dụng để khai báo Managed Nodes, xây dựng Playbooks và tổ chức Ansible Roles.



## Kết quả

Sau khi hoàn thành, Automation Server đã có một workspace riêng cho project:

```text
~/enterprise-infrastructure-automation/
│
├── .venv/
├── .gitignore
└── ansible/
    ├── inventory/
    ├── playbooks/
    └── roles/
```

Project đã sẵn sàng để chuyển sang bước tiếp theo là **thiết lập SSH giữa Automation Server và Managed Nodes**, sau đó xây dựng **Ansible Inventory**.
