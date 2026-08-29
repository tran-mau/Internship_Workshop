---

title : "Automation Server"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.2 </b> "

---

### Overview

In this chapter, we will prepare the **Automation Server** to become the control server of the automation system. The Automation Server uses Ubuntu Server 24.04 LTS and is installed with the necessary tools such as Python, Git, and Ansible.

After completing this chapter, the Automation Server will be ready to perform automation tasks and manage the Managed Nodes.

### List of Detailed Lessons

1. **6.3.1 – Prepare Automation Server**

   * Connect to the Automation Server

   * Check the operating system

   * Change the hostname

   * Check Internet connectivity

   * Update packages

2. **6.3.2 – Install Python**

   * Install Python 3

   * Install pip and python3-venv

   * Create a Python Virtual Environment

   * Activate and check the Virtual Environment

3. **6.3.3 – Install Ansible**

   * Install Ansible

   * Check Ansible

   * Check Ansible commands

   * Check `ansible-galaxy`

4. **6.3.4 – Set Up Project**

   * Create the `enterprise-infrastructure-automation` directory

   * Create `.gitignore`

   * Prepare the project structure for Ansible and Python

### Automation Server Architecture

After completing the preparation steps, the Automation Server has the following basic structure:

~~~text
Automation-Server

│

├── Ubuntu Server 24.04

├── Python

├── Virtual Environment

├── Ansible

└── Git
~~~

The Automation Server will act as the **Ansible Control Node** in the following sections. From here, Ansible will be used to manage and automate configurations on the Managed Nodes.

### List of Practical Chapters

+ [5.2.1 Prepare Automation Server]({{< relref "5.2.1-Prepare-Automation-SV">}})

+ [5.2.2 Install Python]({{< relref "5.2.2-Install-Python">}})

+ [5.2.3 Install Ansible]({{< relref "5.2.3-Install-Ansible">}})

+ [5.2.4 Set Up Project]({{< relref "5.2.4-Setup-Project">}})

+ [5.2.5 Set Up SSH]({{< relref "5.2.5-Setup-SSH">}})