---

title : "Tạo Route Table"

date : "`r Sys.Date()`"

weight : 4

chapter : false

pre : " <b> 5.1.4 </b> "

---



### Các bước thực hiện

1. Vào **VPC → Route Tables** và chọn **Create route table**.

   ![Route Table](/images/01/image_017.png)

2. Đặt tên cho Route Table và chọn VPC của project:

   ```text
   Name:
   Automation-Public-RT

   VPC:
   Automation-VPC
   ```

   Sau đó chọn **Create route table**.

   ![Route Table](/images/01/image_018.png)

3. Đây là giao diện của **Automation-Public-RT** sau khi tạo thành công.

   ![Route Table](/images/01/image_019.png)

4. Tiếp theo, chúng ta sẽ cấu hình route Internet cho Public Route Table.

   Chọn tab **Routes** và chọn **Edit routes**.

   ![Route Table](/images/01/image_020.png)

5. Trong giao diện **Edit routes**, chọn **Add route**.


6. Cấu hình route:

   * **Destination:**

     ```text
     0.0.0.0/0
     ```

   * **Target:** chọn **Internet Gateway** và chọn:

     ```text
     Automation-IGW
     ```

   Route `0.0.0.0/0` có nghĩa là các gói tin đi tới những mạng không thuộc các route cụ thể khác sẽ được gửi tới Internet Gateway.

   Sau đó chọn **Save changes**.

   ![Route Table](/images/01/image_021.png)

7. Tiếp theo, chúng ta sẽ Associate Route Table với **Public Subnet**.

   Trong **Automation-Public-RT**, chuyển sang tab **Subnet associations** và chọn **Edit subnet associations**.

   ![Route Table](/images/01/image_022.png)

8. Chọn:

   ```text
   Automation-Public-Subnet
   ```

   Sau đó chọn **Save associations**.

   ![Route Table](/images/01/image_023.png)

9. Sau khi Associate thành công, **Automation-Public-RT** sẽ được liên kết với **Automation-Public-Subnet**.

   ![Route Table](/images/01/image_024.png)

10. Tiếp theo, tạo Route Table dành cho Private Subnet.

    Đặt tên:

    ```text
    Automation-Private-RT
    ```

    Chọn VPC:

    ```text
    Automation-VPC
    ```

    Sau đó Associate Route Table này với:

    ```text
    Automation-Private-Subnet
    ```

    ![Route Table](/images/01/image_025.png)

Sau khi hoàn thành, hệ thống có hai Route Table:

| Route Table             | Subnet Association          | Mục đích                      |
| ----------------------- | --------------------------- | ----------------------------- |
| `Automation-Public-RT`  | `Automation-Public-Subnet`  | Routing cho Automation Server |
| `Automation-Private-RT` | `Automation-Private-Subnet` | Routing cho Managed Nodes     |

