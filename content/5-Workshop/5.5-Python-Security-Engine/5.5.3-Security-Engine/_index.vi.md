---
title : "Security Engine"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.5.3 </b> "
---

### Tổng quan

**Security Engine** là thành phần trung tâm trong Python Security Engine của project. Thành phần này chịu trách nhiệm điều phối quá trình kiểm tra bảo mật và kết nối các thành phần như Security Checks, Security Policy, Ansible và Finding.

Các file chính liên quan đến Security Engine:

```text
python/security_engine/
├── ansible_runner.py
├── engine.py
├── policy_loader.py
└── remediation.py
```

Trong đó:

- `engine.py`: xử lý logic trung tâm của Security Engine.
- `ansible_runner.py`: kết nối và thực thi các tác vụ thông qua Ansible.
- `policy_loader.py`: tải Security Policy.
- `remediation.py`: xử lý quá trình khắc phục vấn đề bảo mật.

![ASAU](/images/01/image_239.png)

### 1. Vai trò của Security Engine

Security Engine đóng vai trò kết nối các bước trong quy trình bảo mật:

```text
Security Policy
       |
       ↓
Security Engine
       |
   +---+---+
   |       |
   ↓       ↓
Checks   Ansible
   |       |
   +---+---+
       |
       ↓
    Finding
       |
       ↓
 Remediation
```

Nhờ đó, quá trình kiểm tra và xử lý bảo mật không nằm rời rạc ở từng module mà được điều phối thông qua một thành phần trung tâm.

### 2. engine.py

File:

```text
python/security_engine/engine.py
```

là thành phần trung tâm của Security Engine.

Nhiệm vụ cụ thể của file này là nơi điều phối quá trình xử lý giữa các thành phần kiểm tra, policy và kết quả.

![ASAU](/images/01/image_240.png)
![ASAU](/images/01/image_241.png)

Luồng tổng quát:

```text
Input
  |
  ↓
engine.py
  |
  +── Load Policy
  |
  +── Run Checks
  |
  +── Process Findings
  |
  └── Remediation
```


### 3. ansible_runner.py

File:

```text
python/security_engine/ansible_runner.py
```

được sử dụng để kết nối Python Security Engine với Ansible.

Mối quan hệ giữa hai thành phần:

```text
Python Security Engine
          |
          ↓
   ansible_runner.py
          |
          ↓
       Ansible
          |
          ↓
    Managed Nodes
```

Điều này cho phép Python sử dụng Ansible như một thành phần thực thi automation trên các Managed Nodes.

![ASAU](/images/01/image_242.png)
![ASAU](/images/01/image_243.png)

### 4. policy_loader.py

File:

```text
python/security_engine/policy_loader.py
```

được sử dụng để tải Security Policy.

Security Policy của project nằm trong:

```text
ansible/policies/security_policy.yml
```

Luồng xử lý:

```text
security_policy.yml
        |
        ↓
policy_loader.py
        |
        ↓
Security Engine
        |
        ↓
Security Checks
```

Việc tách Policy khỏi code xử lý giúp các tiêu chí bảo mật có thể được quản lý riêng với logic của Security Engine.

![ASAU](/images/01/image_244.png)

### 5. remediation.py

File:

```text
python/security_engine/remediation.py
```

liên quan đến quá trình **Remediation**.

Sau khi hệ thống phát hiện một vấn đề bảo mật, Remediation là bước xử lý để đưa hệ thống về trạng thái mong muốn.

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
Managed Node
```

![ASAU](/images/01/image_245.png)
![ASAU](/images/01/image_246.png)
![ASAU](/images/01/image_247.png)


### 6. Mối quan hệ giữa các thành phần

Các file trong `security_engine/` phối hợp với nhau:

```text
                 engine.py
                    |
       +------------+------------+
       |            |            |
       ↓            ↓            ↓
policy_loader  ansible_runner  remediation
       |            |            |
       ↓            ↓            ↓
 Security       Ansible       Fix
 Policy           |            |
                  ↓            |
            Managed Nodes <-----+
```

Trong đó:

- `policy_loader.py` cung cấp Policy.
- `ansible_runner.py` kết nối với Ansible.
- `engine.py` điều phối quá trình.
- `remediation.py` xử lý bước khắc phục.

### 7. Luồng hoạt động tổng thể

Security Engine nằm ở trung tâm của quy trình:

```text
                     Security Policy
                           |
                           ↓
                    policy_loader.py
                           |
                           ↓
                       engine.py
                           |
                +----------+----------+
                |                     |
                ↓                     ↓
        Security Checks        ansible_runner.py
                |                     |
                ↓                     ↓
             Finding             Ansible
                |                     |
                +----------+----------+
                           |
                           ↓
                    remediation.py
                           |
                           ↓
                     Managed Nodes
```

Quy trình này tạo thành chuỗi:

```text
Policy
  ↓
Check
  ↓
Finding
  ↓
Remediation
```

### 8. Kết quả

Sau khi xây dựng Security Engine, project có một thành phần trung tâm để liên kết:

```text
Security Policy
      ↓
Security Checks
      ↓
Security Engine
      ↓
Ansible
      ↓
Managed Nodes
      ↓
Finding / Remediation
```

Security Engine là cầu nối giữa **logic phân tích bảo mật của Python** và **khả năng automation của Ansible**.

