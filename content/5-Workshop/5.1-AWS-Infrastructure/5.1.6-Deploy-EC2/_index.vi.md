---

title : "Triển khai EC2"

date : "`r Sys.Date()`"

weight : 6

chapter : false

pre : " <b> 5.1.6 </b> "

---


### Các bước thực hiện

Sau khi hoàn thành VPC, Subnet, Internet Gateway, Route Table và Security Group, chúng ta tiến hành triển khai ba EC2 instance cho hệ thống:

* `Automation-Server`
* `Managed-Node-01`
* `Managed-Node-02`

Trong đó, Automation Server đóng vai trò là máy chủ điều khiển và hai Managed Nodes là các máy chủ được quản lý thông qua Ansible. Đây là kiến trúc được sử dụng trong project thực tập.

### 1. Tạo Automation Server

1. Trong **AWS Console**, chọn **EC2 → Instances → Launch instance**.

   ![EC2](/images/01/image_033.png)

2. Đặt tên cho instance:

   ```text
   Automation-Server
   ```

   ![EC2](/images/01/image_034.png)

3. Tại phần **Application and OS Images (AMI)**, chọn:

   ```text
   Ubuntu Server 24.04 LTS
   ```

   Instance type:

   ```text
   t3.micro
   ```

   Đây là cấu hình được sử dụng cho Automation Server trong project.

   ![EC2](/images/01/image_035.png)

4. Ở phần **Key pair**, chọn key pair được sử dụng cho project để có thể SSH vào Automation Server từ máy quản trị.

   ![EC2](/images/01/image_036.png)

5. Tại phần **Network settings**, cấu hình:

   * **VPC:**

     ```text
     Automation-VPC
     ```

   * **Subnet:**

     ```text
     Automation-Public-Subnet
     ```

   * **Auto-assign public IP:** `Enable`

   * **Security Group:**

     ```text
     Automation-SG
     ```

   Automation Server được đặt trong Public Subnet và có Public IP để phục vụ việc quản trị từ bên ngoài.

   ![EC2](/images/01/image_037.png)
   ![EC2](/images/01/image_038.png)

6. Sau khi kiểm tra các thông tin cấu hình, chọn **Launch instance**.

![EC2](/images/01/image_039.png)

7. Sau khi khởi tạo thành công, `Automation-Server` sẽ xuất hiện trong danh sách EC2 Instances.

   ![EC2](/images/01/image_040.png)

### 2. Tạo Managed-Node-01

1. Tiếp tục chọn **Launch instance** để tạo EC2 thứ hai.

2. Đặt tên:

   ```text
   Managed-Node-01
   ```
   ![EC2](/images/01/image_041.png)

3. Sử dụng:

   ```text
   AMI:
   Ubuntu Server 24.04 LTS

   Instance type:
   t3.micro
   ```
 ![EC2](/images/01/image_042.png)
4. Trong **Network settings**, cấu hình:

   ```text
   VPC:
   Automation-VPC

   Subnet:
   Automation-Private-Subnet

   Auto-assign public IP:
   Disable

   Security Group:
   Managed-Node-SG
   ```

   Đây là cấu hình của Managed-Node-01 trong project. Managed Node được đặt trong Private Subnet và không được cấp Public IP.

   ![EC2](/images/01/image_044.png)

5. Sau khi kiểm tra cấu hình, chọn **Launch instance**.

   ![EC2](/images/01/image_047.png)

### 3. Tạo Managed-Node-02

1. Tiếp tục chọn **Launch instance** để tạo EC2 thứ ba.

2. Đặt tên:

   ```text
   Managed-Node-02
   ```
   ![EC2](/images/01/image_048.png)

3. Sử dụng:

   ```text
   AMI:
   Ubuntu Server 24.04 LTS

   Instance type:
   t3.micro
   ```
   ![EC2](/images/01/image_049.png)
4. Trong **Network settings**, cấu hình:

   ```text
   VPC:
   Automation-VPC

   Subnet:
   Automation-Private-Subnet

   Auto-assign public IP:
   Disable

   Security Group:
   Managed-Node-SG
   ```

   Managed-Node-02 được triển khai tương tự Managed-Node-01 và nằm trong Private Subnet.

   ![EC2](/images/01/image_051.png)

5. Sau khi kiểm tra cấu hình, chọn **Launch instance**.

   ![EC2](/images/01/image_053.png)

### 4. Kiểm tra các EC2 instance

Sau khi hoàn thành, trong danh sách EC2 chúng ta sẽ có ba instance:

| Instance            | Subnet                      | Public IP | Security Group    | Vai trò              |
| ------------------- | --------------------------- | --------- | ----------------- | -------------------- |
| `Automation-Server` | `Automation-Public-Subnet`  | Enable    | `Automation-SG`   | Ansible Control Node |
| `Managed-Node-01`   | `Automation-Private-Subnet` | Disable   | `Managed-Node-SG` | Managed Node         |
| `Managed-Node-02`   | `Automation-Private-Subnet` | Disable   | `Managed-Node-SG` | Managed Node         |



Kiến trúc sau khi triển khai:

```text
                         Automation-VPC
                          10.0.0.0/16
                               |
              +----------------+----------------+
              |                                 |
       Public Subnet                     Private Subnet
        10.0.1.0/24                       10.0.2.0/24
              |                                 |
      Automation-Server             +-----------+-----------+
                                    |                       |
                              Managed-Node-01        Managed-Node-02
```

Automation Server sẽ là **Ansible Control Node** và thực hiện kết nối đến hai Managed Nodes để quản lý và tự động hóa cấu hình.

### Kết quả

Sau khi hoàn thành phần này, hạ tầng EC2 của project đã được triển khai theo đúng mô hình:

```text
Internet
    |
    ↓
Automation-Server
Public Subnet
    |
    | SSH
    ↓
Private Subnet
    ├── Managed-Node-01
    └── Managed-Node-02
```

Các EC2 instance đã sẵn sàng cho bước tiếp theo là **chuẩn bị Automation Server và cài đặt môi trường Python, Ansible**.
