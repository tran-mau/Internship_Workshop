---

title : "Ansible Inventory"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.3.2 </b> "

---

**### Tổng quan**

****Ansible Inventory**** là thành phần dùng để khai báo các máy chủ mà Ansible sẽ quản lý.

Trong project, Inventory được tổ chức trong:

```text

ansible/inventory/

├── group_vars/

│   └── managed_nodes.yml

├── host_vars/

│   ├── managed-01.yml

│   └── managed-02.yml

├── hosts.example.ini

└── hosts.ini

```

`hosts.ini` là Inventory chính của project, trong khi `group_vars` và `host_vars` cung cấp các biến cho group hoặc từng host.

![ASAU](/images/01/image_202.png)

**### 1. File hosts.ini**

File:

```text

ansible/inventory/hosts.ini

```

có nhiệm vụ khai báo các Managed Nodes.

Hai Managed Nodes của project là:

```text

managed-01

managed-02

```

Nhờ Inventory, Ansible biết những máy chủ nào thuộc phạm vi quản lý.

![ASAU](/images/01/image_203.png)

> ****Lưu ý:**** Nội dung code của `hosts.ini` trong báo cáo cần sử dụng đúng file FINAL của project. Không sử dụng lại IP hoặc cấu hình từ các phiên bản cũ nếu project đã thay đổi.

**### 2. group_vars**

Thư mục:

```text

inventory/group_vars/

```

chứa các biến áp dụng chung cho một group.

Project có:

```text

managed_nodes.yml

```

Các biến trong file này có thể được sử dụng chung cho các Managed Nodes thuộc cùng group.

![ASAU](/images/01/image_204.png)

**### 3. host_vars**

Thư mục:

```text

inventory/host_vars/

```

chứa các biến riêng cho từng host.

Project có:

```text

host_vars/

├── managed-01.yml

└── managed-02.yml

```

Cách tổ chức này cho phép project tách biến dùng chung và biến riêng của từng Managed Node.



**### 4. hosts.example.ini**

Project có thêm:

```text

hosts.example.ini

```

Đây là file mẫu để tham khảo cấu trúc Inventory.

Trong khi đó:

```text

hosts.ini

```

là Inventory được sử dụng cho môi trường thực tế.

**### 5. Cách Ansible sử dụng Inventory**

Luồng xử lý cơ bản:

```text

                 Ansible

                    |

                    ↓

               ansible.cfg

                    |

                    ↓

                hosts.ini

                    |

          +---------+---------+

          |                   |

          ↓                   ↓

      managed-01          managed-02

          |                   |

          +---------+---------+

                    |

                    ↓

              Playbook / Task

```

Khi Playbook chỉ định một group, Ansible sẽ thực hiện các task trên những host thuộc group đó. Các biến trong `group_vars` và `host_vars` được sử dụng trong quá trình xử lý.

**### 6. Kiểm tra Inventory**

Có thể kiểm tra Inventory bằng:

```bash

ansible-inventory --list

```

Hoặc xem cấu trúc group và host:

```bash

ansible-inventory --graph

```



**### Kết quả**

Sau khi hoàn thành, cấu trúc Inventory của project là:

```text

Inventory

│

├── hosts.ini

│   ├── managed-01

│   └── managed-02

│

├── group_vars/

│   └── managed_nodes.yml

│

└── host_vars/

    ├── managed-01.yml

    └── managed-02.yml

```

Inventory đóng vai trò kết nối giữa ****Ansible Control Node**** và các ****Managed Nodes****, cung cấp danh sách host và các biến cần thiết cho quá trình automation.

Phần tiếp theo sẽ tìm hiểu ****Ansible Playbooks**** và cách Playbook sử dụng Inventory để thực hiện các task trên Managed Nodes.