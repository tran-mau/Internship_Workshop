---

title : "Automation Server"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.2 </b> "

---



### Tổng quan

Trong chương này, chúng ta sẽ chuẩn bị **Automation Server** để trở thành máy chủ điều khiển của hệ thống automation. Automation Server sử dụng Ubuntu Server 24.04 LTS và được cài đặt các công cụ cần thiết như Python, Git và Ansible.

Sau khi hoàn thành chương này, Automation Server sẽ sẵn sàng để thực hiện các tác vụ automation và quản lý các Managed Nodes.

### Danh sách các bài học chi tiết

1. **6.3.1 – Chuẩn bị Automation Server**

   * Kết nối vào Automation Server
   * Kiểm tra hệ điều hành
   * Đổi hostname
   * Kiểm tra kết nối Internet
   * Cập nhật package

2. **6.3.2 – Cài đặt Python**

   * Cài đặt Python 3
   * Cài đặt pip và python3-venv
   * Tạo Python Virtual Environment
   * Kích hoạt và kiểm tra Virtual Environment

3. **6.3.3 – Cài đặt Ansible**

   * Cài đặt Ansible
   * Kiểm tra Ansible
   * Kiểm tra các command của Ansible
   * Kiểm tra `ansible-galaxy`

4. **6.3.4 – Thiết lập Project**

   * Tạo thư mục `enterprise-infrastructure-automation`
   * Tạo `.gitignore`
   * Chuẩn bị cấu trúc project cho các phần Ansible và Python

### Kiến trúc Automation Server

Sau khi hoàn thành các bước chuẩn bị, Automation Server có cấu trúc cơ bản:

```text
Automation-Server
│
├── Ubuntu Server 24.04
├── Python
├── Virtual Environment
├── Ansible
└── Git
```

Automation Server sẽ đóng vai trò **Ansible Control Node** trong các phần tiếp theo. Từ đây, Ansible sẽ được sử dụng để quản lý và tự động hóa cấu hình trên các Managed Nodes.

### Danh sách các chương thực hành: 

  + [5.2.1 Chuẩn bị Automation Server]({{< relref "5.2.1-Prepare-Automation-SV">}})  
  + [5.2.2 Install Python]({{< relref "5.2.2-Install-Python">}})  
  + [5.2.3 Install Ansible]({{< relref "5.2.3-Install-Ansible">}})  
  + [5.2.4 Thiết lập Project]({{< relref "5.2.4-Setup-Project">}})  
  + [5.2.5 Thiết lập SSH]({{< relref "5.2.5-Setup-SSH">}}) 

