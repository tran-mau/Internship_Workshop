---
title : "Ansible Playbooks"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

### Tổng quan

**Ansible Playbook** là thành phần mô tả các tác vụ mà Ansible sẽ thực hiện trên các Managed Nodes.

Trong project, các Playbook được tổ chức trong thư mục:

```text
ansible/playbooks/
```

Cấu trúc hiện tại gồm:

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

Mỗi Playbook đảm nhiệm một nhóm chức năng riêng trong quá trình quản lý và bảo mật Managed Nodes.

![ASAU](/images/01/image_205.png)

### 1. common.yml

`common.yml` chứa các tác vụ cấu hình dùng chung cho Managed Nodes.

Playbook này được sử dụng khi cần thực hiện các thiết lập có tính chất cơ bản hoặc dùng chung cho nhiều máy chủ.

![ASAU](/images/01/image_206.png)

### 2. facts.yml

`facts.yml` được sử dụng để thu thập **Ansible Facts** từ Managed Nodes.

Facts cung cấp thông tin về máy chủ như hệ điều hành, hostname, địa chỉ mạng, bộ nhớ và các thông tin hệ thống khác.

![ASAU](/images/01/image_207.png)

### 3. system_info.yml

`system_info.yml` phục vụ việc thu thập hoặc hiển thị thông tin hệ thống của Managed Nodes.

Playbook này giúp kiểm tra trạng thái cơ bản của các máy chủ trước hoặc trong quá trình automation.

![ASAU](/images/01/image_208.png)

### 4. firewall.yml

`firewall.yml` liên quan đến việc cấu hình **Firewall** trên Managed Nodes.

Playbook này phối hợp với Role `firewall` để thực hiện các cấu hình firewall theo thiết kế của project.

![ASAU](/images/01/image_209.png)

### 5. ssh_hardening.yml

`ssh_hardening.yml` thực hiện các tác vụ liên quan đến **SSH Hardening**.

Playbook này phối hợp với Role `ssh_hardening` để áp dụng các cấu hình bảo mật cho dịch vụ SSH trên Managed Nodes.

![ASAU](/images/01/image_210.png)

### 6. security_audit.yml

`security_audit.yml` được sử dụng để thực hiện **Security Audit** trên Managed Nodes.

Mục đích là kiểm tra trạng thái cấu hình bảo mật và phát hiện những thiết lập chưa đáp ứng yêu cầu của project.

![ASAU](/images/01/image_211.png)

### 7. security_baseline.yml

`security_baseline.yml` liên quan đến việc thiết lập hoặc kiểm tra **Security Baseline**.

Security Baseline cung cấp một trạng thái cấu hình bảo mật cơ bản mà Managed Nodes cần đáp ứng.

![ASAU](/images/01/image_212.png)

### 8. security_collect.yml

`security_collect.yml` được sử dụng để thu thập thông tin trạng thái bảo mật từ Managed Nodes.

Dữ liệu được thu thập có thể được sử dụng bởi các thành phần Security Engine ở phần Python.

![ASAU](/images/01/image_213.png)

### 9. variables_demo.yml

`variables_demo.yml` được sử dụng để minh họa hoặc kiểm tra cách Ansible sử dụng **Variables** trong Playbook.

Playbook này liên quan trực tiếp đến cơ chế lấy giá trị từ Inventory, `group_vars` và `host_vars`.

![ASAU](/images/01/image_214.png)

### 10. Mối quan hệ giữa Playbook và các thành phần Ansible

Playbook không hoạt động độc lập mà sử dụng các thành phần khác của Ansible:

```text
                 ansible.cfg
                      |
                      ↓
                  Inventory
                      |
             +--------+--------+
             |                 |
         group_vars        host_vars
             |                 |
             +--------+--------+
                      |
                      ↓
                  Playbook
                      |
              +-------+-------+
              |       |       |
              ↓       ↓       ↓
           common  firewall  ssh_hardening
              |       |       |
              +-------+-------+
                      |
                      ↓
               Managed Nodes
```

Khi một Playbook được thực thi, Ansible xác định các host mục tiêu từ Inventory, lấy các biến tương ứng và thực hiện các task được mô tả trong Playbook hoặc Role.

### 11. Cách thực thi Playbook

Một Playbook có thể được thực thi bằng command:

```bash
ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/<playbook>.yml
```

Trong đó:

- `ansible-playbook` dùng để thực thi Playbook.
- `-i` chỉ định Inventory.
- `hosts.ini` xác định các Managed Nodes.
- `<playbook>.yml` là Playbook cần thực thi.

Ví dụ, khi cần chạy Playbook kiểm tra hoặc cấu hình security, command sẽ trỏ tới Playbook tương ứng trong thư mục `ansible/playbooks/`.


### 12. Luồng hoạt động

Luồng xử lý tổng quát:

```text
Ansible Control Node
        |
        ↓
    ansible.cfg
        |
        ↓
    Inventory
        |
        ↓
    Playbook
        |
        ↓
   Tasks / Roles
        |
        ↓
 Managed Nodes
```

Playbook đóng vai trò trung tâm trong việc mô tả **Ansible cần làm gì**, trong khi Inventory xác định **làm trên máy nào** và Variables cung cấp **các giá trị cấu hình cần thiết**.

### Kết quả

Sau khi xây dựng các Playbook, project có thể tổ chức các tác vụ automation theo từng chức năng:

```text
Ansible Playbooks
│
├── System Management
│   ├── common.yml
│   ├── facts.yml
│   └── system_info.yml
│
├── Security
│   ├── firewall.yml
│   ├── ssh_hardening.yml
│   ├── security_audit.yml
│   ├── security_baseline.yml
│   └── security_collect.yml
│
└── Variables
    └── variables_demo.yml
```

Cách tổ chức này giúp project tách biệt các nhiệm vụ automation và tạo nền tảng để sử dụng **Ansible Roles** trong phần tiếp theo.
