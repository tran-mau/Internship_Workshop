---
title : "Security Audit"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.4.3 </b> "
---

### Tổng quan

Sau khi triển khai **SSH Hardening** và **Firewall**, project cần có cơ chế kiểm tra để xác định trạng thái bảo mật của các Managed Nodes.

Trong phần Ansible, chức năng **Security Audit** được tổ chức thông qua:

```text
ansible/playbooks/security_audit.yml
```

Playbook này được sử dụng để thực hiện quá trình kiểm tra bảo mật trên các Managed Nodes.


### 1. Playbook security_audit.yml

File:

```text
ansible/playbooks/security_audit.yml
```

đóng vai trò điều phối quá trình Security Audit.

Luồng xử lý tổng quát:

```text
Automation Server
        |
      Ansible
        |
security_audit.yml
        |
        ↓
Managed Nodes
        |
        ↓
Security Audit
```
![ASAU](/images/01/image_231.png)

### 2. Mục đích của Security Audit

Security Audit được sử dụng để kiểm tra trạng thái cấu hình bảo mật trên Managed Nodes.

Trong project, quá trình kiểm tra liên quan đến các thành phần bảo mật đã được triển khai, đặc biệt:

```text
Managed Node
    |
    +── SSH configuration
    |
    └── Firewall configuration
```

Kết quả kiểm tra được sử dụng để xác định trạng thái bảo mật của từng Managed Node.



### 3. Cách Security Audit hoạt động

Khi thực thi Playbook, Ansible sử dụng Inventory để xác định các Managed Nodes cần kiểm tra.

Sau đó, các task trong `security_audit.yml` được thực hiện trên những host mục tiêu.

```text
Inventory
    |
    ↓
security_audit.yml
    |
    ↓
Audit Tasks
    |
    ↓
Managed-Node-01
Managed-Node-02
```

Các task thực hiện việc thu thập hoặc kiểm tra thông tin liên quan đến trạng thái bảo mật.

### 4. Kết hợp với các thành phần Security

Security Audit là bước kiểm tra sau khi các cấu hình bảo mật được triển khai.

```text
             Security
                 |
       +---------+---------+
       |                   |
       ↓                   ↓
 SSH Hardening         Firewall
       |                   |
       +---------+---------+
                 |
                 ↓
          Security Audit
                 |
                 ↓
          Audit Result
```

Trong đó:

- **SSH Hardening** áp dụng cấu hình bảo mật cho SSH.
- **Firewall** kiểm soát lưu lượng mạng.
- **Security Audit** kiểm tra trạng thái sau khi cấu hình.

### 5. Thực thi Security Audit

Từ Automation Server, chạy:

```bash
ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/security_audit.yml
```

Trong đó:

- `ansible-playbook`: thực thi Playbook.
- `-i`: chỉ định Inventory.
- `hosts.ini`: xác định Managed Nodes.
- `security_audit.yml`: Playbook thực hiện Security Audit.

![ASAU](/images/01/image_232.png)
### 6. Kiểm tra kết quả

Sau khi Playbook hoàn thành, kiểm tra output để xác nhận quá trình Audit đã thực hiện thành công.

```text
Security Audit
      |
      +── Managed-Node-01
      |
      └── Managed-Node-02
```

![ASAU](/images/01/image_233.png)

Các kết quả Audit có thể được sử dụng ở phần **Python Security Engine** để tiếp tục phân tích trạng thái bảo mật.

### 7. Luồng hoạt động tổng thể

```text
                  Automation Server
                         |
                       Ansible
                         |
                      Inventory
                         |
                         ↓
                security_audit.yml
                         |
               +---------+---------+
               |                   |
               ↓                   ↓
        Managed-Node-01     Managed-Node-02
               |                   |
               +---------+---------+
                         |
                         ↓
                  Security Audit
                         |
                         ↓
                    Audit Result
```

Security Audit tạo bước chuyển từ **cấu hình bảo mật** sang **kiểm tra trạng thái bảo mật**.

### Kết quả

Sau khi hoàn thành, project có quy trình:

```text
Configure
    ↓
SSH Hardening + Firewall
    ↓
Security Audit
    ↓
Check Security Status
```

Ansible chịu trách nhiệm thực hiện quá trình kiểm tra trên các Managed Nodes. Kết quả này sẽ được sử dụng làm cơ sở cho phần **Python Security Engine**.


