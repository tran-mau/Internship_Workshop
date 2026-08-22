---

title : "Overview of AWS Systems Manager and SSM Agent"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.6.1 </b> "

---

## 1. What is AWS Systems Manager?

**AWS Systems Manager (SSM)** is an AWS service that helps manage and operate EC2 instances remotely. SSM allows administrators to perform management tasks without directly connecting to the server through SSH.

In this lesson, AWS Systems Manager is used to manage EC2 instances, especially **EC2 instances located in the Private Subnet**, through **Session Manager**.

## 2. What is the SSM Agent?

**SSM Agent** is software installed and running on EC2 that allows the server to communicate with AWS Systems Manager. The Agent is responsible for receiving and executing management requests sent from Systems Manager.

Operating model:

**AWS Systems Manager → SSM Agent → EC2**

When the SSM Agent is running and the EC2 instance is assigned an appropriate **IAM Role**, the server can connect to Systems Manager and receive commands from the administrator.

## 3. Role in the Mini Project

In the mini project, AWS Systems Manager and the SSM Agent are used in combination with an **IAM Role** to manage EC2 instances.

The components work as follows:

+ **IAM Role:** Provides permissions for EC2 to communicate with Systems Manager.

+ **SSM Agent:** Runs on EC2 and receives requests from Systems Manager.

+ **AWS Systems Manager:** Provides tools to manage and execute commands on EC2.

+ **Session Manager:** Allows administrators to access EC2 without opening an SSH port.

Using SSM improves security and convenience during server administration, especially for EC2 instances without a **Public IP**.