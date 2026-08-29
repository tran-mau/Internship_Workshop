---

title : "Prepare Automation Server"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.2.1 </b> "

---

### Steps

After completing the EC2 deployment, we proceed to prepare the **Automation Server** to be used as the control server for the automation system.

## 1. SSH into Automation Server

From the Windows machine, use SSH to connect to the `Automation-Server` EC2 instance.

The EC2 private key is used for authentication when establishing the connection.

![ATSV](/images/01/image_062.png)

## 2. Check the Operating System

After logging in, check the operating system information:

```bash
cat /etc/os-release
```

The Automation Server uses **Ubuntu Server 24.04 LTS**.

![ATSV](/images/01/image_063.png)

## 3. Change the Hostname

Check the current hostname:

```bash
hostname
```

Then change the hostname to make the server easier to identify:

```bash
sudo hostnamectl set-hostname automation-server
```

New hostname:

```text
automation-server
```

![ATSV](/images/01/image_064.png)

## 4. Check Internet Connectivity

The Automation Server is located in the **Public Subnet**, so we need to verify its Internet connectivity.

Check IP connectivity:

```bash
ping -c 4 8.8.8.8
```

Check DNS resolution:

```bash
ping -c 4 google.com
```

If the above commands work normally, the Automation Server has Internet connectivity through the AWS network configuration that was deployed.

![ATSV](/images/01/image_065.png)

## 5. Update Packages

Update the package list:

```bash
sudo apt update
```

Then upgrade the existing packages:

```bash
sudo apt upgrade -y
```

![ATSV](/images/01/image_067.png)

## Result

After completing the above steps, the Automation Server has been prepared with:

```text
Automation-Server

│

├── Ubuntu Server 24.04 LTS

├── Hostname: automation-server

├── Public Subnet

└── Internet connectivity
```

The Automation Server is now ready for **Python and Ansible** installation in the following steps.