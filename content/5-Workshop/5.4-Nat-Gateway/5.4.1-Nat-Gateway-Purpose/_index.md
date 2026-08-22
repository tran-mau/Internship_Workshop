---

title : "Why Do We Need a NAT Gateway?"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.4.1 </b> "

--- 

## What is a NAT Gateway?

**NAT Gateway (Network Address Translation Gateway)** is an AWS service that allows resources located in a **Private Subnet** to access the external Internet, while the Internet cannot proactively initiate a direct connection to these resources.

In our network model, the Private EC2 is not assigned a Public IP. Therefore, if we want the Private EC2 to access the Internet to update the system, install software, or download necessary packages, we need to use a NAT Gateway.

## Why Do We Need a NAT Gateway?

1. Allow Private EC2 to access the Internet

+ Private EC2 can access the Internet to:

  + Update the operating system.

  + Install necessary packages.

  + Download software and libraries.

  + Connect to external services.

2. No need to assign a Public IP to Private EC2

+ Private EC2 can still access the Internet without being assigned a Public IPv4.

+ This helps prevent the Application Server from being directly exposed to the Internet.

3. Improve security

+ Private EC2 can only proactively send outbound connections through the NAT Gateway.

+ The external Internet cannot use the NAT Gateway to proactively establish a direct connection to the Private EC2.