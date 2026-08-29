---
title : "Cài đặt Python"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

### Các bước thực hiện

Python là một thành phần quan trọng trong hệ thống automation. Trong project, Python được sử dụng làm nền tảng cho các script và **Python Security Engine**, đồng thời Ansible cũng được xây dựng trên Python. fileciteturn22file0

## 1. Cài đặt các package Python

Trên Automation Server, chạy:

```bash
sudo apt install -y python3 python3-pip python3-venv
```

Trong đó:

- `python3`: cung cấp Python 3.
- `python3-pip`: trình quản lý package của Python.
- `python3-venv`: cung cấp công cụ tạo Python Virtual Environment.

Các package này được sử dụng để chuẩn bị môi trường Python cho project. fileciteturn22file0

## 2. Kiểm tra Python và pip

Kiểm tra phiên bản Python:

```bash
python3 --version
```

Kiểm tra pip:

```bash
pip3 --version
```

![ATSV](/images/01/image_070.png)

## 3. Tạo thư mục project

Tạo thư mục chính cho project:

```bash
mkdir -p ~/enterprise-infrastructure-automation
```

Sau đó di chuyển vào thư mục:

```bash
cd ~/enterprise-infrastructure-automation
```

Đây sẽ là thư mục làm việc chính cho các thành phần Ansible và Python của project. fileciteturn22file1

## 4. Tạo Python Virtual Environment

Không nên cài toàn bộ thư viện Python trực tiếp vào system Python. Vì vậy, project sử dụng **Virtual Environment** để tạo một môi trường Python độc lập.

Tạo môi trường ảo:

```bash
python3 -m venv .venv
```

Trong đó:

- `python3`: sử dụng Python 3.
- `-m venv`: thực thi module `venv` để tạo môi trường ảo.
- `.venv`: thư mục chứa môi trường ảo của project.


## 5. Kích hoạt Virtual Environment

Kích hoạt môi trường ảo:

```bash
source .venv/bin/activate
```

Sau khi kích hoạt, môi trường `.venv` sẽ được sử dụng thay cho Python system khi thực hiện các thao tác Python trong project.

Kiểm tra Python đang được sử dụng:

```bash
which python
```

Kiểm tra phiên bản:

```bash
python --version
```

![ATSV](/images/01/image_072.png)

## Kết quả

Sau khi hoàn thành, Automation Server có môi trường Python cơ bản:

```text
enterprise-infrastructure-automation/
│
└── .venv/
```

Python Virtual Environment giúp tách biệt các thư viện của project khỏi môi trường Python mặc định của hệ điều hành, tạo nền tảng để triển khai các thành phần Python trong các phần tiếp theo. 
