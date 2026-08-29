---

title : "Tạo Subnet"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.1.2 </b> "

---


### Các bước thực hiện

1. Vào giao diện **AWS Console**, tìm kiếm **Subnet** và chọn dịch vụ **VPC → Subnets**.

   ![Subnet](/images/01/image_005.png)

2. Sau khi vào giao diện Subnets, chọn **Create subnet**.

   ![Subnet](/images/01/image_001.png)

   * Đầu tiên, chọn VPC mà chúng ta đã tạo ở bước trước:

     ```text
     Automation-VPC
     ```

   ![Subnet](/images/01/image_007.png)

   * Tiếp theo, điền các thông tin trong phần **Subnet settings**:

     * **Subnet name:** `Automation-Public-Subnet`
     * **Availability Zone:** chọn `ap-southeast-1a`
     * **IPv4 VPC CIDR block:** `10.0.0.0/16`
     * **IPv4 subnet CIDR block:** `10.0.1.0/24`

     Dải `10.0.1.0/24` được sử dụng cho Public Subnet, nơi sẽ triển khai **Automation Server**.

   ![Subnet](/images/01/image_008.png)

3. Sau khi tạo thành công, **Automation-Public-Subnet** sẽ xuất hiện trong danh sách Subnets của `Automation-VPC`.

   ![Subnet](/images/01/image_009.png)

4. Tiếp tục tạo Private Subnet cho các Managed Nodes.

   Chọn **Create subnet** và sử dụng VPC:

   ```text
   Automation-VPC
   ```

   Sau đó thiết lập:

   * **Subnet name:** `Automation-Private-Subnet`
   * **Availability Zone:** `ap-southeast-1a`
   * **IPv4 VPC CIDR block:** `10.0.0.0/16`
   * **IPv4 subnet CIDR block:** `10.0.2.0/24`

   Private Subnet này sẽ được sử dụng để triển khai:

   * `Managed-Node-01`
   * `Managed-Node-02`

   ![Subnet](/images/01/image_010.png)

5. Sau khi hoàn thành, chúng ta có hai Subnet trong `Automation-VPC`:

   | Subnet                      | CIDR          | Mục đích                           |
   | --------------------------- | ------------- | ---------------------------------- |
   | `Automation-Public-Subnet`  | `10.0.1.0/24` | Automation Server                  |
   | `Automation-Private-Subnet` | `10.0.2.0/24` | Managed-Node-01 và Managed-Node-02 |

Hai Subnet này sẽ được sử dụng ở các bước tiếp theo để xây dựng kiến trúc Public/Private cho hệ thống automation.
