---

title : "Create IAM Role for EC2"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.5.1 </b> "

---  

### Steps to Perform  

1. Go to IAM -> Roles -> Create role  

![IAM](/images/05/image_090.png)  

![IAM](/images/05/image_091.png)  

2. Select trusted entity:  

+ Entity type: select AWS Service  

+ Service or use case: EC2  

+ Add permissions: Select Use existing policy  

-> Search for the Policy: AmazonSSMManagedInstanceCore and select it -> Next  

![IAM](/images/05/image_092.png)  

+ Next, we will set the Role name:  

  + Role name: MiniProject-EC2-Role  

  + Description: Allows EC2 instances to call AWS services on your behalf  

  + Select Create Role  

![IAM](/images/05/image_093.png)