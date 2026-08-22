---

title : "Create Private EC2"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.3.2 </b> "

---

### Steps to Perform  

1. Go to EC2 → Instances → Launch instance, just as we did with the public EC2  

![Subnet](/images/05/image_052.png)  

2. Fill in the information fields for the Private EC2  

+ Name: mini-company-private-01  

![Subnet](/images/05/image_053.png)  

+ AMI: Ubuntu Server 24.04 LTS (64-bit ARM / x86)  

+ Instance type: t3.micro  

+ In the key pair section, we will use the key pair created in the previous section  

![Subnet](/images/05/image_054.png)  

+ Network settings: 

  + VPC: mini-company-vpc  

  + Subnet: select private-subnet-a  

  + Auto-assign public IP: select Disable because it is located in the private subnet, so it will not have a public IP, only a private IP  

![Subnet](/images/05/image_055.png)  

+ For the security groups section, we will also create a new SG for this Private EC2  

![Subnet](/images/05/image_056.png)  

  + SG Name: private-ec2-sg  

  + Description: Security group for private EC2  

  + Inbound SG Rules: SSH/TCP/22 (Source type: Custom, Source: sg web)  

  -> This means that we will only allow SSH from the SG in the public subnet to the private subnet, rather than allowing the private subnet to connect directly to the Internet.

+ For Configure storage, we will also allocate only 8 GB gp3 -> Launch instance  

![Subnet](/images/05/image_057.png)  

+ This is our private EC2. It will not have a public IPv4 Address, but only a Private IPv4 address: 10.10.2.155  

![Subnet](/images/05/image_058.png) 

3. Note: Now, if we want to SSH into our private EC2, we must first SSH into the public EC2 that we created earlier. However, the key pair is stored on our laptop, not on the public EC2, so it cannot access the private EC2. Although this does not meet the security requirement if we upload the key pair to the public EC2, for this lab we will use this method to make testing easier.