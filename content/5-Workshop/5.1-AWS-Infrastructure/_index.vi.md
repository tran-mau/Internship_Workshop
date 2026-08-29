---

title : "AWS Infrastructure"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.1 </b> "

---


### Tổng quan

Trong phần này, chúng ta xây dựng hạ tầng AWS làm nền tảng cho hệ thống Enterprise Infrastructure Automation.

Môi trường được triển khai trong AWS Region **Asia Pacific (Singapore) – `ap-southeast-1`**, sử dụng một VPC riêng với hai Subnet:

* **Public Subnet**: dành cho Automation Server.
* **Private Subnet**: dành cho Managed-Node-01 và Managed-Node-02.

Kiến trúc mạng tổng quát:

```text
                         AWS VPC
                       10.0.0.0/16
                            |
              +-------------+-------------+
              |                           |
       Public Subnet               Private Subnet
        10.0.1.0/24                10.0.2.0/24
              |                           |
      Automation Server          +--------+--------+
                                 |                 |
                           Managed-Node-01   Managed-Node-02
```

<!--
Chèn hình: Sơ đồ kiến trúc AWS Infrastructure của project.
-->
  
### Danh sách các chương thực hành: 

  + [5.1.1 Tạo VPC]({{< relref "5.1.1-Create-VPC">}})  
  + [5.1.2 Tạo Subnet]({{< relref "5.1.2-Create-Subnet">}})  
  + [5.1.3 Tạo Internet Gateway]({{< relref "5.1.3-Create-Internet-Gateway">}})  
  + [5.1.4 Tạo Route Table]({{< relref "5.1.4-Create-Route-Table">}})  
  + [5.1.5 Security Group]({{< relref "5.1.5-Security-Group">}}) 
  + [5.1.6 Triển khai EC2]({{< relref "5.1.6-Deploy-EC2">}}) 
  + [5.1.7 IAM Role]({{< relref "5.1.7-IAM-Role">}}) 
  + [5.1.8 Thiết lập SSH]({{< relref "5.1.8-Setup-SSH">}}) 