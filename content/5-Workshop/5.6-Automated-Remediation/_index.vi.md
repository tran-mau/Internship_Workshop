---
title : "Automated Remediation"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 5.6 </b> "
---

### Tổng quan

Sau khi hệ thống thực hiện Security Checks và xác định các vấn đề bảo mật, bước tiếp theo là **Remediation**.

Trong project, chức năng Remediation được tổ chức trong Python Security Engine và có sự kết hợp giữa Python và Ansible.

Thành phần chính liên quan đến Remediation:

```text
python/
└── security_engine/
    └── remediation.py
```

Bên cạnh đó, Ansible đảm nhiệm việc thực thi các thay đổi trên Managed Nodes.


### 1. Vai trò của Automated Remediation

Automated Remediation nhằm xử lý các vấn đề được phát hiện trong quá trình Security Audit thay vì yêu cầu người quản trị thực hiện thủ công từng bước.

Luồng tổng quát:

```text
Security Check
      |
      ↓
   Finding
      |
      ↓
Remediation
      |
      ↓
   Ansible
      |
      ↓
Managed Nodes
      |
      ↓
Verify
```

Như vậy, hệ thống có thể tạo thành một quy trình khép kín từ phát hiện vấn đề đến xử lý và kiểm tra lại.

### 2. remediation.py

File:

```text
python/security_engine/remediation.py
```

là thành phần liên quan đến quá trình Remediation trong Python Security Engine.

Nó nằm giữa bước phát hiện Finding và bước thực hiện thay đổi trên Managed Nodes.

```text
Finding
   |
   ↓
remediation.py
   |
   ↓
Ansible
   |
   ↓
Managed Node
```
![ASAU](/images/01/image_262.png)
![ASAU](/images/01/image_263.png)
![ASAU](/images/01/image_264.png)


### 3. Kết hợp Python và Ansible

Trong kiến trúc project, Python và Ansible đảm nhiệm hai vai trò khác nhau.

```text
Python
  |
  | Phân tích / quyết định
  ↓
Remediation
  |
  | Gọi automation
  ↓
Ansible
  |
  | Thực thi thay đổi
  ↓
Managed Nodes
```

Python chịu trách nhiệm xử lý logic của Security Engine, trong khi Ansible cung cấp cơ chế automation để áp dụng cấu hình trên Managed Nodes.

### 4. Quy trình Detect → Remediate → Verify

Automated Remediation có thể được mô tả theo ba giai đoạn:

```text
       Detect
          ↓
      Finding
          ↓
      Remediate
          ↓
      Managed Node
          ↓
       Verify
          ↓
    Security Status
```

#### Detect

Security Checks kiểm tra trạng thái của Managed Nodes và tạo Finding khi phát hiện vấn đề.

#### Remediate

Security Engine xác định cách xử lý Finding và thực hiện remediation thông qua cơ chế automation của project.

#### Verify

Sau khi remediation hoàn thành, hệ thống có thể kiểm tra lại trạng thái để xác định vấn đề đã được xử lý hay chưa.

![ASAU](/images/01/image_265.png)

### 5. Mối quan hệ với Security Policy

Security Policy cung cấp các tiêu chí mà hệ thống sử dụng để đánh giá trạng thái bảo mật.

Luồng tổng quát:

```text
Security Policy
      |
      ↓
Security Checks
      |
      ↓
   Finding
      |
      ↓
Remediation
      |
      ↓
Managed Nodes
```

Điều này giúp quá trình remediation hướng tới việc đưa Managed Node về trạng thái phù hợp với policy của project.

### 6. Mối quan hệ với Ansible Playbooks

Ansible là lớp thực thi automation.

```text
Python Security Engine
          |
          ↓
      Remediation
          |
          ↓
       Ansible
          |
          ↓
      Playbook / Role
          |
          ↓
    Managed Nodes
```

Playbook và Role thực hiện các thay đổi cần thiết trên máy chủ theo thiết kế của project.

### 7. Luồng hoạt động tổng thể

```text
                    Managed Nodes
                         |
                         ↓
                  Security Checks
                         |
                         ↓
                      Finding
                         |
                         ↓
                  Security Engine
                         |
                         ↓
                  remediation.py
                         |
                         ↓
                      Ansible
                         |
                         ↓
                  Managed Nodes
                         |
                         ↓
                     Verify
                         |
                         ↓
                  Updated State
```

Quy trình này tạo thành vòng lặp:

```text
Detect → Remediate → Verify
```

Kết quả sau khi Verify có thể tiếp tục được lưu vào Security State hoặc Report.

### 8. Kết quả

Sau khi triển khai Automated Remediation, project có thể xây dựng quy trình xử lý bảo mật theo hướng tự động:

```text
Security Audit
      ↓
Detect Finding
      ↓
Remediation
      ↓
Ansible
      ↓
Managed Node
      ↓
Verify
      ↓
Report / State
```

Điểm quan trọng của kiến trúc này là **Python không trực tiếp thay thế Ansible**, mà sử dụng Python để xử lý logic Security Engine và kết hợp Ansible để thực hiện automation trên Managed Nodes.

