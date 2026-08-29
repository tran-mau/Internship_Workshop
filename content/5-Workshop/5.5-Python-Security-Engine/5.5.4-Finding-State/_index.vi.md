---
title : "Finding và State"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.5.4 </b> "
---

### Tổng quan

Sau khi Security Checks thực hiện kiểm tra, kết quả cần được biểu diễn dưới một cấu trúc dữ liệu thống nhất để Security Engine có thể tiếp tục xử lý.

Trong project, phần này được tổ chức trong:

```text
python/
├── models/
│   └── finding.py
│
└── state_loader.py
```

`finding.py` tập trung vào mô hình **Security Finding**, trong khi `state_loader.py` hỗ trợ việc đọc hoặc xử lý trạng thái bảo mật được lưu lại.


### 1. Security Finding

File:

```text
python/models/finding.py
```

được sử dụng để định nghĩa cấu trúc dữ liệu của một **Finding**.

Finding đại diện cho một kết quả được phát hiện trong quá trình kiểm tra bảo mật.

Luồng tổng quát:

```text
Security Check
      |
      ↓
   Finding
      |
      ↓
Security Engine
```

![ASAU](/images/01/image_248.png)

### 2. Vai trò của Finding

Finding giúp chuẩn hóa kết quả từ nhiều loại Security Checks khác nhau.

Ví dụ về luồng:

```text
SSH Check
    |
    ↓
 Finding
    ↑
    |
Firewall Check
```

Thay vì mỗi module trả về một dạng dữ liệu khác nhau, các kết quả có thể được biểu diễn thông qua model Finding để những thành phần phía sau xử lý thống nhất.



### 3. State

Bên cạnh Finding, project có:

```text
python/state_loader.py
```

Thành phần này liên quan đến việc xử lý trạng thái bảo mật của hệ thống.

Project cũng lưu trạng thái trong thư mục:

```text
output/security_state/
├── managed-01.json
└── managed-02.json
```

Các file state tương ứng với từng Managed Node.

![ASAU](/images/01/image_249.png)

### 4. state_loader.py

File:

```text
python/state_loader.py
```

được sử dụng để làm việc với dữ liệu trạng thái được lưu trong hệ thống.

Luồng tổng quát:

```text
Security State
      |
      ↓
state_loader.py
      |
      ↓
Python Security Engine
```

![ASAU](/images/01/image_250.png)



### 5. Finding và Security State

Finding và State phục vụ hai mục đích khác nhau:

```text
Finding
  ↓
Kết quả / vấn đề được phát hiện

State
  ↓
Trạng thái được lưu lại của Managed Node
```

Có thể hình dung mối quan hệ:

```text
Managed Node
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
Security State
```

Finding phản ánh kết quả kiểm tra, còn State giúp hệ thống lưu giữ thông tin trạng thái để phục vụ các bước xử lý tiếp theo.

### 6. Liên kết với Output

Các trạng thái của Managed Nodes được lưu trong:

```text
output/security_state/
├── managed-01.json
└── managed-02.json
```

Ngoài ra, kết quả của hệ thống còn được lưu trong:

```text
output/reports/
├── history/
└── latest.json
```

Do đó, dữ liệu bảo mật có thể được tổ chức theo hai hướng:

```text
Python Security Engine
        |
        +── Security State
        |       ↓
        |   security_state/
        |
        └── Report
                ↓
             reports/
```

![ASAU](/images/01/image_251.png)
![ASAU](/images/01/image_252.png)

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
                 +-----+-----+
                 |           |
                 ↓           ↓
              State       Report
                 |           |
                 ↓           ↓
        security_state/   reports/
```

Security Checks tạo Finding, Security Engine xử lý các kết quả và hệ thống lưu trạng thái hoặc tạo báo cáo tương ứng.

### Kết quả

Sau khi hoàn thành phần Finding và State, project có cơ chế chuẩn hóa và lưu trữ kết quả bảo mật:

```text
Security Check
      ↓
   Finding
      ↓
Security Engine
      ↓
+-----+------+
|            |
↓            ↓
State       Report
```

Cách tổ chức này giúp kết quả bảo mật có thể được sử dụng tiếp cho **Reporting** và **Automated Remediation**.


