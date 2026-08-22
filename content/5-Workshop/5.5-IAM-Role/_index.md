---

title : "IAM Role"

date : "`r Sys.Date()`"

weight : 5

chapter : false

pre : " <b> 5.5 </b> "

---

+ In this chapter, we will deploy an IAM Role and assign the Role to the EC2 instances in the system. The IAM Role allows EC2 to use AWS services through the granted permissions without storing the Access Key and Secret Access Key directly on the server.  

+ The IAM Role is used to grant EC2 permissions to perform necessary tasks such as accessing Amazon S3, using AWS Systems Manager (SSM), and sending monitoring data to Amazon CloudWatch. Using an IAM Role helps improve security and convenience during system administration.  



### Detailed Lesson List:  

+ [5.5.1 Create IAM Role for EC2]({{< relref "5.5.1-Create-IAM-Role">}})  

+ [5.5.2 Attach IAM Role to EC2]({{< relref "5.5.2-Attach-Role-EC2">}})