---

title : "Set Up AWS Systems Manager (SSM)" 

date : "`r Sys.Date()`" 

weight : 2 

chapter : false 

pre : " <b> 5.6.2 </b> " 

---

In this section, we will use **AWS Systems Manager (SSM)** to connect to and manage the **Private EC2** without using SSH through the Public EC2.

### 1. Check the Private EC2 in Systems Manager

Go to:

**AWS Systems Manager → Fleet Manager → Managed nodes**

![Role](/images/05/image_097.png)

Here, we can check the list of servers currently managed by AWS Systems Manager.

The **Private EC2** appears in the **Managed nodes** list with an active status, indicating that the EC2 has successfully connected to Systems Manager.

For the EC2 to appear in this list, the server must have the **SSM Agent running** and be assigned an appropriate **IAM Role** to communicate with Systems Manager.

### 2. Access Session Manager

Next, go to:

**AWS Systems Manager → Session Manager → Sessions**

![SMM](/images/05/image_098.png)

**Session Manager** is a feature that allows administrators to establish a direct working session with EC2 through the AWS browser interface.

The advantage of this method is that it does not require SSH or an SSH Private Key to access the server.

### 3. Create a Connection Session to the Private EC2

Select **Start session**.

Then select the **Private EC2** that needs to be managed and click **Start session**.

![SMM](/images/05/image_099.png)

AWS Systems Manager will use the **SSM Agent** on the EC2 to establish the connection. After the connection is successfully established, the system will open a terminal session directly in the browser.

### 4. Manage the Private EC2 Through the Terminal

After the session is started, we will see the terminal interface provided by AWS directly in the browser.

![SMM](/images/05/image_100.png)

Here, we can execute administrative commands on the Private EC2 similarly to using SSH.