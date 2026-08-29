---

title : "Tạo Internet Gateway"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.1.3 </b> "

---



### Các bước thực hiện

1. Trong giao diện **VPC**, chọn **Internet Gateways** và chọn **Create internet gateway**.

   ![Internet Gateway](/images/01/image_011.png)

2. Tại giao diện tạo Internet Gateway, nhập tên:

   ```text
   Automation-IGW
   ```

   Sau đó chọn **Create internet gateway**.

   ![Internet Gateway](/images/01/image_012.png)

3. Sau khi tạo thành công, chúng ta sẽ thấy **Automation-IGW** trong danh sách Internet Gateways.

   ![Internet Gateway](/images/01/image_013.png)

   Ban đầu, trạng thái (**State**) của Internet Gateway là **Detached**. Điều này có nghĩa là Internet Gateway chưa được gắn vào VPC `Automation-VPC`.

   Để sử dụng Internet Gateway, chúng ta cần attach nó vào VPC.

4. Chọn **Actions** → **Attach to a VPC**.

   ![Internet Gateway](/images/01/image_014.png)

5. Tại phần chọn VPC, chọn:

   ```text
   Automation-VPC
   ```

   Sau đó chọn **Attach internet gateway**.

   ![Internet Gateway](/images/01/image_015.png)

6. Sau khi attach thành công, trạng thái (**State**) của Internet Gateway sẽ chuyển sang **Attached**.

   Điều này cho biết `Automation-IGW` đã được gắn vào `Automation-VPC` và sẵn sàng được sử dụng trong cấu hình routing của Public Subnet.

