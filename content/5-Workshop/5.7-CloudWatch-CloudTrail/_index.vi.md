---
title : "Thiết lập CloudWatch và CloudTrail"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 5.7 </b> "
---

+ Trong chương này, chúng ta sẽ triển khai **Amazon CloudWatch** và **AWS CloudTrail** nhằm giám sát, theo dõi và kiểm tra các hoạt động diễn ra trong hệ thống AWS. Hai dịch vụ đóng vai trò quan trọng trong việc quản lý hạ tầng, phát hiện sự cố và nâng cao khả năng kiểm soát hệ thống.

+ **Amazon CloudWatch** được sử dụng để thu thập và theo dõi các chỉ số hoạt động của các tài nguyên AWS, đặc biệt là các máy chủ **EC2** trong mini project. Thông qua CloudWatch, người quản trị có thể theo dõi các thông số như mức sử dụng CPU, trạng thái của EC2 và các chỉ số liên quan đến hoạt động của máy chủ.

+ Trong mini project, CloudWatch được sử dụng để tạo **Alarm** nhằm phát hiện khi mức sử dụng CPU của EC2 vượt quá ngưỡng được thiết lập. Khi điều kiện cảnh báo xảy ra, trạng thái của Alarm sẽ thay đổi từ **OK** sang **ALARM**, giúp người quản trị nhanh chóng phát hiện các vấn đề về tài nguyên và hiệu suất của máy chủ.

+ Bên cạnh CloudWatch, **AWS CloudTrail** được sử dụng để ghi nhận và theo dõi các hoạt động được thực hiện trên tài khoản AWS thông qua các API. CloudTrail giúp xác định **ai đã thực hiện thao tác gì, thao tác được thực hiện khi nào và trên tài nguyên nào**, từ đó hỗ trợ việc kiểm tra, truy vết và đảm bảo an toàn cho hệ thống.

+ Việc kết hợp CloudWatch và CloudTrail giúp xây dựng một cơ chế giám sát và kiểm toán tương đối đầy đủ cho mini project. CloudWatch tập trung vào **tình trạng và hiệu suất của tài nguyên**, trong khi CloudTrail tập trung vào **lịch sử hoạt động và các thay đổi đối với tài nguyên AWS**.


### Danh sách các bài học chi tiết:

+ [5.7.1 Thiết lập Cloud Watch]({{< relref "5.7.1-Cloud-Watch">}})

+ [5.7.2 Thiết lập Cloud Trail]({{< relref "5.7.2-Cloud-Trail">}})
