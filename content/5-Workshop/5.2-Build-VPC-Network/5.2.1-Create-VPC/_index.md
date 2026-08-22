--- 
title : "Create VPC" 
date : "`r Sys.Date()`" 
weight : 1 
chapter : false 
pre : " <b> 5.2.1 </b> " 
--- 
 
1. Go to the AWS Console interface, type VPC in the search bar, and select the VPC icon.    
![VPC](/images/05/image_003.png)   
   
![VPC](/images/05/image_004.png)   
   
2. After accessing VPC, select Create VPC.   
   ![VPC](/images/05/image_005.png)   
    
3. After selecting Create VPC, we will have an interface to enter the information fields for our VPC:   
   + In the Resources to create section: select VPC only because here we want to configure the other components in the network ourselves.   
   + In the Name tag – optional section: name it mini-company-vpc (this is only an identifier for the VPC).   
   + IPv4 CIDR block has 2 options: IPv4 CIDR manual input and IPAM-allocated IPv4 CIDR block.   
     + IPv4 CIDR manual input means that we manually enter a fixed IP range according to the CIDR standard (for example: 10.0.0.0/16 or 172.16.0.0/16).   
     + IPAM-allocated IPv4 CIDR block means that we select an IP range that is managed and automatically allocated by AWS VPC IPAM.   
     -> Therefore, select IPv4 CIDR manual input.   
   + In the IPv4 CIDR section, we will enter the address range for the VPC: 10.10.0.0/16.   
   + For IPv6 CIDR block, select No IPv6 CIDR block because we do not use IPv6 in this lesson.   
   + Tenancy:   
     + default means that the physical server will be shared with multiple customers.   
     + Dedicated means that AWS reserves a physical server exclusively for you, and the cost will be very high.   
        -> Therefore, we will only use default here.   
   + Then select Create VPC.   
   
  ![VPC](/images/05/image_008.png)    
  ![VPC](/images/05/image_009.png)   
 
This is the interface we will see after successfully creating the VPC.