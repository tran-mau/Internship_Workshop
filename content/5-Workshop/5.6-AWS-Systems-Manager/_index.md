---

title : "AWS Systems Manager" 

date : "`r Sys.Date()`" 

weight : 6

chapter : false 

pre : " <b> 5.6 </b> " 

---

+ In this chapter, we will deploy **AWS Systems Manager (SSM)** to manage and monitor EC2 instances in the system without needing to connect directly through SSH. AWS Systems Manager provides tools to support server administration, execute remote commands, and check the status of EC2 instances.

+ In the mini project, **AWS Systems Manager** is used in combination with an **IAM Role**. EC2 is assigned an appropriate IAM Role to connect to Systems Manager. Through SSM, administrators can access and execute commands on EC2 securely without needing to open the SSH port to the entire Internet.

+ Using AWS Systems Manager helps reduce dependence on SSH, minimizes the need to manage SSH Keys, and increases the security level when managing servers located in the **Private Subnet**.

### Detailed Lesson List:

+ [5.6.1 Overview of AWS Systems Manager]({{< relref "5.6.1-Overview-Systems-Manager">}})

+ [5.6.2 Set Up AWS Systems Manager (SSM)]({{< relref "5.6.2-Setup-Systems-Manager">}})



### Chapter Objectives

After completing this chapter, the learner will be able to:

+ Understand the functions and role of **AWS Systems Manager** in server administration.

+ Understand the relationship between **EC2, IAM Role, and SSM Agent**.

+ Configure an IAM Role so that EC2 can use AWS Systems Manager.

+ Check the operating status of the **SSM Agent** on EC2.

+ Connect to EC2 using **Session Manager** without using SSH.

+ Execute administrative commands on EC2 through Systems Manager.

+ Manage and check EC2 instances located in the **Private Subnet**.

+ Check and troubleshoot issues that prevent EC2 from appearing in Systems Manager.

### AWS Systems Manager in the Mini Project

In the mini project architecture, AWS Systems Manager serves as a tool to support the management of EC2 instances.

The operating model can be described as follows:

**EC2 → IAM Role → SSM Agent → AWS Systems Manager**

Where:

+ **EC2** is the server that needs to be managed.

+ **IAM Role** provides the necessary permissions for EC2 to communicate with AWS services.

+ **SSM Agent** is installed and running on EC2 to receive management requests from Systems Manager.

+ **AWS Systems Manager** provides the interface and tools for administrators to connect, execute commands, and manage EC2 instances.

For the **Private EC2**, using Systems Manager is particularly useful because the server does not need a Public IP and does not necessarily need to open an SSH port from the Internet. When the EC2 can communicate with the required AWS Systems Manager endpoints, administrators can use **Session Manager** to access the server.

### Role of Systems Manager in System Security

Using AWS Systems Manager helps enhance the security of the system architecture by:

+ Limiting the opening of **TCP/22 (SSH)** ports in the Security Group.

+ No need to use a Public IP to manage EC2.

+ No need to store an SSH Private Key on the administrator's computer to use Session Manager.

+ Access permissions can be controlled through **IAM**.

+ EC2 instances located in the Private Subnet can also be managed.

+ Provides centralized support for managing and operating servers on AWS.

In the mini project, Systems Manager is used in combination with **IAM Role, VPC, Private Subnet, and EC2** to build a more secure server management architecture.