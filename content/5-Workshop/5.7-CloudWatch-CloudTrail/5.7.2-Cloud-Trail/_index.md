---

title : "Set Up CloudTrail"  

date : "`r Sys.Date()`"  

weight : 2  

chapter : false  

pre : " <b> 5.7.2 </b> "  

---

In this section, we will use **AWS CloudTrail** to record and monitor activities occurring within the AWS account. CloudTrail helps administrators determine **who performed what action, on which resource, and at what time**.

### 1. Access CloudTrail Event History

Go to:

**AWS Console → CloudTrail → Event history**

![Role](/images/05/image_112.png)

**Event history** is where the history of API activities that have occurred in the AWS account is displayed.

Here, we can view information related to each event, such as:

+ **Event name:** The name of the action that was performed.

+ **Event time:** The time when the action occurred.

+ **Username:** The person or component that performed the action.

+ **Event source:** The AWS service on which the action was performed.

+ **Resource:** The resource associated with the event.

+ **Source IP address:** The IP address from which the request was made.

**### 2. Check Activity History**

CloudTrail automatically records administrative activities and API requests performed through the AWS Console, AWS CLI, or AWS services.

For example, when an administrator performs actions such as creating, modifying, or deleting EC2, VPC, Security Group, or IAM resources, the corresponding activities can be searched in **Event history**.

Administrators can use filters to search for a specific event based on **Event name, User name, Resource type, Resource name**, or a specific time range.

### 3. Result

Through **AWS CloudTrail**, administrative activities within the system are recorded and can be reviewed when necessary.

CloudTrail improves the ability to **audit, trace, and identify the causes of incidents**, thereby helping administrators monitor and secure the AWS system more effectively.