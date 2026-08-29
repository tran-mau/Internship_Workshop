---
title : "Python Security Engine"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

### Tổng quan

Trong project, **Python Security Engine** là thành phần chịu trách nhiệm xử lý và phân tích thông tin bảo mật sau khi Ansible thực hiện các tác vụ trên Managed Nodes.

Khác với Ansible, thành phần Python tập trung vào việc xây dựng logic kiểm tra, xử lý Security Finding, quản lý trạng thái và tạo báo cáo.

Toàn bộ thành phần Python được tổ chức trong thư mục:

```text
python/
```

### Cấu trúc Python

Cấu trúc chính của Python Security Engine trong project:

```text
python/
├── main.py
│
├── checks/
│   ├── firewall_checks.py
│   └── ssh_checks.py
│
├── models/
│   └── finding.py
│
├── security_engine/
│   ├── ansible_runner.py
│   ├── engine.py
│   ├── policy_loader.py
│   └── remediation.py
│
└── reporters/
    ├── console.py
    └── json_reporter.py
```

![ASAU](/images/01/image_234.png)

### Danh sách các thành phần

1. **`main.py`**
   - Là điểm khởi chạy của chương trình Python.
   - Điều phối các thành phần của Security Engine.

2. **`checks/`**
   - Chứa các module thực hiện kiểm tra bảo mật.
   - `ssh_checks.py`: kiểm tra các vấn đề liên quan đến SSH.
   - `firewall_checks.py`: kiểm tra các vấn đề liên quan đến Firewall.

3. **`models/`**
   - Chứa các model dùng để biểu diễn dữ liệu.
   - `finding.py` định nghĩa cấu trúc của một Security Finding.

4. **`security_engine/`**
   - Chứa logic chính của hệ thống.
   - `ansible_runner.py`: tương tác với Ansible.
   - `engine.py`: xử lý logic Security Engine.
   - `policy_loader.py`: tải Security Policy.
   - `remediation.py`: xử lý quá trình remediation.

5. **`reporters/`**
   - Chứa các thành phần xuất kết quả.
   - `console.py`: hiển thị kết quả trên console.
   - `json_reporter.py`: xuất kết quả dưới dạng JSON.

### Luồng hoạt động tổng thể

Các thành phần Python phối hợp theo luồng:

```text
                    main.py
                       |
                       ↓
              Security Engine
                       |
          +------------+------------+
          |            |            |
          ↓            ↓            ↓
       Checks       Policies     Ansible
          |            |            |
          +------------+------------+
                       |
                       ↓
                    Finding
                       |
                       ↓
                   Reporting
                  /         \
                 ↓           ↓
             Console        JSON
```

Security Engine nhận thông tin từ các thành phần liên quan, thực hiện kiểm tra theo policy, tạo Security Finding và chuyển kết quả đến các Reporter.

### Mối quan hệ giữa Ansible và Python

Trong kiến trúc project, Ansible và Python đảm nhiệm các vai trò khác nhau:

```text
              Automation Server
                      |
          +-----------+-----------+
          |                       |
          ↓                       ↓
       Ansible                  Python
          |                       |
          ↓                       ↓
Configuration              Security Analysis
  & Automation                  |
          |                       ↓
          |                    Finding
          |                       |
          +-----------+-----------+
                      |
                      ↓
                   Output
```

Ansible tập trung vào **automation và configuration management**, trong khi Python tập trung vào **security checking, xử lý Finding, remediation và reporting**.

### Các nhóm chức năng chính

Python Security Engine được chia thành các nhóm:

```text
Python Security Engine
│
├── Checks
│   ├── SSH
│   └── Firewall
│
├── Security Engine
│   ├── Ansible Runner
│   ├── Policy Loader
│   └── Remediation
│
├── Models
│   └── Finding
│
└── Reporters
    ├── Console
    └── JSON
```

Cách tổ chức này giúp tách riêng phần **kiểm tra**, **xử lý**, **mô hình dữ liệu** và **xuất kết quả**.

### Kết quả

Sau khi xây dựng Python Security Engine, project có một thành phần riêng để xử lý các vấn đề bảo mật bên cạnh Ansible:

```text
Ansible
   ↓
Automation / Configuration
   ↓
Managed Nodes
   ↓
Python Security Engine
   ↓
Security Checks
   ↓
Finding
   ↓
Reports / Remediation
```

Phần tiếp theo sẽ đi sâu vào **Security Checks**, trong đó tập trung vào cách `ssh_checks.py` và `firewall_checks.py` kiểm tra trạng thái bảo mật.

