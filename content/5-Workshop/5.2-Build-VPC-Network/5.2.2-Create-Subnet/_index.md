---
title : "Create Subnet"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

1. Go to the AWS Console interface, search for subnet -> select Subnet  
   ![Subnet](/images/05/image_010.png)  
2. After entering the subnet interface, select create subnet  
   ![Subnet](/images/05/image_011.png)  
   + First, we will select the VPC that we created above for this subnet
   ![Subnet](/images/05/image_012.png)  
   + Next, we will fill in the information fields for the subnet settings  
     + Subnet name: Public-subnet-a (only used to identify the subnet)  
     + AZ: select az Asia Pacific (Singapore) / apse1-az2 (ap-southeast-1a)  
     + IPv4 VPC CIDR block: 10.10.0.0/16 (the IP of the VPC)  
     + IPv4 subnet CIDR block: select the address range for subnet a as 10.10.1.0/24
   ![Subnet](/images/05/image_013.png)  
3. This is the interface after we successfully create the public subnet of the mini – company VPC  


4. Continue doing the same to create a private subnet for this VPC:  
   ![Subnet](/images/05/image_014.png)  
   + These will be the properties for the private subnet  
     + Subnet name: private-subnet-a  
     + AZ: Asia Pacific (Singapore) / apse1-az2 (ap-southeast-1a)  
     + Ipv4 Subnet: 10.10.2.0/24  
   ![Subnet](/images/05/image_015.png)
5. These are the 2 subnets that we have just created