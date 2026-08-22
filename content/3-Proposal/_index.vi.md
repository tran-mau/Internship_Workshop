---
title : "Bản đề xuất"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

# Thiết kế hạ tầng Cloud AWS an toàn, giám sát tập trung và tối ưu chi phí cho hệ thống doanh nghiệp vừa và nhỏ

## Kiến trúc hạ tầng Cloud tích hợp bảo mật, giám sát và quản trị tập trung trên AWS

### 1. Tóm tắt điều hành

Đề xuất này trình bày giải pháp thiết kế và triển khai một hạ tầng Cloud trên Amazon Web Services (AWS) dành cho các hệ thống doanh nghiệp vừa và nhỏ, tập trung giải quyết ba vấn đề quan trọng trong quá trình chuyển đổi lên Cloud: **an toàn mạng, khả năng giám sát và kiểm soát chi phí vận hành**.

Trong thực tế, nhiều doanh nghiệp triển khai máy chủ trên Cloud theo hướng đưa trực tiếp các tài nguyên như EC2 ra Internet để thuận tiện truy cập. Tuy nhiên, việc phân quyền chưa chặt chẽ, mở các cổng dịch vụ không cần thiết, sử dụng tài khoản có quyền quá lớn hoặc thiếu cơ chế giám sát tập trung có thể tạo ra các điểm yếu bảo mật.

Bên cạnh đó, các tài nguyên Cloud như EC2, NAT Gateway, Load Balancer và Data Transfer có thể phát sinh chi phí ngay cả khi hệ thống chưa được sử dụng với công suất cao. Nếu không có cơ chế theo dõi và tối ưu, doanh nghiệp rất khó xác định nguyên nhân khiến chi phí tăng.

Giải pháp đề xuất xây dựng mô hình hạ tầng AWS theo nguyên tắc **Defense in Depth**, phân tách hệ thống thành Public Subnet và Private Subnet, kiểm soát truy cập thông qua Security Group và IAM, hạn chế việc truy cập trực tiếp từ Internet đến các máy chủ nội bộ.

Hệ thống đồng thời sử dụng **Amazon CloudWatch** để giám sát tài nguyên và hiệu năng, **AWS CloudTrail** để ghi nhận hoạt động API và hành vi quản trị, **AWS Systems Manager (SSM)** để quản lý EC2 mà hạn chế phụ thuộc vào SSH công khai, cùng với **Amazon S3** để lưu trữ dữ liệu và log.

Mục tiêu của đề xuất là xây dựng một mô hình Cloud có thể **triển khai thực tế, dễ giám sát, có khả năng mở rộng và kiểm soát được chi phí**, đồng thời có thể sử dụng làm kiến trúc tham khảo cho các hệ thống doanh nghiệp nhỏ và vừa.

---

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

**1. Nguy cơ mất an toàn do cấu hình Cloud sai**

Khi triển khai hệ thống trên Cloud, một trong những rủi ro phổ biến là cấu hình sai tài nguyên mạng hoặc quyền truy cập. Ví dụ, EC2 có thể được cấp Public IP và mở cổng SSH trực tiếp ra Internet. Nếu Security Group cho phép truy cập quá rộng như `0.0.0.0/0`, máy chủ có thể trở thành mục tiêu của các hoạt động dò quét và tấn công tự động.

**2. Khó kiểm soát quyền truy cập**

Việc sử dụng tài khoản IAM với quyền quá lớn hoặc sử dụng Access Key trực tiếp trên máy chủ làm tăng nguy cơ lộ thông tin xác thực.

Do đó, cần áp dụng nguyên tắc **Least Privilege**, trong đó mỗi người dùng và tài nguyên chỉ được cấp quyền cần thiết để thực hiện nhiệm vụ của mình.

**3. Thiếu khả năng giám sát tập trung**

Nếu chỉ sử dụng SSH để đăng nhập và kiểm tra máy chủ thủ công, quản trị viên khó phát hiện các vấn đề như CPU tăng cao, bộ nhớ gần đầy, tiến trình bất thường hoặc hoạt động truy cập không hợp lệ.

Hệ thống cần có cơ chế thu thập metric, log và cảnh báo tập trung.

**4. Khó truy vết các hoạt động quản trị**

Trong môi trường Cloud, có nhiều hoạt động được thực hiện thông qua AWS Management Console, CLI hoặc API. Nếu không bật cơ chế ghi nhận lịch sử API, rất khó xác định ai đã thực hiện một thay đổi, thay đổi tài nguyên nào và thay đổi vào thời điểm nào.

**5. Chi phí Cloud khó kiểm soát**

Các tài nguyên như EC2, NAT Gateway, Load Balancer và Data Transfer có thể phát sinh chi phí. Việc triển khai nhiều tài nguyên phục vụ thử nghiệm nhưng không xóa hoặc tắt đúng cách có thể khiến chi phí tăng nhanh.

Vì vậy, cần xây dựng hệ thống ngay từ đầu với nguyên tắc **Cost Awareness**, theo dõi mức sử dụng và xác định những tài nguyên tạo ra chi phí.

---

### Giải pháp đề xuất

Hệ thống được thiết kế theo mô hình **Secure, Monitorable and Cost-Optimized Cloud Infrastructure**.

Kiến trúc được chia thành các lớp:

1. **Network Layer** – VPC, Public Subnet, Private Subnet, Internet Gateway và NAT Gateway.
2. **Compute Layer** – EC2 phục vụ ứng dụng và các tác vụ quản trị.
3. **Security Layer** – IAM, Security Group và phân quyền theo nguyên tắc Least Privilege.
4. **Management Layer** – AWS Systems Manager giúp quản lý EC2.
5. **Monitoring Layer** – Amazon CloudWatch giám sát metric, log và cảnh báo.
6. **Audit Layer** – AWS CloudTrail ghi nhận các hoạt động API.
7. **Storage Layer** – Amazon S3 lưu trữ dữ liệu và các đối tượng cần thiết.
8. **Application Access Layer** – có thể mở rộng với Application Load Balancer khi hệ thống cần phân phối lưu lượng.

Các máy chủ có yêu cầu tiếp nhận Internet được đặt trong Public Subnet hoặc được truy cập thông qua tầng trung gian phù hợp. Những thành phần không cần nhận kết nối trực tiếp từ Internet được đặt trong Private Subnet.

Security Group được cấu hình theo nguyên tắc chỉ cho phép các luồng giao tiếp thực sự cần thiết.

Đối với hoạt động quản trị EC2, AWS Systems Manager được sử dụng để giảm sự phụ thuộc vào SSH trực tiếp từ Internet.

Amazon CloudWatch được sử dụng để theo dõi trạng thái hệ thống và tạo cảnh báo khi tài nguyên vượt ngưỡng.

AWS CloudTrail được sử dụng để ghi lại hoạt động quản trị và API nhằm hỗ trợ kiểm toán và điều tra sự cố.

---

## 3. Kiến trúc giải pháp

### 3.1. Mô hình tổng thể

```text
                         INTERNET
                             |
                             v
                    +----------------+
                    | Internet       |
                    | Gateway        |
                    +-------+--------+
                            |
                 +----------+----------+
                 |         VPC          |
                 |                     |
        +--------v--------+   +--------v--------+
        | Public Subnet   |   | Private Subnet  |
        |                 |   |                 |
        | EC2 / ALB       |   | Private EC2     |
        |                 |   | Application     |
        +--------+--------+   +--------+--------+
                 |                     |
                 |                     |
                 +----------+----------+
                            |
                     +------v------+
                     | NAT Gateway |
                     +-------------+

       IAM / SSM / CloudWatch / CloudTrail / S3
                         |
                         v
                AWS Management Layer
```

Kiến trúc được thiết kế nhằm tách biệt giữa **luồng truy cập Internet**, **luồng ứng dụng nội bộ** và **luồng quản trị/giám sát**.

### 3.2. Luồng A – Network & Traffic Flow

Người dùng từ Internet gửi request đến hệ thống thông qua Public Subnet.

Internet Gateway đóng vai trò kết nối giữa VPC và Internet.

Các tài nguyên cần phục vụ trực tiếp Internet được đặt trong Public Subnet.

Các máy chủ không cần Public IP được đặt trong Private Subnet.

Khi Private EC2 cần truy cập Internet để cập nhật package hoặc tải dữ liệu cần thiết, lưu lượng được định tuyến thông qua NAT Gateway.

Security Group kiểm soát traffic giữa các thành phần theo nguyên tắc:

- Chỉ mở các port cần thiết.
- Không mở SSH cho toàn bộ Internet.
- Chỉ cho phép Private EC2 nhận traffic từ nguồn hợp lệ.
- Chỉ cho phép các server giao tiếp với nhau khi thực sự cần thiết.

### 3.3. Luồng B – EC2 Management với AWS Systems Manager

Quản trị viên không cần phải mở cổng SSH công khai cho tất cả Internet.

EC2 được gắn IAM Role phù hợp để có thể hoạt động với AWS Systems Manager.

Quản trị viên sử dụng SSM để:

- Truy cập EC2.
- Kiểm tra trạng thái máy chủ.
- Thực hiện lệnh quản trị.
- Thu thập thông tin hệ thống.
- Quản lý máy chủ từ AWS Console.

Cách tiếp cận này giúp giảm bề mặt tấn công của máy chủ và hạn chế nhu cầu duy trì cổng SSH công khai.

### 3.4. Luồng C – Monitoring với Amazon CloudWatch

Amazon CloudWatch thu thập các thông tin giám sát từ hệ thống.

Các metric quan trọng bao gồm:

- CPU Utilization.
- Network In/Out.
- Disk usage thông qua CloudWatch Agent khi cần.
- Trạng thái EC2.
- Log của ứng dụng.
- Các chỉ số liên quan đến dịch vụ AWS.

Quản trị viên có thể thiết lập CloudWatch Alarm để phát hiện các tình huống bất thường.

```text
CPU > 80%
      |
      v
CloudWatch Alarm
      |
      v
Cảnh báo quản trị viên
      |
      v
Kiểm tra EC2 / Application
```

Điều này giúp chuyển từ mô hình **phát hiện sự cố thủ công** sang mô hình **giám sát chủ động**.

### 3.5. Luồng D – Audit với AWS CloudTrail

AWS CloudTrail ghi lại các hoạt động API trong tài khoản AWS.

Ví dụ:

- Tạo hoặc xóa EC2.
- Thay đổi Security Group.
- Thay đổi IAM Policy.
- Tạo hoặc xóa S3 Bucket.
- Thay đổi cấu hình các dịch vụ AWS.

Thông qua CloudTrail, quản trị viên có thể xác định:

- Ai thực hiện hành động.
- Thời gian thực hiện.
- API nào được gọi.
- Tài nguyên nào bị tác động.

CloudTrail đóng vai trò quan trọng trong việc điều tra sự cố và kiểm toán hệ thống.

### 3.6. Luồng E – Storage với Amazon S3

Amazon S3 được sử dụng làm tầng lưu trữ đối tượng của hệ thống.

Các trường hợp sử dụng bao gồm:

- Lưu trữ file.
- Lưu trữ dữ liệu backup.
- Lưu trữ log.
- Lưu trữ các file triển khai.
- Lưu trữ dữ liệu phục vụ ứng dụng.

Bucket được cấu hình theo nguyên tắc hạn chế Public Access và chỉ cấp quyền IAM cần thiết cho các tài nguyên có nhu cầu truy cập.

---

## 4. Các dịch vụ AWS sử dụng

| Dịch vụ | Vai trò |
|---|---|
| Amazon VPC | Xây dựng mạng Cloud riêng |
| Public/Private Subnet | Phân tách tài nguyên theo mức độ truy cập |
| Internet Gateway | Kết nối Public Subnet với Internet |
| NAT Gateway | Cho Private Subnet truy cập Internet outbound |
| Amazon EC2 | Chạy máy chủ ứng dụng |
| Security Group | Kiểm soát lưu lượng mạng |
| IAM | Quản lý danh tính và quyền truy cập |
| AWS Systems Manager | Quản lý EC2 từ xa |
| Amazon CloudWatch | Giám sát metric, log và cảnh báo |
| AWS CloudTrail | Audit và ghi nhận hoạt động API |
| Amazon S3 | Lưu trữ dữ liệu và file |
| Application Load Balancer | Phân phối traffic khi hệ thống mở rộng |

---

## 5. Triển khai kỹ thuật

### Giai đoạn 1: Thiết kế VPC và Network

- Tạo VPC.
- Xây dựng Public Subnet và Private Subnet.
- Cấu hình Route Table.
- Cấu hình Internet Gateway.
- Triển khai NAT Gateway khi cần.
- Thiết kế Security Group.

Mục tiêu của giai đoạn này là tạo nền tảng mạng có khả năng phân tách rõ ràng giữa tài nguyên công khai và tài nguyên nội bộ.

### Giai đoạn 2: Triển khai EC2

- Tạo Public EC2.
- Tạo Private EC2.
- Cấu hình IAM Role cho EC2.
- Kiểm tra kết nối giữa các máy chủ.
- Kiểm tra kết nối Internet outbound từ Private EC2.

### Giai đoạn 3: Triển khai quản trị tập trung

- Cấu hình AWS Systems Manager.
- Kiểm tra EC2 xuất hiện trong Systems Manager.
- Thực hiện quản trị máy chủ thông qua SSM.
- Hạn chế việc mở SSH trực tiếp ra Internet.

### Giai đoạn 4: Triển khai CloudWatch

- Cấu hình CloudWatch.
- Thu thập metric EC2.
- Cài đặt CloudWatch Agent khi cần.
- Thu thập log.
- Tạo Dashboard.
- Tạo CloudWatch Alarm.
- Kiểm thử cảnh báo bằng cách tạo tải trên EC2.

### Giai đoạn 5: Triển khai CloudTrail

- Bật CloudTrail.
- Cấu hình lưu trữ log.
- Theo dõi các hoạt động API.
- Thực hiện một số thao tác thay đổi tài nguyên để kiểm tra audit log.
- Phân tích các sự kiện đáng chú ý.

### Giai đoạn 6: Triển khai S3 và bảo mật dữ liệu

- Tạo S3 Bucket.
- Tắt Public Access không cần thiết.
- Cấu hình IAM Policy.
- Kiểm tra quyền truy cập.
- Kiểm thử upload/download dữ liệu.

### Giai đoạn 7: Kiểm thử và tối ưu chi phí

Tiến hành kiểm thử:

- Kiểm thử kết nối Public → Private.
- Kiểm thử Security Group.
- Kiểm thử SSM.
- Kiểm thử CloudWatch Alarm.
- Kiểm thử CloudTrail.
- Kiểm thử quyền IAM.
- Kiểm tra khả năng truy cập S3.
- Kiểm tra chi phí phát sinh của EC2, NAT Gateway và các tài nguyên khác.

---

## 6. Yêu cầu kỹ thuật và bảo mật

### 6.1. Nguyên tắc Least Privilege

IAM Role và Policy chỉ được cấp những quyền cần thiết.

Không sử dụng quyền Administrator cho các tài nguyên chỉ cần thực hiện một số thao tác cụ thể.

### 6.2. Phân tách Public và Private

Các tài nguyên không cần truy cập trực tiếp từ Internet phải được đặt trong Private Subnet.

Private EC2 không sử dụng Public IP nếu không có yêu cầu đặc biệt.

### 6.3. Security Group

Security Group được cấu hình theo nguyên tắc:

```text
Internet
   |
   | Chỉ port cần thiết
   v
Public Layer
   |
   | Chỉ traffic hợp lệ
   v
Private Layer
```

Không mở toàn bộ port cho Internet.

Đặc biệt hạn chế:

```text
SSH 22 -> 0.0.0.0/0
```

Thay vào đó có thể sử dụng SSM hoặc giới hạn nguồn truy cập cụ thể.

### 6.4. Giám sát chủ động

CloudWatch được sử dụng để phát hiện:

- CPU tăng bất thường.
- Network traffic tăng đột biến.
- Disk gần đầy.
- Instance gặp vấn đề.
- Application log xuất hiện lỗi.

### 6.5. Audit và truy vết

CloudTrail giúp xây dựng lịch sử hoạt động của tài khoản AWS.

Khi xảy ra sự cố, quản trị viên có thể sử dụng CloudTrail để xác định nguyên nhân và hành động đã xảy ra.

---

## 7. Lộ trình triển khai

```text
+---------------------------------------------------------------+
| Giai đoạn 1: Thiết kế Network                                 |
| - VPC, Subnet, Route Table                                    |
| - Internet Gateway, NAT Gateway                              |
| - Security Group                                               |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Giai đoạn 2: Triển khai Compute                               |
| - Public EC2                                                  |
| - Private EC2                                                 |
| - IAM Role                                                    |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Giai đoạn 3: Quản trị tập trung                               |
| - AWS Systems Manager                                         |
| - Quản lý EC2                                                 |
| - Hạn chế SSH công khai                                       |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Giai đoạn 4: Monitoring & Audit                               |
| - CloudWatch                                                  |
| - CloudWatch Agent                                            |
| - CloudTrail                                                   |
| - Alarm & Dashboard                                           |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Giai đoạn 5: Storage & Security                               |
| - Amazon S3                                                   |
| - IAM Policy                                                  |
| - Kiểm soát Public Access                                     |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Giai đoạn 6: Kiểm thử & Cost Optimization                     |
| - Security Testing                                            |
| - Load Testing                                                |
| - Monitoring Testing                                          |
| - Kiểm tra và tối ưu chi phí                                  |
+---------------------------------------------------------------+
```

---

## 8. Ước tính chi phí

Giải pháp được thiết kế theo nguyên tắc **Pay-as-you-go**, chỉ sử dụng các tài nguyên cần thiết.

Các thành phần cần đặc biệt theo dõi chi phí:

- Amazon EC2.
- NAT Gateway.
- Application Load Balancer.
- Data Transfer.
- EBS Volume.
- Amazon S3.
- CloudWatch.
- CloudTrail.

Trong môi trường học tập và thử nghiệm, có thể giảm chi phí bằng cách:

1. Sử dụng EC2 kích thước nhỏ phù hợp với workload.
2. Stop hoặc terminate các EC2 không sử dụng.
3. Xóa EBS Volume và Elastic IP không còn cần thiết.
4. Không duy trì NAT Gateway khi không thực sự cần thiết.
5. Không triển khai ALB nếu chưa có nhu cầu cân bằng tải.
6. Kiểm tra Cost Explorer thường xuyên.
7. Sử dụng Budget/Cost Alert để cảnh báo khi chi phí vượt ngưỡng.

Điểm quan trọng của đề tài không chỉ là xây dựng hệ thống chạy được mà còn phải chứng minh khả năng **kiểm soát và tối ưu chi phí Cloud**.

---

## 9. Đánh giá rủi ro

| Rủi ro | Mức độ ảnh hưởng | Xác suất | Chiến lược giảm thiểu |
|---|---|---|---|
| Security Group mở quá rộng | Cao | Trung bình | Áp dụng Least Privilege và giới hạn nguồn |
| Lộ thông tin IAM | Cao | Thấp | Sử dụng IAM Role, hạn chế Access Key |
| EC2 bị tấn công từ Internet | Cao | Trung bình | Private Subnet, SSM, giới hạn Security Group |
| Không phát hiện sự cố kịp thời | Cao | Trung bình | CloudWatch Alarm và Dashboard |
| Không truy vết được hoạt động | Cao | Thấp | Sử dụng CloudTrail |
| Chi phí Cloud tăng bất thường | Trung bình | Cao | Cost monitoring và Budget Alert |
| NAT Gateway phát sinh chi phí cao | Trung bình | Cao | Chỉ sử dụng khi cần thiết |
| EC2 chạy khi không sử dụng | Trung bình | Cao | Stop/Terminate và tự động hóa quản lý |

---

## 10. Kết quả kỳ vọng

### 10.1. Về kỹ thuật

Xây dựng thành công một hạ tầng Cloud AWS có khả năng:

- Phân tách Public Subnet và Private Subnet.
- Triển khai EC2 an toàn.
- Kiểm soát traffic bằng Security Group.
- Quản lý EC2 thông qua AWS Systems Manager.
- Giám sát hệ thống bằng CloudWatch.
- Theo dõi hoạt động quản trị bằng CloudTrail.
- Lưu trữ dữ liệu trên Amazon S3.
- Áp dụng IAM theo nguyên tắc Least Privilege.

### 10.2. Về bảo mật

Giảm bề mặt tấn công của hệ thống bằng cách hạn chế các dịch vụ công khai, giảm phụ thuộc vào SSH và kiểm soát chặt chẽ quyền truy cập.

Hệ thống đồng thời có khả năng phát hiện và truy vết các sự kiện bất thường thông qua CloudWatch và CloudTrail.

### 10.3. Về vận hành

Quản trị viên có thể theo dõi tình trạng hệ thống từ một môi trường tập trung thay vì phải kiểm tra từng EC2 thủ công.

CloudWatch cung cấp khả năng giám sát và cảnh báo, trong khi Systems Manager hỗ trợ quản trị máy chủ.

### 10.4. Về chi phí

Đề tài hướng tới việc chứng minh rằng việc thiết kế kiến trúc ngay từ đầu có ảnh hưởng trực tiếp đến chi phí Cloud.

Thông qua việc lựa chọn Public/Private Subnet, kiểm soát NAT Gateway, EC2, EBS, Load Balancer và Data Transfer, hệ thống có thể hạn chế những khoản chi phí không cần thiết.

### 10.5. Giá trị mở rộng

Kiến trúc có thể tiếp tục mở rộng trong tương lai bằng:

- Application Load Balancer.
- Auto Scaling Group.
- Amazon RDS.
- AWS Lambda.
- Amazon DynamoDB.
- AWS WAF.
- CloudFront.
- Infrastructure as Code với Terraform hoặc AWS CloudFormation.
- CI/CD Pipeline.

Qua đó, mô hình có thể phát triển từ một hệ thống Cloud thử nghiệm thành nền tảng hạ tầng phục vụ các ứng dụng doanh nghiệp thực tế.
