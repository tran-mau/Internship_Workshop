---

title : "Set Up CloudWatch and CloudTrail"

date : "`r Sys.Date()`"

weight : 7

chapter : false

pre : " <b> 5.7 </b> "

---

+ In this chapter, we will deploy **Amazon CloudWatch** and **AWS CloudTrail** to monitor, track, and inspect activities taking place within the AWS system. Both services play an important role in infrastructure management, troubleshooting, and improving system control.

+ **Amazon CloudWatch** is used to collect and monitor performance metrics of AWS resources, especially **EC2** instances in the mini project. Through CloudWatch, administrators can monitor metrics such as CPU utilization, EC2 status, and other metrics related to server activity.

+ In the mini project, CloudWatch is used to create an **Alarm** to detect when the CPU utilization of an EC2 instance exceeds the configured threshold. When the alarm condition occurs, the Alarm status changes from **OK** to **ALARM**, allowing administrators to quickly identify resource and server performance issues.

+ In addition to CloudWatch, **AWS CloudTrail** is used to record and track activities performed on the AWS account through APIs. CloudTrail helps determine **who performed what action, when the action was performed, and on which resource**, thereby supporting auditing, tracing, and system security.

+ Combining CloudWatch and CloudTrail helps build a relatively comprehensive monitoring and auditing mechanism for the mini project. CloudWatch focuses on the **status and performance of resources**, while CloudTrail focuses on the **activity history and changes made to AWS resources**.



### Detailed Lesson List:

+ [5.7.1 Set Up CloudWatch]({{< relref "5.7.1-Cloud-Watch">}})

+ [5.7.2 Set Up CloudTrail]({{< relref "5.7.2-Cloud-Trail">}})