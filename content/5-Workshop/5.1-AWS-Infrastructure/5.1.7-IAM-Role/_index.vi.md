---

title : "Tạo IAM Role cho Automation Server"

date : "`r Sys.Date()`"

weight : 7

chapter : false

pre : " <b> 5.1.7 </b> "

---


### Các bước thực hiện

Trong project này, **Automation Server** cần tương tác với các dịch vụ của AWS. Vì vậy, chúng ta tạo một **IAM Role** để cấp quyền cho Automation Server.



### 1. Truy cập IAM

Trong **AWS Console**, tìm kiếm **IAM** và chọn dịch vụ **IAM**.

![IAM](/images/01/image_054.png)

### 2. Tạo IAM Role

Trong giao diện IAM, chọn:

```text
Roles
→ Create role
```

3. Tại giao diện tạo Role, lựa chọn loại Trusted Entity phù hợp để EC2 có thể sử dụng IAM Role.

![IAM](/images/01/image_055.png)

4. Tiếp theo, cấu hình các quyền (**Permissions**) cần thiết cho Automation Server.

   Các quyền được cấp cần phù hợp với những dịch vụ AWS mà Automation Server sử dụng trong project.

![IAM](/images/01/image_057.png)

5. Đặt tên cho IAM Role theo cấu hình thực tế của project và chọn **Create role**.

   ```text
   Role name:
   <Automation-Server-Role>
   ```

   ![IAM](/images/01/image_058.png)

### 3. Gán IAM Role cho Automation Server

Sau khi tạo IAM Role, quay lại giao diện EC2:

```text
EC2
→ Instances
→ Automation-Server
```

Chọn:

```text
Actions
→ Security
→ Modify IAM role
```


6. Tại phần **IAM role**, chọn Role vừa tạo và chọn **Update IAM role**.

 