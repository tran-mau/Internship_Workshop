---

title : "Create IAM Role for Automation Server"

date : "`r Sys.Date()`"

weight : 7

chapter : false

pre : " <b> 5.1.7 </b> "

---

### Steps

In this project, the **Automation Server** needs to interact with AWS services. Therefore, we create an **IAM Role** to grant permissions to the Automation Server.

### 1. Access IAM

In the **AWS Console**, search for **IAM** and select the **IAM** service.

![IAM](/images/01/image_054.png)

### 2. Create IAM Role

In the IAM interface, select:

~~~text
Roles

→ Create role
~~~

3. In the Role creation interface, select the appropriate Trusted Entity type so that EC2 can use the IAM Role.

![IAM](/images/01/image_055.png)

4. Next, configure the required **Permissions** for the Automation Server.

   The permissions granted should be appropriate for the AWS services that the Automation Server uses in the project.

![IAM](/images/01/image_057.png)

5. Set the IAM Role name according to the actual project configuration and select **Create role**.

   ~~~text
   Role name:

   <Automation-Server-Role>
   ~~~

   ![IAM](/images/01/image_058.png)

### 3. Attach IAM Role to Automation Server

After creating the IAM Role, return to the EC2 interface:

~~~text
EC2

→ Instances

→ Automation-Server
~~~

Select:

~~~text
Actions

→ Security

→ Modify IAM role
~~~

6. In the **IAM role** section, select the newly created Role and select **Update IAM role**.