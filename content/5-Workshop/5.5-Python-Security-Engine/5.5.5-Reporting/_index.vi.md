---
title : "Reporting"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5.5.5 </b> "
---

### Tổng quan

Sau khi Security Checks thực hiện kiểm tra và Security Engine xử lý các Finding, project cần thành phần để đưa kết quả ra cho người sử dụng.

Chức năng **Reporting** được tổ chức trong:

```text
python/reporters/
├── console.py
└── json_reporter.py
```

Kết quả được lưu trong:

```text
output/reports/
├── history/
└── latest.json
```
![ASAU](/images/01/image_253.png)

### 1. Vai trò của Reporting

Reporting là lớp đưa kết quả từ Security Engine ra bên ngoài.

```text
Security Checks
       |
       ↓
    Finding
       |
       ↓
Security Engine
       |
       ↓
   Reporting
    /     \
   ↓       ↓
Console    JSON
```

Kết quả có thể được hiển thị trực tiếp trên console hoặc lưu dưới dạng JSON.

### 2. console.py

File:

```text
python/reporters/console.py
```

được sử dụng để hiển thị kết quả Security Engine trên terminal.

```text
Security Engine
      |
      ↓
  console.py
      |
      ↓
   Terminal
```

![ASAU](/images/01/image_254.png)
![ASAU](/images/01/image_255.png)
![ASAU](/images/01/image_256.png)

### 3. json_reporter.py

File:

```text
python/reporters/json_reporter.py
```

được sử dụng để xuất kết quả dưới dạng **JSON**.

```text
Finding / Result
      |
      ↓
json_reporter.py
      |
      ↓
JSON Report
```

![ASAU](/images/01/image_257.png)
![ASAU](/images/01/image_258.png)
![ASAU](/images/01/image_259.png)
![ASAU](/images/01/image_260.png)

### 4. latest.json

Project lưu báo cáo hiện tại tại:

```text
output/reports/latest.json
```

File này đại diện cho kết quả báo cáo mới nhất.

```text
Security Engine
      |
      ↓
json_reporter.py
      |
      ↓
latest.json
```

![ASAU](/images/01/image_251.png)

### 5. History

Project có thư mục:

```text
output/reports/history/
```

để lưu các báo cáo trước đó.

```text
output/reports/
│
├── latest.json
│
└── history/
    └── Previous Reports
```

![ASAU](/images/01/image_261.png)

### 6. Console và JSON Reporting

Hai Reporter có vai trò khác nhau:

| Reporter | Mục đích |
|---|---|
| `console.py` | Hiển thị kết quả trên terminal |
| `json_reporter.py` | Xuất kết quả thành JSON |

Luồng:

```text
                    Finding
                       |
                       ↓
                 Security Engine
                       |
                 +-----+-----+
                 |           |
                 ↓           ↓
            console.py   json_reporter.py
                 |           |
                 ↓           ↓
             Terminal    latest.json
                              |
                              ↓
                         history/
```

### 7. Luồng Reporting tổng thể

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
Reporters
   /       \
  ↓         ↓
Console     JSON
  |           |
  ↓           ↓
Terminal   latest.json
              |
              ↓
           history/
```

Reporting là bước chuyển kết quả nội bộ của Python Security Engine thành dữ liệu mà người dùng có thể quan sát hoặc lưu trữ.

### Kết quả

Sau khi hoàn thành Reporting, project có thể cung cấp kết quả theo hai dạng:

```text
Python Security Engine
          |
          ↓
       Finding
          |
          ↓
      Reporting
       /     \
      ↓       ↓
 Console     JSON
    |          |
    ↓          ↓
Terminal   latest.json
               |
               ↓
            history/
```

Cấu trúc này giúp kết quả bảo mật vừa có thể **hiển thị trực tiếp**, vừa có thể **lưu trữ dưới dạng dữ liệu có cấu trúc**.

