---

title : "Create Route Table"

date : "`r Sys.Date()`"

weight : 4

chapter : false

pre : " <b> 5.2.4 </b> "

---

### Steps to Perform  

1. Go to the Route Table tab and select Create route table  

![Subnet](/images/05/image_023.png)  

2. Enter a name for the route table and select your mini-company VPC, then select Create route table  

![Subnet](/images/05/image_024.png)  

3. This will be the interface after we successfully create the public route table  

![Subnet](/images/05/image_025.png)  

4. Next, we will create an Internet route  

![Subnet](/images/05/image_026.png)  

5. Select Edit routes, then select Add route  

![Subnet](/images/05/image_027.png)  

6. Select the Destination range as 0.0.0.0/0 and the target as Internet Gateway. This means that packets destined for any other network → will be sent to the Internet Gateway. Then select Save changes  

![Subnet](/images/05/image_028.png)  

7. Next, we will Associate the route table with the public subnet  

![Subnet](/images/05/image_029.png)  

8. In the public-route-table, select Subnet associations and then select Edit subnet associations  

![Subnet](/images/05/image_030.png)  

9. Here, we will select public-subnet-a (the subnet that will connect to the IGW to access the Internet) and then select Save associations  

![Subnet](/images/05/image_031.png)  

10. This is the result after we have Associated the route table with the public subnet  

![Subnet](/images/05/image_032.png)  

![Subnet](/images/05/image_033.png)