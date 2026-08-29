---

title : "Set Up Project"

date : "`r Sys.Date()`"

weight : 4

chapter : false

pre : " <b> 5.2.4 </b> "

---

### Steps

After preparing Python and Ansible, we proceed to create the project structure on the **Automation Server**.

The project uses the main directory:

```text
~/enterprise-infrastructure-automation
```

## 1. Create the Ansible Directory Structure

Move into the project directory:

```bash
cd ~/enterprise-infrastructure-automation
```

Create the main directories:

```bash
mkdir -p ansible/inventory
mkdir -p ansible/playbooks
mkdir -p ansible/roles
```

Initial structure:

```text
enterprise-infrastructure-automation/

│

├── .venv/

├── ansible/

│   ├── inventory/

│   ├── playbooks/

│   └── roles/

│

└── .gitignore
```

This is the foundation for organizing the Ansible components of the project.

![ATSV](/images/01/image_100.png)

## 2. Create the .gitignore File

Create or edit the `.gitignore` file:

```bash
nano .gitignore
```

This file is used to instruct Git to ignore files and directories that should not be included in the project's source code.

Some entries used in the project are:

```text
.venv/

__pycache__/

*.pyc

*.pem

*.key

.env

*.log

reports/*.tmp
```

In this configuration, `.venv/` is ignored because it is the project's Python virtual environment. Files such as `*.pem`, `*.key`, and `.env` are ignored to prevent sensitive information from being added to the repository.

## 3. Check the Project Structure

After creating the directories, check the structure again:

```bash
tree -L 3
```

The structure at this point will be the foundation for continuing the development:

```text
enterprise-infrastructure-automation/

│

├── ansible/

│   ├── inventory/

│   ├── playbooks/

│   └── roles/

│

├── .venv/

└── .gitignore
```

The `inventory`, `playbooks`, and `roles` directories will respectively be used to define Managed Nodes, build Playbooks, and organize Ansible Roles.

## Result

After completing these steps, the Automation Server has a dedicated workspace for the project:

```text
~/enterprise-infrastructure-automation/

│

├── .venv/

├── .gitignore

└── ansible/

    ├── inventory/

    ├── playbooks/

    └── roles/
```

The project is now ready to proceed to the next step: **setting up SSH between the Automation Server and Managed Nodes**, followed by creating the **Ansible Inventory**.