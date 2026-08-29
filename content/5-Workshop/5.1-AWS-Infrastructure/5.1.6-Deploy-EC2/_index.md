---

title : "Deploy EC2"

date : "`r Sys.Date()`"

weight : 6

chapter : false

pre : " <b> 5.1.6 </b> "

---

### Steps

After completing the VPC, Subnets, Internet Gateway, Route Tables, and Security Groups, we proceed to deploy three EC2 instances for the system:

* `Automation-Server`

* `Managed-Node-01`

* `Managed-Node-02`

The Automation Server acts as the control server, while the two Managed Nodes are the servers managed through Ansible. This is the architecture used in the internship project.

### 1. Create Automation Server

1. In the **AWS Console**, select **EC2 → Instances → Launch instance**.

   ![EC2](/images/01/image_033.png)

2. Set the instance name:

   ~~~text
   Automation-Server
   ~~~

   ![EC2](/images/01/image_034.png)

3. In **Application and OS Images (AMI)**, select:

   ~~~text
   Ubuntu Server 24.04 LTS
   ~~~

   Instance type:

   ~~~text
   t3.micro
   ~~~

   This is the configuration used for the Automation Server in the project.

   ![EC2](/images/01/image_035.png)

4. In the **Key pair** section, select the key pair used for the project to allow SSH access to the Automation Server from the management computer.

   ![EC2](/images/01/image_036.png)

5. In the **Network settings** section, configure:

   * **VPC:**

     ~~~text
     Automation-VPC
     ~~~

   * **Subnet:**

     ~~~text
     Automation-Public-Subnet
     ~~~

   * **Auto-assign public IP:** `Enable`

   * **Security Group:**

     ~~~text
     Automation-SG
     ~~~

   The Automation Server is placed in the Public Subnet and has a Public IP to allow management from outside.

   ![EC2](/images/01/image_037.png)

   ![EC2](/images/01/image_038.png)

6. After checking the configuration information, select **Launch instance**.

   ![EC2](/images/01/image_039.png)

7. After successfully launching the instance, `Automation-Server` will appear in the EC2 Instances list.

   ![EC2](/images/01/image_040.png)

### 2. Create Managed-Node-01

1. Continue by selecting **Launch instance** to create the second EC2 instance.

2. Set the name:

   ~~~text
   Managed-Node-01
   ~~~

   ![EC2](/images/01/image_041.png)

3. Use:

   ~~~text
   AMI:

   Ubuntu Server 24.04 LTS

   Instance type:

   t3.micro
   ~~~

   ![EC2](/images/01/image_042.png)

4. In **Network settings**, configure:

   ~~~text
   VPC:

   Automation-VPC

   Subnet:

   Automation-Private-Subnet

   Auto-assign public IP:

   Disable

   Security Group:

   Managed-Node-SG
   ~~~

   This is the configuration of Managed-Node-01 in the project. The Managed Node is placed in the Private Subnet and is not assigned a Public IP.

   ![EC2](/images/01/image_044.png)

5. After checking the configuration, select **Launch instance**.

   ![EC2](/images/01/image_047.png)

### 3. Create Managed-Node-02

1. Continue by selecting **Launch instance** to create the third EC2 instance.

2. Set the name:

   ~~~text
   Managed-Node-02
   ~~~

   ![EC2](/images/01/image_048.png)

3. Use:

   ~~~text
   AMI:

   Ubuntu Server 24.04 LTS

   Instance type:

   t3.micro
   ~~~

   ![EC2](/images/01/image_049.png)

4. In **Network settings**, configure:

   ~~~text
   VPC:

   Automation-VPC

   Subnet:

   Automation-Private-Subnet

   Auto-assign public IP:

   Disable

   Security Group:

   Managed-Node-SG
   ~~~

   Managed-Node-02 is deployed similarly to Managed-Node-01 and is located in the Private Subnet.

   ![EC2](/images/01/image_051.png)

5. After checking the configuration, select **Launch instance**.

   ![EC2](/images/01/image_053.png)

### 4. Check the EC2 Instances

After completing the deployment, there will be three instances in the EC2 list:

| Instance | Subnet | Public IP | Security Group | Role |
| ------------------- | --------------------------- | --------- | ----------------- | -------------------- |
| `Automation-Server` | `Automation-Public-Subnet` | Enable | `Automation-SG` | Ansible Control Node |
| `Managed-Node-01` | `Automation-Private-Subnet` | Disable | `Managed-Node-SG` | Managed Node |
| `Managed-Node-02` | `Automation-Private-Subnet` | Disable | `Managed-Node-SG` | Managed Node |

The architecture after deployment:

~~~text
                        Automation-VPC

                         10.0.0.0/16

                              |

              +----------------+----------------+

              |                                 |

       Public Subnet                     Private Subnet

        10.0.1.0/24                       10.0.2.0/24

              |                                 |

       Automation-Server              +-----------+-----------+

                                      |                       |

                                Managed-Node-01        Managed-Node-02
~~~

The Automation Server will be the **Ansible Control Node** and will establish connections to the two Managed Nodes to manage and automate their configuration.

### Result

After completing this section, the project's EC2 infrastructure has been deployed according to the following model:

~~~text
Internet

    |

    ↓

Automation-Server

Public Subnet

    |

    | SSH

    ↓

Private Subnet

    ├── Managed-Node-01

    └── Managed-Node-02
~~~

The EC2 instances are now ready for the next step: **preparing the Automation Server and installing the Python and Ansible environment**.