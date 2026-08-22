---

title : "Create Internet Gateway"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.2.3 </b> "

---

### Steps to Perform

1. In the VPC console, select the Internet gateways tab and select Create internet gateway  

![Subnet](/images/05/image_016.png)  

+ Here, we only enter a name for the IGW and then select Create internet gateway  

![Subnet](/images/05/image_017.png)  

+ This is the interface that we will see after creating the IGW  

![Subnet](/images/05/image_018.png)  

+ After creation, the State of the internet gateway is detach – this means that the IGW has not been assigned to our mini-company VPC, so we need to Attach Internet Gateway to the VPC:  

  + Select Actions and select Attach to VPC  

  ![Subnet](/images/05/image_020.png)  

  + Select our VPC and then select Attach internet gateway  

  ![Subnet](/images/05/image_021.png)  

  + The State is now attached (the IGW has been assigned to the mini-company VPC)  

  ![Subnet](/images/05/image_022.png)  