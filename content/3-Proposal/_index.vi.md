---
title : "Bản đề xuất"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---


# Enterprise Infrastructure Automation & Security trên AWS

## Tự động hóa quản lý hạ tầng, kiểm tra bảo mật và khắc phục cấu hình bằng Ansible và Python

### 1. Tóm tắt điều hành

Đề xuất này trình bày giải pháp xây dựng hệ thống **tự động hóa quản lý hạ tầng và kiểm tra bảo mật** trên nền tảng AWS.

Project kết hợp ba thành phần chính:

- **AWS**: cung cấp hạ tầng Cloud gồm VPC, Subnet, EC2, Security Group và IAM Role.
- **Ansible**: thực hiện configuration management, system automation, SSH Hardening, Firewall và Security Audit trên Managed Nodes.
- **Python Security Engine**: thực hiện Security Checks, xử lý Security Finding, quản lý Security State, Reporting và hỗ trợ Automated Remediation.

Kiến trúc được xây dựng theo mô hình **Automation Server → Managed Nodes**. Automation Server đóng vai trò Ansible Control Node và chạy Python Security Engine. Các Managed Nodes được triển khai trên AWS và được quản lý tập trung thông qua SSH.

Quy trình tổng quát:

```text
Configure → Collect → Check → Detect Finding → Remediate → Verify → Report
```

---

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

- **Cấu hình thủ công**: Quản trị viên phải thực hiện lặp lại các thao tác trên từng máy chủ.
- **Không đồng nhất cấu hình**: Các Managed Nodes có thể khác nhau về SSH, Firewall hoặc cấu hình hệ thống.
- **Khó kiểm tra bảo mật liên tục**: Việc kiểm tra thủ công khó phát hiện kịp thời các cấu hình không phù hợp.
- **Khó khắc phục hàng loạt**: Việc sửa thủ công trên nhiều máy chủ mất thời gian và dễ xảy ra sai sót.
- **Thiếu khả năng theo dõi kết quả**: Kết quả kiểm tra khó được lưu trữ và so sánh nếu chỉ thực hiện trực tiếp trên terminal.

#### Giải pháp đề xuất

Project xây dựng một hệ thống tập trung trên AWS, trong đó:

1. AWS cung cấp môi trường hạ tầng và phân vùng mạng.
2. Ansible quản lý Managed Nodes thông qua Inventory, Playbooks và Roles.
3. Security Policy cung cấp các tiêu chí bảo mật.
4. Python Security Engine thực hiện Security Checks và xử lý Finding.
5. Finding được chuẩn hóa để các thành phần phía sau tiếp tục xử lý.
6. Automated Remediation được thực hiện thông qua Ansible.
7. Kết quả được lưu thành Security State và Security Reports.

#### Lợi ích

- Giảm thao tác thủ công.
- Đồng nhất cấu hình giữa các Managed Nodes.
- Tập trung hóa kiểm tra bảo mật.
- Tự động hóa phát hiện và khắc phục.
- Dễ mở rộng khi số lượng Managed Nodes tăng.
- Dễ theo dõi thông qua State và Reports.

---

### 3. Kiến trúc giải pháp

#### Sơ đồ kiến trúc tổng thể

![ASAU](/images/01/image_266.png)

#### Các thành phần chính

##### 1. AWS Infrastructure

AWS cung cấp VPC, Subnet, Internet Gateway, Route Table, EC2, Security Group và IAM Role.

##### 2. Automation Server

Automation Server là máy chủ trung tâm, chạy Ansible và Python Security Engine, đồng thời kết nối SSH tới Managed Nodes.

##### 3. Managed Nodes

Managed Nodes là các EC2 instance được Ansible quản lý, thực hiện system configuration, SSH Hardening, Firewall và Security Audit.

##### 4. Ansible Automation

```text
ansible/
├── inventory/
├── playbooks/
├── policies/
├── roles/
└── ansible.cfg
```

Ansible chịu trách nhiệm configuration management và automation execution.

##### 5. Python Security Engine

```text
python/
├── checks/
├── models/
├── security_engine/
└── reporters/
```

Python chịu trách nhiệm Security Checks, Finding, State, Reporting và Remediation.

##### 6. Output

```text
output/
├── reports/
│   ├── history/
│   └── latest.json
└── security_state/
    ├── managed-01.json
    └── managed-02.json
```

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

1. **AWS Infrastructure**
   - Xây dựng VPC và Subnet.
   - Thiết lập Route Table và Internet Gateway.
   - Triển khai EC2.
   - Cấu hình Security Group và IAM Role.

2. **Connectivity**
   - Chuẩn bị Automation Server và Managed Nodes.
   - Thiết lập SSH.
   - Kiểm tra kết nối.

3. **Ansible Automation**
   - Xây dựng Inventory.
   - Thiết lập Variables.
   - Xây dựng Playbooks và Roles.
   - Xây dựng Security Policy.
   - Thiết lập `ansible.cfg`.

4. **Security**
   - SSH Hardening.
   - Firewall.
   - Security Audit.
   - Thu thập Security State.

5. **Python Security Engine**
   - Security Checks.
   - Security Finding.
   - Security Engine.
   - Ansible Runner.
   - State và Reporting.

6. **Automated Remediation**
   - Phát hiện Finding.
   - Thực hiện remediation thông qua Ansible.
   - Verify trạng thái sau remediation.
   - Lưu State và Report.

#### Yêu cầu kỹ thuật & Bảo mật

- Kiểm soát nguồn truy cập SSH bằng Security Group.
- Sử dụng SSH Key Authentication.
- Áp dụng IAM Least Privilege.
- Tách biệt Automation Server và Managed Nodes.
- Không lưu thông tin nhạy cảm trực tiếp trong source code.
- Tách Security Policy khỏi logic xử lý.
- Lưu Security State và Reports để theo dõi kết quả.

---

### 5. Lộ trình & Mốc triển khai

```text
+------------------------------------------------------------+
| Giai đoạn 1: AWS Infrastructure                            |
| VPC → Subnet → Route Table → EC2 → SG → IAM               |
+------------------------------------------------------------+
                         |
                         v
+------------------------------------------------------------+
| Giai đoạn 2: Connectivity                                  |
| Automation Server → SSH → Managed Nodes                    |
+------------------------------------------------------------+
                         |
                         v
+------------------------------------------------------------+
| Giai đoạn 3: Ansible Automation                            |
| Inventory → Variables → Playbooks → Roles → Policies      |
+------------------------------------------------------------+
                         |
                         v
+------------------------------------------------------------+
| Giai đoạn 4: Security                                       |
| SSH Hardening → Firewall → Security Audit                  |
+------------------------------------------------------------+
                         |
                         v
+------------------------------------------------------------+
| Giai đoạn 5: Python Security Engine                        |
| Checks → Finding → Engine → Reporting                      |
+------------------------------------------------------------+
                         |
                         v
+------------------------------------------------------------+
| Giai đoạn 6: Remediation & Validation                       |
| Detect → Remediate → Verify → State / Report              |
+------------------------------------------------------------+
```

---

### 6. Ước tính ngân sách

Project được triển khai ở quy mô nhỏ phục vụ mục đích thực tập và thử nghiệm. Chi phí thực tế phụ thuộc vào Region, loại EC2, thời gian chạy, dung lượng EBS, lưu lượng mạng và các dịch vụ AWS được sử dụng.

| Thành phần | Mục đích | Chi phí phụ thuộc |
|---|---|---|
| **Amazon EC2** | Automation Server và Managed Nodes | Instance type + thời gian chạy |
| **Amazon EBS** | Lưu trữ hệ điều hành và dữ liệu | Dung lượng + loại volume |
| **Amazon VPC** | Hạ tầng mạng | Thành phần mạng được sử dụng |
| **S3** | Lưu trữ dữ liệu/report khi cần | Dung lượng + request |
| **CloudWatch** | Monitoring khi triển khai | Metrics/logs |
| **IAM** | Phân quyền AWS | Không tính phí riêng |

Có thể giảm chi phí bằng cách sử dụng instance phù hợp, dừng tài nguyên khi không sử dụng và thường xuyên theo dõi AWS Billing.

---

### 7. Đánh giá rủi ro

| Rủi ro | Mức độ | Chiến lược giảm thiểu |
|---|---|---|
| SSH không kết nối được | Cao | Kiểm tra SG, Route Table, SSH Key và SSH configuration |
| Cấu hình không đồng nhất | Trung bình | Sử dụng Inventory, Playbooks và Roles |
| Security Check sai trạng thái | Cao | Kiểm thử từng Security Check |
| Remediation sai cấu hình | Cao | Kiểm tra Policy và Verify sau remediation |
| Mất Security State | Trung bình | Lưu state theo từng Managed Node |
| Lộ SSH Private Key | Cao | Không commit key vào repository và giới hạn quyền file |
| IAM cấp quyền quá mức | Cao | Áp dụng Least Privilege |
| Chi phí AWS ngoài dự kiến | Trung bình | Theo dõi Billing và dừng tài nguyên không cần thiết |
| Python Engine lỗi | Trung bình | Tách module và kiểm thử từng component |

---

### 8. Kết quả kỳ vọng

- Xây dựng thành công môi trường AWS phục vụ automation và security management.
- Thiết lập Automation Server và Managed Nodes.
- Quản lý Managed Nodes tập trung bằng Ansible.
- Tự động hóa System Configuration, Firewall và SSH Hardening.
- Xây dựng Security Audit.
- Xây dựng Python Security Engine.
- Chuẩn hóa kết quả thông qua Security Finding.
- Lưu Security State theo từng Managed Node.
- Tạo Security Reports dưới dạng JSON và hiển thị trên Console.
- Hỗ trợ Automated Remediation thông qua Ansible.
- Hình thành quy trình:

```text
AWS Infrastructure
        ↓
Ansible Automation
        ↓
Managed Nodes
        ↓
Security Checks
        ↓
Finding
        ↓
Python Security Engine
        ↓
+---------------+---------------+
|                               |
↓                               ↓
Remediation                  Reporting
|                               |
↓                               ↓
Managed Nodes              State / Reports
```

Giá trị chính của project là xây dựng mô hình **Infrastructure Automation kết hợp Security Automation**, trong đó AWS cung cấp hạ tầng, Ansible thực hiện automation và Python đảm nhiệm logic phân tích bảo mật. Kiến trúc có thể tiếp tục mở rộng bằng cách bổ sung Managed Nodes, Security Checks, Policies và các cơ chế Reporting.

