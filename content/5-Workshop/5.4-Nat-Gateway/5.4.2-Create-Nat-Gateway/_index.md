---

title : "Create NAT Gateway"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.4.2 </b> "

---  

### Steps to Perform  

1. First, we need to create an Elastic IP because a NAT Gateway requires a static public IP address at the time of creation, and AWS does not automatically assign a random Public IP to a NAT Gateway as it does for an EC2 instance.  

+ Go to VPC -> Elastic IPs -> Allocate Elastic IP address  

![NATGW](/images/05/image_079.png)  

2. Select Amazon's pool of IPv4 addresses in the Public IPv4 address pool field -> select Allocate  

![NATGW](/images/05/image_080.png)  

3. This is the Elastic IP that we have created  

![NATGW](/images/05/image_081.png)  

4. Next, we will create the NAT Gateway  

+ In the AWS Console: Select VPC → NAT Gateways → Create NAT gateway  

![NATGW](/images/05/image_082.png)  

5. Configure the NAT Gateway:  

+ Name: mini-company-nat-gateway  

+ Subnet: Select Public subnet 2  

+ Availability mode: select Zonal and then select public subnet a  

+ Connectivity type: select Public  

+ Elastic IP allocation ID: Select the Elastic IP that we just created  

![NATGW](/images/05/image_084.png)  

![NATGW](/images/05/image_085.png)  

6. This is the interface after successfully creating the NAT Gateway  

![NATGW](/images/05/image_086.png)  