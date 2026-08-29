---

title : "Create Security Group"

date : "`r Sys.Date()`"

weight : 5

chapter : false

pre : " <b> 5.1.5 </b> "

---

### Steps

In this project, we create **two separate Security Groups** to control connections to the Automation Server and Managed Nodes.

The connection model is configured as follows:

~~~text
Internet

   |
   | SSH TCP/22
   | My IP
   ↓
Automation-Server

   |
   | SSH TCP/22
   | Source: Automation-SG
   ↓
Managed-Node-01
Managed-Node-02
~~~

### 1. Create a Security Group for the Automation Server

In the AWS Console, go to:

~~~text
VPC
→ Security Groups
→ Create security group
~~~

![SG](/images/01/image_026.png)

Create the Security Group with the following information:

~~~text
Security group name:

Automation-SG

Description:

Security Group for Automation Server

VPC:

Automation-VPC
~~~

![SG](/images/01/image_027.png)

### 2. Configure Inbound Rules for Automation-SG

The Automation Server is located in the Public Subnet, so SSH connections from the management computer need to be allowed.

In the **Inbound rules** section, add the following rule:

| Type | Protocol | Port | Source |
| ---- | -------- | ---: | ------ |
| SSH  | TCP      | 22   | My IP  |

The **My IP** source helps restrict SSH access to the Automation Server from the IP address currently being used.

Outbound rule:

~~~text
All traffic
~~~

![SG](/images/01/image_028.png)

### 3. Create a Security Group for the Managed Nodes

Continue by creating a second Security Group for the two Managed Nodes.

Configure:

~~~text
Security group name:

Managed-Node-SG

VPC:

Automation-VPC
~~~

Managed Nodes are located in the Private Subnet, so SSH access is not opened directly from the Internet.

![SG](/images/01/image_030.png)

### 4. Configure Inbound Rules for Managed-Node-SG

In the **Inbound rules** section, create the following rule:

| Type | Protocol | Port | Source |
| ---- | -------- | ---: | ------------- |
| SSH  | TCP      | 22   | Automation-SG |

Here, the Source is configured as the **Security Group `Automation-SG`** instead of a specific IP address.

This allows servers using `Automation-SG`, specifically the Automation Server, to establish SSH connections to the Managed Nodes.

Outbound rule:

~~~text
All traffic
~~~

![SG](/images/01/image_031.png)

### 5. Result

After completing the configuration, the project has two Security Groups:

| Security Group | Object | Inbound SSH |
| ----------------- | ------------------ | ----------------------- |
| `Automation-SG` | Automation Server | TCP 22 from My IP |
| `Managed-Node-SG` | Managed-Node-01/02 | TCP 22 from Automation-SG |

The connection flow is controlled as follows:

~~~text
             My IP
               |
            TCP/22
               ↓
      +------------------+
      | Automation-SG    |
      | Automation-Server|
      +------------------+
               |
            TCP/22
               |
      Source: Automation-SG
               ↓
       +---------------+
       | Managed-Node- |
       | 01 / 02       |
       +---------------+
~~~

With this configuration, the Automation Server can be accessed via SSH from the management computer, while the Managed Nodes only allow SSH connections from the Automation Server through `Automation-SG`.

This Security Group configuration will be used in the subsequent steps to deploy EC2 instances and establish SSH connections between the Automation Server and Managed Nodes.