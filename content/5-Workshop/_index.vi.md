---

title : "Workshop"

date : "`r Sys.Date()`"

weight : 5

chapter : false

pre : " <b> 5. </b> "

---


### Tổng quan

Trong project này, chúng ta xây dựng một hệ thống **Enterprise Infrastructure Automation** nhằm tự động hóa việc triển khai, cấu hình, kiểm tra và quản lý các máy chủ Linux.

Project sử dụng **Amazon Web Services (AWS)** để xây dựng môi trường hạ tầng, **Ansible** để thực hiện configuration management và remediation, kết hợp với **Python** để xây dựng Security Engine phục vụ việc kiểm tra và đánh giá trạng thái bảo mật.

Môi trường triển khai gồm một **Automation Server** và hai **Managed Nodes**. Automation Server đóng vai trò là trung tâm điều khiển, trong khi Managed-Node-01 và Managed-Node-02 là các máy chủ được quản lý thông qua Ansible.

### Kiến trúc tổng thể

Kiến trúc của project được tổ chức theo mô hình:

```text
                    AWS VPC
                  10.0.0.0/16
                       |
          +------------+------------+
          |                         |
    Public Subnet             Private Subnet
     10.0.1.0/24               10.0.2.0/24
          |                         |
          |                 +-------+-------+
          |                 |               |
  Automation Server   Managed-Node-01  Managed-Node-02
          |
     Ansible + Python
```

Automation Server được triển khai trong **Public Subnet** và đóng vai trò là máy chủ điều khiển. Hai Managed Nodes được triển khai trong **Private Subnet** và được quản lý tập trung từ Automation Server.

Mô hình này giúp tách biệt máy chủ điều khiển khỏi các máy chủ được quản lý, đồng thời hạn chế việc Managed Nodes phải trực tiếp exposed ra Internet.

<!--
Chèn hình: Sơ đồ kiến trúc tổng thể của project.
Có thể sử dụng sơ đồ thể hiện AWS VPC, Public/Private Subnet,
Automation Server và hai Managed Nodes.
-->

### Công nghệ sử dụng

Project sử dụng các thành phần chính:

| Thành phần | Vai trò                                                   |
| ---------- | --------------------------------------------------------- |
| AWS VPC    | Xây dựng môi trường mạng cho project                      |
| AWS EC2    | Cung cấp các máy chủ Linux                                |
| Ansible    | Configuration management và automation                    |
| Python     | Xây dựng Security Engine                                  |
| SSH        | Thiết lập kết nối giữa Automation Server và Managed Nodes |
| Git        | Quản lý source code của project                           |

Các EC2 instance trong project sử dụng **Ubuntu Server 24.04 LTS**. Automation Server được cấu hình để chạy Ansible và Python, trong khi hai Managed Nodes được đặt trong Private Subnet để được quản lý tập trung.

### Luồng hoạt động

Quá trình hoạt động của hệ thống được triển khai theo các bước chính:

```text
AWS Infrastructure
        ↓
Automation Server
        ↓
SSH Connectivity
        ↓
Ansible Automation
        ↓
Security Hardening
        ↓
Security Audit
        ↓
Python Security Engine
        ↓
Automated Remediation
        ↓
Verification
```

Đầu tiên, AWS được sử dụng để xây dựng hạ tầng mạng và các EC2 instance. Sau đó, Automation Server được chuẩn bị với Python và Ansible.

Tiếp theo, SSH được thiết lập giữa Automation Server và các Managed Nodes. Ansible được sử dụng để quản lý cấu hình hệ thống, thực hiện security hardening và hỗ trợ kiểm tra trạng thái bảo mật.

Python Security Engine tiếp tục xử lý thông tin bảo mật, thực hiện các Security Checks và tạo ra các Security Findings. Khi phát hiện vấn đề cần khắc phục, Ansible được sử dụng để thực hiện remediation. Sau đó, hệ thống kiểm tra lại để xác minh trạng thái sau khi remediation.

### Nội dung Workshop

Workshop được chia thành các phần chính:

* **AWS Infrastructure** — Xây dựng VPC, Subnet, Internet Gateway, Route Table, Security Group và EC2.
* **Automation Server** — Chuẩn bị môi trường Python và Ansible.
* **SSH Connectivity** — Thiết lập kết nối giữa Automation Server và Managed Nodes.
* **Ansible Automation** — Xây dựng Inventory, Playbook và Roles.
* **Security** — Thực hiện SSH Hardening, Firewall và Security Audit.
* **Python Security Engine** — Xây dựng Security Checks, Security Engine và Reporting.
* **Automated Remediation** — Phát hiện, khắc phục và xác minh các vấn đề bảo mật.
* **Project Validation** — Kiểm tra toàn bộ luồng hoạt động của hệ thống.

Các phần tiếp theo sẽ lần lượt triển khai từng thành phần, bắt đầu từ việc xây dựng hạ tầng AWS, chuẩn bị Automation Server, thiết lập kết nối SSH, triển khai Ansible Automation và tiếp tục đến các chức năng Security, Python Security Engine và Automated Remediation.
