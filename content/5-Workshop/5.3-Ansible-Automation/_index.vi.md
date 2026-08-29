---

title : "Ansible Automation"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.3 </b> "

---


### Tổng quan

Trong project, **Ansible Automation** được sử dụng để tự động hóa quá trình quản lý và cấu hình các Managed Nodes. Thay vì thực hiện thủ công trên từng máy chủ, Ansible cho phép tập trung các cấu hình và tác vụ quản trị thông qua Inventory, Playbooks, Roles và Security Policy.

Các thành phần chính của Ansible trong project bao gồm:

```text
Ansible Automation
│
├── Inventory
│   └── Xác định các Managed Nodes
│
├── Playbooks
│   └── Định nghĩa các tác vụ automation
│
├── Roles
│   └── Tổ chức các chức năng cấu hình
│
├── Policies
│   └── Xác định các yêu cầu bảo mật
│
└── ansible.cfg
    └── Cấu hình môi trường Ansible
```

### Danh sách các chương thực hành: 

  + [5.3.1 Kiến trúc Ansible]({{< relref "5.3.1-Ansible-Structure">}})  
  + [5.3.2 Ansible Inventory]({{< relref "5.3.2-Ansible-Inventory">}})  
  + [5.3.3 Ansible Playbooks]({{< relref "5.3.3-Playbooks">}})  
  + [5.3.4 Role Policies]({{< relref "5.3.4-Role-Policies">}})  
