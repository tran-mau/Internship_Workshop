---

title : "Install Python"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.2.2 </b> "

---

### Steps

Python is an important component of the automation system. In the project, Python is used as the foundation for scripts and the **Python Security Engine**, while Ansible is also built on Python.

## 1. Install Python Packages

On the Automation Server, run:

```bash
sudo apt install -y python3 python3-pip python3-venv
```

These packages include:

- `python3`: Provides Python 3.
- `python3-pip`: Python package manager.
- `python3-venv`: Provides the tools required to create a Python Virtual Environment.

These packages are used to prepare the Python environment for the project.

## 2. Check Python and pip

Check the Python version:

```bash
python3 --version
```

Check pip:

```bash
pip3 --version
```

![ATSV](/images/01/image_070.png)

## 3. Create the Project Directory

Create the main project directory:

```bash
mkdir -p ~/enterprise-infrastructure-automation
```

Then move into the directory:

```bash
cd ~/enterprise-infrastructure-automation
```

This will be the main working directory for the Ansible and Python components of the project.

## 4. Create a Python Virtual Environment

It is not recommended to install all Python libraries directly into the system Python environment. Therefore, the project uses a **Virtual Environment** to create an isolated Python environment.

Create the virtual environment:

```bash
python3 -m venv .venv
```

Where:

- `python3`: Uses Python 3.
- `-m venv`: Executes the `venv` module to create a virtual environment.
- `.venv`: Directory containing the project's virtual environment.

## 5. Activate the Virtual Environment

Activate the virtual environment:

```bash
source .venv/bin/activate
```

After activation, the `.venv` environment will be used instead of the system Python when performing Python-related operations in the project.

Check which Python executable is being used:

```bash
which python
```

Check the Python version:

```bash
python --version
```

![ATSV](/images/01/image_072.png)

## Result

After completing these steps, the Automation Server has a basic Python environment:

```text
enterprise-infrastructure-automation/

│

└── .venv/
```

The Python Virtual Environment separates the project's libraries from the operating system's default Python environment, providing a foundation for deploying the Python components in the following sections.