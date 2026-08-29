---
title : "Cấu trúc Ansible"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

### Tổng quan

Trong project, **Ansible** là thành phần chịu trách nhiệm quản lý và tự động hóa cấu hình trên các Managed Nodes.

Toàn bộ thành phần Ansible được tổ chức trong thư mục:

```text
ansible/
```

Cấu trúc chính gồm **Inventory, Playbooks, Policies, Roles và file cấu hình `ansible.cfg`**.

### 1. Cấu trúc thư mục

```text
ansible/
├── inventory/
│   ├── group_vars/
│   │   └── managed_nodes.yml
│   ├── host_vars/
│   │   ├── managed-01.yml
│   │   └── managed-02.yml
│   ├── hosts.example.ini
│   └── hosts.ini
│
├── playbooks/
│   ├── common.yml
│   ├── facts.yml
│   ├── firewall.yml
│   ├── security_audit.yml
│   ├── security_baseline.yml
│   ├── security_collect.yml
│   ├── ssh_hardening.yml
│   ├── system_info.yml
│   └── variables_demo.yml
│
├── policies/
│   └── security_policy.yml
│
├── roles/
│   ├── common/
│   ├── firewall/
│   └── ssh_hardening/
│
└── ansible.cfg
```

![ASAU](/images/01/image_197.png)

### 2. Inventory

Thư mục `inventory/` chứa thông tin về các Managed Nodes mà Ansible quản lý.

```text
inventory/
├── group_vars/
│   └── managed_nodes.yml
├── host_vars/
│   ├── managed-01.yml
│   └── managed-02.yml
├── hosts.example.ini
└── hosts.ini
```

Trong đó:

- `hosts.ini` chứa danh sách các Managed Nodes.
- `group_vars/` chứa các biến áp dụng cho một nhóm host.
- `host_vars/` chứa các biến riêng cho từng host.
- `hosts.example.ini` là file mẫu.

Inventory giúp Ansible xác định **máy chủ nào cần được quản lý** và các biến tương ứng.

### 3. Playbooks

Thư mục `playbooks/` chứa các Playbook thực hiện những nhiệm vụ automation khác nhau.

```text
playbooks/
├── common.yml
├── facts.yml
├── firewall.yml
├── security_audit.yml
├── security_baseline.yml
├── security_collect.yml
├── ssh_hardening.yml
├── system_info.yml
└── variables_demo.yml
```

Các Playbook được tổ chức theo chức năng như thu thập thông tin hệ thống, firewall, security audit, security baseline, security collection, SSH hardening và variables.

Playbook là nơi mô tả **các task mà Ansible sẽ thực hiện trên Managed Nodes**.

### 4. Policies

Thư mục `policies/` chứa:

```text
policies/
└── security_policy.yml
```

File `security_policy.yml` lưu các tiêu chí và cấu hình liên quan đến security policy của project.

### 5. Roles

Thư mục `roles/` tổ chức các automation component có thể tái sử dụng:

```text
roles/
├── common/
├── firewall/
└── ssh_hardening/
```

Các Role chính:

- `common`: cấu hình dùng chung.
- `firewall`: cấu hình firewall.
- `ssh_hardening`: cấu hình SSH Hardening.

Role giúp chia nhỏ automation thành các thành phần có cấu trúc rõ ràng và dễ quản lý.

### 6. Ansible Configuration

File:

```text
ansible.cfg
```

là file cấu hình chung cho Ansible.

File này xác định các thiết lập được sử dụng khi Ansible thực thi, chẳng hạn như Inventory và các tùy chọn liên quan đến quá trình chạy.

![ASAU](/images/01/image_200.png)

### 7. Luồng hoạt động tổng thể

```text
                 ansible.cfg
                      |
                      ↓
                  Inventory
                      |
          +-----------+-----------+
          |                       |
      group_vars               host_vars
          |                       |
          +-----------+-----------+
                      |
                      ↓
                  Playbook
                      |
                      ↓
                    Role
                      |
                      ↓
               Managed Nodes
```

Khi thực thi Playbook, Ansible sử dụng cấu hình trong `ansible.cfg`, lấy danh sách host từ Inventory, kết hợp variables và thực hiện các task trên Managed Nodes.

### Kết quả

```text
Ansible
│
├── Inventory   → Xác định Managed Nodes
├── Variables   → Cung cấp cấu hình
├── Playbooks   → Mô tả automation tasks
├── Policies    → Xác định security policy
├── Roles       → Tổ chức automation component
└── ansible.cfg → Cấu hình Ansible
```

Cấu trúc này là nền tảng cho các phần tiếp theo, trong đó chúng ta sẽ đi sâu vào **Inventory, Variables, Playbooks và Roles** của project.
