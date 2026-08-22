---

title : "Configure Route Table for Private Subnet"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.4.3 </b> "

---

### Steps to Perform

After creating the **NAT Gateway**, we need to configure the **Route Table** of the Private Subnet to route Internet traffic through the NAT Gateway.

### 1. Associate the Route Table with the Private Subnet

Go to:

**VPC → Subnets → Private subnet a → Route table → Edit route table association**

![RTB](/images/05/image_087.png)

Here, check the Route Table that is associated with the **Private Subnet**.

This Route Table determines how packets from the Private EC2 are routed to other resources within the VPC or to the Internet.

### 2. Add a Route to the NAT Gateway

In the Route Table of the Private Subnet, select **Edit routes** and add a route:

+ **Destination:** `0.0.0.0/0`

+ **Target:** The NAT Gateway that was created (`mini company nat gateway`)

![RTB](/images/05/image_088.png)

The route `0.0.0.0/0` represents all IPv4 traffic that does not belong to the specific networks defined in the Route Table.

When the Target is configured as the **NAT Gateway**, requests from the Private EC2 to the Internet will be routed through:

**Private EC2 → Private Subnet → Route Table → NAT Gateway → Internet Gateway → Internet**

The NAT Gateway will act on behalf of the Private EC2 to establish connections to the Internet. Therefore, the Private EC2 does not need a Public IP but can still access the Internet.



### 3. Check Internet Connectivity from the Private EC2

After completing the NAT Gateway and Route Table configuration, we proceed to check the Internet connectivity of the Private EC2.

![RTB](/images/05/image_089.png)