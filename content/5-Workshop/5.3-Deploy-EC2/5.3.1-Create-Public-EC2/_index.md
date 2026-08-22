---

title : "Create Public EC2"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.3.1 </b> "

---

### Steps to Perform  

1. In the AWS Console, select EC2, then select Instances → Launch instance  

![Subnet](/images/05/image_034.png)  

![Subnet](/images/05/image_035.png)  

2. Next, we will name the instance `mini-company-web-01`  

![Subnet](/images/05/image_036.png)  

3. Next:  

  + AMI: Ubuntu Server 24.04 LTS (64-bit ARM / x86)  

  + Instance type: t3.micro  

![Subnet](/images/05/image_037.png)  

4. In the key pair section, we will create a new key:  

  + Key pair name: mini-company-key  

  + Key pair type: RSA  

  + Private key file format: Keep the `.pem` format  

  + Then select Save key to your computer  

![Subnet](/images/05/image_038.png)  

5. Next is the Network settings section  

![Subnet](/images/05/image_039.png)  

  + VPC: Select the VPC that we created in the previous lesson (mini-company-vpc)  

  + Subnet: select public-subnet-a  

  + Auto-assign public IP: Select Enable  

  + For Firewall (security groups), we will need to create one because we have not created a security group before  

  ![Subnet](/images/05/image_040.png)  

  + Here, there will be the following information fields:

    + Security group name: web-sg  

    + Description: Security Group for web server

    + Inbound Security Group Rules: Create 3 inbound security rules:

      + SSH/TCP/22 from My IP

      + The second inbound security rule is ALL ICMP-IPv4/ICMP/all from Anywhere (0.0.0.0/0)  

      + The third inbound security rule is HTTP/TCP/80 also from Anywhere (0.0.0.0/0)  

    ![Subnet](/images/05/image_041.png)  

  + For Configure storage, allocate only 8 GB gp3  

  ![Subnet](/images/05/image_042.png)  

  + Then select Launch instance  

  ![Subnet](/images/05/image_043.png)  

  + This is the EC2 instance that we have just created  

6. Now we will check whether the network architecture is actually working correctly  

  + ![Subnet](/images/05/image_044.png)  

  + ![Subnet](/images/05/image_045.png)  

  + ![Subnet](/images/05/image_046.png)  

  + Check IP:

  ![Subnet](/images/05/image_047.png)  

  + Check Route Table:

  ![Subnet](/images/05/image_048.png)  

  + Check Internet connectivity:

  ![Subnet](/images/05/image_050.png)

7. How to test SSH to the second public EC2: use MobaXterm  

  ![Subnet](/images/05/image_060.png)  

  + Here, we will enter the information to SSH into the public EC2  

  + Remote host: 54.169.82.121, this is the public IP address of the public EC2  

  + Username: ubuntu, the default username for Ubuntu Server 24.04 LTS  

  + Check Use private key and use the `.pem` key that we created  

  + Select OK to connect to the EC2  

  ![Subnet](/images/05/image_061.png)  

  + This is the result after successfully connecting  

  ![Subnet](/images/05/image_062.png) 