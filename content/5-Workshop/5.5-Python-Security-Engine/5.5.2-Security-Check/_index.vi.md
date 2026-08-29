---
title : "Security Checks"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

### Tổng quan

Trong Python Security Engine, **Security Checks** là nhóm thành phần thực hiện việc kiểm tra trạng thái bảo mật của Managed Nodes.

Các module kiểm tra được tổ chức trong:

```text
python/checks/
├── ssh_checks.py
└── firewall_checks.py
```

Hai module tập trung vào hai nhóm kiểm tra chính:

```text
Security Checks
│
├── ssh_checks.py
│   └── SSH
│
└── firewall_checks.py
    └── Firewall
```

![ASAU](/images/01/image_235.png)

### 1. Vai trò của Security Checks

Security Checks là lớp thực hiện các kiểm tra cụ thể trước khi kết quả được xử lý bởi Security Engine.

Luồng tổng quát:

```text
Managed Node
     |
     ↓
Security Checks
     |
     +── SSH Checks
     |
     └── Firewall Checks
             |
             ↓
          Finding
```

Các kết quả kiểm tra là cơ sở để hệ thống xác định những vấn đề bảo mật cần được xử lý.

### 2. ssh_checks.py

File:

```text
python/checks/ssh_checks.py
```

được sử dụng cho các kiểm tra liên quan đến cấu hình và trạng thái SSH.

Trong kiến trúc project, module này tập trung vào việc kiểm tra các tiêu chí SSH đã được định nghĩa trong hệ thống.

![ASAU](/images/01/image_236.png)
![ASAU](/images/01/image_237.png)
#### Cách hoạt động

Luồng xử lý của module:

```text
SSH configuration
       |
       ↓
ssh_checks.py
       |
       ↓
Check
       |
       ↓
Finding
```

Module nhận thông tin cần kiểm tra, thực hiện các điều kiện kiểm tra và tạo kết quả tương ứng.


### 3. firewall_checks.py

File:

```text
python/checks/firewall_checks.py
```

được sử dụng cho các kiểm tra liên quan đến Firewall.

Module này thực hiện các kiểm tra cần thiết để xác định trạng thái Firewall trên Managed Nodes.

![ASAU](/images/01/image_238.png)

#### Cách hoạt động

Luồng xử lý:

```text
Firewall configuration
       |
       ↓
firewall_checks.py
       |
       ↓
Check
       |
       ↓
Finding
```

Các kết quả kiểm tra Firewall được đưa vào quá trình xử lý Security Engine.

> **Lưu ý:** Các rule hoặc tiêu chí Firewall cụ thể cần được mô tả dựa trên code FINAL của `firewall_checks.py`.

### 4. Security Finding

Kết quả của các Security Checks được biểu diễn dưới dạng **Finding**.

Luồng:

```text
SSH Check ───────┐
                 |
                 ↓
              Finding
                 ↑
                 |
Firewall Check ──┘
```

Finding sẽ chứa thông tin cần thiết để các thành phần phía sau có thể phân tích và xử lý vấn đề bảo mật.

Cấu trúc cụ thể của Finding được định nghĩa trong:

```text
python/models/finding.py
```

Phần này sẽ được trình bày chi tiết ở mục **Finding và State**.

### 5. Mối quan hệ với Security Engine

Security Checks không tự đảm nhiệm toàn bộ quy trình bảo mật. Chúng là một phần trong Python Security Engine.

```text
                 Security Engine
                       |
              +--------+--------+
              |                 |
              ↓                 ↓
       ssh_checks.py     firewall_checks.py
              |                 |
              +--------+--------+
                       |
                       ↓
                    Finding
                       |
                       ↓
                  Next Stage
```

Security Engine điều phối quá trình, còn các module trong `checks/` tập trung vào việc thực hiện từng loại kiểm tra.

### 6. Luồng hoạt động tổng thể

```text
                    Managed Nodes
                         |
                         ↓
                  Security Checks
                         |
              +----------+----------+
              |                     |
              ↓                     ↓
         SSH Checks            Firewall Checks
              |                     |
              +----------+----------+
                         |
                         ↓
                      Finding
                         |
                         ↓
                Security Engine
```

Cách phân tách này giúp mỗi loại kiểm tra có một module riêng, tránh đưa toàn bộ logic kiểm tra vào một file duy nhất.

### 7. Kết quả

Sau khi xây dựng Security Checks, Python Security Engine có hai nhóm kiểm tra chính:

```text
python/checks/
│
├── ssh_checks.py
│   └── Kiểm tra SSH
│
└── firewall_checks.py
    └── Kiểm tra Firewall
```

Các module này tạo nền tảng cho quá trình phát hiện vấn đề bảo mật. Kết quả kiểm tra sẽ được chuyển sang các thành phần tiếp theo để tạo **Finding**, phân tích và xử lý.

