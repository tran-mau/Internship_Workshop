---
title : "Ansible Roles và Policies"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.3.4 </b> "
---

### Tổng quan

Trong project, **Ansible Roles** được sử dụng để tổ chức các thành phần automation theo từng chức năng. Bên cạnh Roles, thư mục `policies/` chứa các chính sách bảo mật được sử dụng trong hệ thống.

Cấu trúc:

```text
ansible/
├── policies/
│   └── security_policy.yml
│
└── roles/
    ├── common/
    │   ├── defaults/
    │   │   └── main.yml
    │   ├── handlers/
    │   │   └── main.yml
    │   └── tasks/
    │       └── main.yml
    │
    ├── firewall/
    │   ├── defaults/
    │   │   └── main.yml
    │   └── tasks/
    │       └── main.yml
    │
    └── ssh_hardening/
        ├── defaults/
        │   └── main.yml
        ├── handlers/
        │   └── main.yml
        └── tasks/
            └── main.yml
```

![ASAU](/images/01/image_215.png)

### 1. Ansible Role là gì?

Role là cách Ansible tổ chức các task, variables và handlers thành một cấu trúc riêng biệt.

Thay vì đặt toàn bộ task vào một Playbook lớn, project chia automation thành các Role theo chức năng.

```text
Playbook
   |
   +── common
   |
   +── firewall
   |
   └── ssh_hardening
```

Cách tổ chức này giúp code dễ đọc, dễ bảo trì và có thể tái sử dụng.

### 2. Role common

Role:

```text
roles/common/
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
└── tasks/
    └── main.yml
```

`common` chứa các thành phần cấu hình dùng chung.

Trong đó:

- `tasks/main.yml`: chứa các task chính của Role.
- `defaults/main.yml`: chứa các giá trị mặc định của Role.
- `handlers/main.yml`: chứa các Handler được gọi khi có task yêu cầu thực hiện.

![ASAU](/images/01/image_216.png)
![ASAU](/images/01/image_217.png)



### 3. Role firewall

Role:

```text
roles/firewall/
├── defaults/
│   └── main.yml
└── tasks/
    └── main.yml
```

Role `firewall` tập trung vào các tác vụ liên quan đến Firewall.

Các cấu hình hoặc giá trị có thể thay đổi được tổ chức trong:

```text
defaults/main.yml
```

Các task thực thi được đặt trong:

```text
tasks/main.yml
```
![ASAU](/images/01/image_218.png)

### 4. Role ssh_hardening

Role:

```text
roles/ssh_hardening/
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
└── tasks/
    └── main.yml
```

Role `ssh_hardening` tập trung vào các tác vụ bảo mật SSH.

Cấu trúc gồm:

- `tasks/main.yml`: các task thực hiện SSH Hardening.
- `defaults/main.yml`: các giá trị mặc định.
- `handlers/main.yml`: các Handler phục vụ việc áp dụng thay đổi khi cần thiết.

![ASAU](/images/01/image_219.png)

### 5. Defaults

Các Role có thể sử dụng:

```text
defaults/main.yml
```

để khai báo giá trị mặc định.

Ví dụ về luồng sử dụng:

```text
defaults/main.yml
        |
        ↓
     Role
        |
        ↓
 tasks/main.yml
```

Việc tách các giá trị cấu hình khỏi task giúp Role linh hoạt hơn khi được sử dụng trong các môi trường hoặc trường hợp khác nhau.

### 6. Tasks

File:

```text
tasks/main.yml
```

là thành phần chính chứa các task của Role.

Khi Role được gọi, Ansible thực thi các task được định nghĩa trong file này theo thứ tự.


### 7. Handlers

Một số Role có:

```text
handlers/main.yml
```

Handler được sử dụng cho những tác vụ chỉ cần thực hiện khi một task trước đó tạo ra thay đổi và gửi thông báo (`notify`).

Luồng cơ bản:

```text
Task
  |
  | changed
  ↓
notify
  |
  ↓
Handler
```

Trong project, `common` và `ssh_hardening` có thư mục `handlers`.

![ASAU](/images/01/image_221.png)

### 8. Security Policy

Ngoài Roles, project có:

```text
ansible/policies/security_policy.yml
```

File này thuộc nhóm **Policies**, dùng để lưu các tiêu chí hoặc cấu hình liên quan đến chính sách bảo mật của hệ thống.

Việc tách Security Policy thành một file riêng giúp phần chính sách không bị trộn lẫn trực tiếp với phần task thực thi.

![ASAU](/images/01/image_222.png)

### 9. Mối quan hệ giữa Roles, Playbooks và Policies

Các thành phần phối hợp theo mô hình:

```text
                 Security Policy
                       |
                       ↓
                 security_policy.yml
                       |
                       |
Inventory → Playbook → Role
                       |
              +--------+--------+
              |        |        |
              ↓        ↓        ↓
           common   firewall  ssh_hardening
              |        |        |
              +--------+--------+
                       |
                       ↓
                 Managed Nodes
```

Playbook xác định quá trình automation, Role tổ chức các task theo chức năng, còn Policy cung cấp các tiêu chí hoặc cấu hình bảo mật được sử dụng trong hệ thống.

### 10. Kết quả

Sau khi tổ chức Roles và Policies, phần Ansible của project có cấu trúc:

```text
ansible/
│
├── policies/
│   └── security_policy.yml
│
└── roles/
    ├── common/
    ├── firewall/
    └── ssh_hardening/
```

Cách tổ chức này giúp project tách biệt rõ:

```text
Playbooks → Điều phối automation
Roles     → Tổ chức task theo chức năng
Policies  → Quản lý tiêu chí bảo mật
```

Đây là nền tảng để triển khai các chức năng **Security Hardening, Security Audit và Automated Remediation** trong các phần tiếp theo.


