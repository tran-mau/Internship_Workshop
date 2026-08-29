---

title : "Tạo VPC"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.1.1 </b> "

---


### Các bước thực hiện

1. Vào giao diện **AWS Console**, trên thanh tìm kiếm gõ **VPC**, sau đó chọn dịch vụ **VPC**.

   ![VPC](/images/01/image_001.png)

2. Sau khi truy cập vào dịch vụ VPC, chọn **Your VPCs** và chọn **Create VPC**.

   ![VPC](/images/01/image_002.png)

3. Sau khi chọn **Create VPC**, chúng ta sẽ có giao diện để nhập các thông tin cho VPC:

   * Ở mục **Resources to create**, chọn **VPC only** vì trong project này chúng ta muốn tự thiết lập các thành phần mạng như Subnet, Internet Gateway và Route Table.

   * Ở mục **Name tag – optional**, đặt tên là **Automation-VPC**. Đây là tên dùng để nhận diện VPC trong project.

   * Ở mục **IPv4 CIDR block**, chọn **IPv4 CIDR manual input** để tự xác định dải địa chỉ IPv4 cho VPC.

   * Ở mục **IPv4 CIDR**, nhập:

     ```text
     10.0.0.0/16
     ```

     Dải địa chỉ này được sử dụng làm không gian địa chỉ mạng cho toàn bộ hạ tầng của project.

   * Ở mục **IPv6 CIDR block**, chọn **No IPv6 CIDR block** vì project không sử dụng IPv6.

   * Ở mục **Tenancy**, chọn **Default**. Với cấu hình này, các EC2 instance sẽ sử dụng phần cứng vật lý dùng chung của AWS thay vì yêu cầu phần cứng dành riêng.

   * Sau khi hoàn tất các thông tin, chọn **Create VPC** để tạo VPC.

   ![VPC](/images/01/image_003.png)

4. Sau khi tạo thành công, VPC **Automation-VPC** sẽ xuất hiện trong danh sách VPC.

   VPC này sẽ là nền tảng để triển khai các thành phần còn lại của hệ thống, bao gồm:

   * **Automation-Public-Subnet**
   * **Automation-Private-Subnet**
   * **Automation-IGW**
   * **Automation-Public-RT**
   * **Automation-Private-RT**
   * Các EC2 instance của project

   ![VPC](/images/01/image_004.png)
