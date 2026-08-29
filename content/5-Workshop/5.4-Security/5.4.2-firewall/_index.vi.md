---
title : "Firewall"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

### Tổng quan

Bên cạnh SSH Hardening, project sử dụng **Firewall** như một lớp bảo vệ bổ sung trên các Managed Nodes.

Trong phần Ansible, chức năng Firewall được tổ chức thông qua Playbook và Role:

```text
ansible/
├── playbooks/
│   └── firewall.yml
│
└── roles/
    └── firewall/
        ├── defaults/
        │   └── main.yml
        └── tasks/
            └── main.yml
```


### 1. Playbook firewall.yml

File:

```text
ansible/playbooks/firewall.yml
```

đóng vai trò điều phối quá trình cấu hình Firewall.

Playbook xác định các host mục tiêu và gọi Role `firewall` để thực hiện các task liên quan đến Firewall.

Luồng xử lý:

```text
firewall.yml
      |
      ↓
firewall Role
      |
      ↓
Firewall Tasks
      |
      ↓
Managed Nodes
```

![ASAU](/images/01/image_228.png)

### 2. Role firewall

Role:

```text
ansible/roles/firewall/
```

được sử dụng để tổ chức các task cấu hình Firewall.

Role gồm:

```text
firewall/
├── defaults/
│   └── main.yml
└── tasks/
    └── main.yml
```

Trong đó:

- `tasks/main.yml`: chứa các task thực hiện cấu hình Firewall.
- `defaults/main.yml`: chứa các giá trị mặc định được Role sử dụng.

### 3. Firewall Tasks

File:

```text
roles/firewall/tasks/main.yml
```

là thành phần trực tiếp thực hiện các thay đổi liên quan đến Firewall trên Managed Nodes.

Khi `firewall.yml` gọi Role `firewall`, Ansible sẽ thực thi các task trong file này.

```text
Playbook
   ↓
firewall Role
   ↓
tasks/main.yml
   ↓
Managed Node
   ↓
Firewall configuration
```

![ASAU](/images/01/image_229.png)


### 4. Defaults

File:

```text
roles/firewall/defaults/main.yml
```

chứa các giá trị mặc định cho Role Firewall.

Việc tách các giá trị cấu hình khỏi `tasks/main.yml` giúp Role dễ thay đổi và quản lý hơn.



### 5. Cách Firewall được triển khai

Luồng triển khai Firewall:

```text
                 Automation Server
                        |
                     Ansible
                        |
                   firewall.yml
                        |
                   firewall Role
                        |
              +---------+---------+
              |                   |
              ↓                   ↓
       Managed-Node-01     Managed-Node-02
              |                   |
              ↓                   ↓
          Firewall            Firewall
```

Automation Server thực thi Playbook, Playbook gọi Role và Role thực hiện các task trên Managed Nodes.

### 6. Kiểm tra kết quả

Sau khi thực thi Playbook, cần kiểm tra kết quả trên Managed Nodes để xác nhận Firewall đã được cấu hình.

Việc kiểm tra cần sử dụng các command hoặc Playbook kiểm tra tương ứng với cấu hình thực tế của project.

![ASAU](/images/01/image_230.png)

### Kết quả

Sau khi hoàn thành, chức năng Firewall được tổ chức:

```text
firewall.yml
      ↓
firewall Role
      ↓
tasks/main.yml
      ↓
Managed Nodes
```

Firewall tạo thêm một lớp kiểm soát lưu lượng mạng trên Managed Nodes, đồng thời được triển khai tập trung thông qua Ansible.


