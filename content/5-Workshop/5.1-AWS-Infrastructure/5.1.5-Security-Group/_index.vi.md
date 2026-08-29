---

title : "Tạo Security Group"

date : "`r Sys.Date()`"

weight : 5

chapter : false

pre : " <b> 5.1.5 </b> "

---

### Các bước thực hiện

Trong project này, chúng ta tạo **hai Security Group riêng biệt** để kiểm soát kết nối đến Automation Server và các Managed Nodes.

Mô hình kết nối được thiết lập như sau:

```text
Internet
   |
   | SSH TCP/22
   | My IP
   ↓
Automation-Server
   |
   | SSH TCP/22
   | Source: Automation-SG
   ↓
Managed-Node-01
Managed-Node-02
```

### 1. Tạo Security Group cho Automation Server

Trong AWS Console, vào:

```text
VPC
→ Security Groups
→ Create security group
```
![SG](/images/01/image_026.png)
Tạo Security Group với các thông tin:

```text
Security group name:
Automation-SG

Description:
Security Group for Automation Server

VPC:
Automation-VPC
```
![SG](/images/01/image_027.png)


### 2. Cấu hình Inbound Rules cho Automation-SG

Automation Server nằm trong Public Subnet nên cần cho phép kết nối SSH từ máy quản trị.

Tại phần **Inbound rules**, thêm rule:

| Type | Protocol | Port | Source |
| ---- | -------- | ---: | ------ |
| SSH  | TCP      |   22 | My IP  |

Source **My IP** giúp giới hạn quyền truy cập SSH vào Automation Server từ địa chỉ IP đang sử dụng.

Outbound rule:

```text
All traffic
```

![SG](/images/01/image_028.png)

### 3. Tạo Security Group cho Managed Nodes

Tiếp tục tạo Security Group thứ hai dành cho hai Managed Nodes.

Thiết lập:

```text
Security group name:
Managed-Node-SG

VPC:
Automation-VPC
```

Managed Nodes nằm trong Private Subnet nên không mở SSH trực tiếp từ Internet.

![SG](/images/01/image_030.png)

### 4. Cấu hình Inbound Rules cho Managed-Node-SG

Tại phần **Inbound rules**, tạo rule:

| Type | Protocol | Port | Source        |
| ---- | -------- | ---: | ------------- |
| SSH  | TCP      |   22 | Automation-SG |

Ở đây, Source được thiết lập là **Security Group `Automation-SG`** thay vì một địa chỉ IP cụ thể.

Điều này cho phép các máy chủ sử dụng `Automation-SG`, cụ thể là Automation Server, kết nối SSH tới các Managed Nodes.

Outbound rule:

```text
All traffic
```

![SG](/images/01/image_031.png)

### 5. Kết quả

Sau khi hoàn thành, project có hai Security Group:

| Security Group    | Đối tượng          | Inbound SSH             |
| ----------------- | ------------------ | ----------------------- |
| `Automation-SG`   | Automation Server  | TCP 22 từ My IP         |
| `Managed-Node-SG` | Managed-Node-01/02 | TCP 22 từ Automation-SG |

Luồng kết nối được kiểm soát:

```text
             My IP
               |
            TCP/22
               ↓
      +------------------+
      | Automation-SG    |
      | Automation-Server|
      +------------------+
               |
            TCP/22
               |
      Source: Automation-SG
               ↓
       +---------------+
       | Managed-Node- |
       | 01 / 02       |
       +---------------+
```

Với cấu hình này, Automation Server có thể được truy cập SSH từ máy quản trị, trong khi Managed Nodes chỉ cho phép SSH từ Automation Server thông qua `Automation-SG`.

Cấu hình Security Group này sẽ được sử dụng ở các bước triển khai EC2 và thiết lập SSH giữa Automation Server với Managed Nodes.
