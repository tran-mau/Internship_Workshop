---

title : "Install Ansible"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.2.3 </b> "

---

### Steps

In the project, **Ansible** is the main component responsible for **configuration management and automation**. The Automation Server will use Ansible to manage the Managed Nodes in the following steps.

## 1. Install Ansible

On the Automation Server, update the package list:

```bash
sudo apt update
```

Then install Ansible:

```bash
sudo apt install -y ansible
```

![ATSV](/images/01/image_077.png)

## 2. Check the Ansible Version

After installation, check Ansible:

```bash
ansible --version
```

This command confirms that Ansible has been installed successfully and displays information about the Ansible version and the Python environment being used.

![ATSV](/images/01/image_078.png)

## 3. Check Ansible Commands

Check the location of Ansible:

```bash
which ansible
```

Continue checking the important commands:

```bash
which ansible-playbook
```

```bash
which ansible-inventory
```

```bash
which ansible-galaxy
```

These commands will be used during the development of the automation system.

![ATSV](/images/01/image_079.png)

## 4. Check ansible-galaxy

In the project, we will use **Ansible Roles** and **Collections**.

`ansible-galaxy` is a command used to create and manage Roles and Collections.

## Result

After completing these steps, the Automation Server has Ansible and the required commands:

```text
Automation-Server

│

├── Python

├── Virtual Environment

├── Ansible

│   ├── ansible

│   ├── ansible-playbook

│   ├── ansible-inventory

│   └── ansible-galaxy

└── Git
```

The Automation Server is now ready to proceed to the **SSH connection setup with the Managed Nodes**, followed by the creation of the Ansible Inventory, Playbooks, and Roles.