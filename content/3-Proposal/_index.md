---
title : "Proposal"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---
# Designing a Secure, Monitored, and Cost-Optimized AWS Cloud Infrastructure for Small and Medium-Sized Enterprises

## A Cloud Infrastructure Architecture Integrating Security, Centralized Monitoring, and Cost Management on AWS

### 1. Executive Summary

This proposal presents a solution for designing and deploying a Cloud infrastructure on Amazon Web Services (AWS) for small and medium-sized enterprise systems, focusing on three important challenges during Cloud adoption: **network security, system monitoring, and operational cost control**.

In practice, many organizations deploy Cloud servers by exposing resources such as Amazon EC2 directly to the Internet for convenient access. However, weak permission management, unnecessary open ports, excessive privileges, or the absence of centralized monitoring can create significant security vulnerabilities.

In addition, Cloud resources such as EC2, NAT Gateway, Load Balancer, and Data Transfer may generate costs even when the system is not operating at high capacity. Without appropriate monitoring and optimization mechanisms, organizations may have difficulty identifying the causes of increasing Cloud costs.

The proposed solution follows the **Defense in Depth** principle. The infrastructure is divided into Public and Private Subnets, access is controlled through Security Groups and IAM, and direct Internet access to internal servers is minimized.

The system also uses **Amazon CloudWatch** to monitor resources and performance, **AWS CloudTrail** to record API activities and administrative actions, **AWS Systems Manager (SSM)** to manage EC2 instances while reducing dependence on publicly accessible SSH, and **Amazon S3** for data and log storage.

The main objective is to build a Cloud infrastructure that is **practical to deploy, easy to monitor, scalable, secure, and cost-conscious**, while providing an architectural reference that can be reused for small and medium-sized enterprise systems.

---

### 2. Problem Statement

#### Current Problems

**1. Security risks caused by incorrect Cloud configuration**

One of the most common risks when deploying systems on the Cloud is incorrect configuration of network resources or access permissions.

For example, an EC2 instance may be assigned a Public IP address and expose SSH directly to the Internet. If the Security Group allows unrestricted access such as `0.0.0.0/0`, the server may become a target for automated scanning and attacks.

**2. Difficulty controlling access permissions**

Using IAM accounts with excessive privileges or storing Access Keys directly on servers increases the risk of credential exposure.

Therefore, the system should follow the **Least Privilege** principle, where each user and resource receives only the permissions required to perform its intended tasks.

**3. Lack of centralized monitoring**

If administrators rely only on SSH to log in and manually inspect servers, it becomes difficult to detect issues such as high CPU utilization, insufficient disk space, abnormal processes, or suspicious access activities.

The system therefore requires centralized mechanisms for collecting metrics, logs, and alerts.

**4. Difficulty auditing administrative activities**

In a Cloud environment, many operations are performed through the AWS Management Console, CLI, or APIs.

Without API activity logging, it can be difficult to determine who performed a particular action, which resource was modified, and when the change occurred.

**5. Difficulty controlling Cloud costs**

Resources such as EC2, NAT Gateway, Load Balancer, and Data Transfer may generate costs.

Deploying multiple resources for testing without properly stopping or deleting them can cause unnecessary cost increases.

Therefore, the infrastructure should be designed with a **Cost Awareness** approach, continuously monitoring resource usage and identifying cost-generating resources.

---

### Proposed Solution

The system is designed according to the **Secure, Monitorable, and Cost-Optimized Cloud Infrastructure** model.

The architecture is divided into the following layers:

1. **Network Layer** – VPC, Public Subnet, Private Subnet, Internet Gateway, and NAT Gateway.
2. **Compute Layer** – EC2 instances for applications and management tasks.
3. **Security Layer** – IAM, Security Groups, and Least Privilege access control.
4. **Management Layer** – AWS Systems Manager for EC2 management.
5. **Monitoring Layer** – Amazon CloudWatch for metrics, logs, and alarms.
6. **Audit Layer** – AWS CloudTrail for API activity auditing.
7. **Storage Layer** – Amazon S3 for data, backup, logs, and deployment files.
8. **Application Access Layer** – Application Load Balancer when traffic distribution is required.

Servers that need to receive Internet traffic are placed in the Public Subnet or accessed through an appropriate intermediate layer. Components that do not require direct Internet access are placed in the Private Subnet.

Security Groups are configured according to the principle of allowing only required communication flows.

For EC2 management, AWS Systems Manager is used to reduce dependence on direct SSH access from the Internet.

Amazon CloudWatch monitors system status and generates alerts when resources exceed predefined thresholds.

AWS CloudTrail records administrative and API activities to support auditing and incident investigation.

---

## 3. Solution Architecture

### 3.1. Overall Architecture

```text
                         INTERNET
                             |
                             v
                    +----------------+
                    | Internet       |
                    | Gateway        |
                    +-------+--------+
                            |
                 +----------+----------+
                 |         VPC          |
                 |                     |
        +--------v--------+   +--------v--------+
        | Public Subnet   |   | Private Subnet  |
        |                 |   |                 |
        | EC2 / ALB       |   | Private EC2     |
        |                 |   | Application     |
        +--------+--------+   +--------+--------+
                 |                     |
                 |                     |
                 +----------+----------+
                            |
                     +------v------+
                     | NAT Gateway |
                     +-------------+

       IAM / SSM / CloudWatch / CloudTrail / S3
                         |
                         v
                AWS Management Layer
```

The architecture is designed to separate **Internet access traffic**, **internal application traffic**, and **management and monitoring traffic**.

### 3.2. Flow A – Network & Traffic Flow

Users from the Internet send requests to the system through the Public Subnet.

The Internet Gateway provides connectivity between the VPC and the Internet.

Resources that need to serve Internet traffic are placed in the Public Subnet.

Servers that do not require a Public IP address are placed in the Private Subnet.

When a Private EC2 instance needs outbound Internet access to update packages or download required resources, traffic is routed through the NAT Gateway.

Security Groups control traffic between system components according to the following principles:

- Open only required ports.
- Do not expose SSH to the entire Internet.
- Allow Private EC2 to receive traffic only from trusted sources.
- Allow communication between servers only when required.

### 3.3. Flow B – EC2 Management with AWS Systems Manager

Administrators do not need to expose a public SSH port to the entire Internet.

EC2 instances are attached to an appropriate IAM Role so that they can work with AWS Systems Manager.

Administrators can use SSM to:

- Access EC2 instances.
- Check server status.
- Execute management commands.
- Collect system information.
- Manage servers through the AWS Console.

This approach reduces the attack surface and minimizes the need to maintain publicly accessible SSH ports.

### 3.4. Flow C – Monitoring with Amazon CloudWatch

Amazon CloudWatch collects monitoring information from the infrastructure.

Important metrics include:

- CPU Utilization.
- Network In/Out.
- Disk usage through CloudWatch Agent when required.
- EC2 instance status.
- Application logs.
- Metrics from relevant AWS services.

Administrators can configure CloudWatch Alarms to detect abnormal conditions.

```text
CPU > 80%
      |
      v
CloudWatch Alarm
      |
      v
Administrator Alert
      |
      v
Check EC2 / Application
```

This changes the operational model from **manual problem detection** to **proactive system monitoring**.

### 3.5. Flow D – Audit with AWS CloudTrail

AWS CloudTrail records API activities within the AWS account.

Examples include:

- Creating or deleting EC2 instances.
- Modifying Security Groups.
- Changing IAM Policies.
- Creating or deleting S3 Buckets.
- Modifying AWS service configurations.

Through CloudTrail, administrators can identify:

- Who performed an action.
- When the action occurred.
- Which API was called.
- Which resource was affected.

CloudTrail therefore plays an important role in incident investigation and system auditing.

### 3.6. Flow E – Storage with Amazon S3

Amazon S3 is used as the object storage layer of the system.

Potential use cases include:

- File storage.
- Backup storage.
- Log storage.
- Deployment file storage.
- Application data storage.

The S3 Bucket is configured according to the principle of restricting unnecessary Public Access and granting only the IAM permissions required by authorized resources.

---

## 4. AWS Services

| Service | Role |
|---|---|
| Amazon VPC | Build the private Cloud network |
| Public/Private Subnet | Separate resources according to access requirements |
| Internet Gateway | Connect the Public Subnet to the Internet |
| NAT Gateway | Provide outbound Internet access for the Private Subnet |
| Amazon EC2 | Run application servers |
| Security Group | Control network traffic |
| IAM | Manage identities and permissions |
| AWS Systems Manager | Remotely manage EC2 instances |
| Amazon CloudWatch | Monitor metrics, logs, and alarms |
| AWS CloudTrail | Audit and record API activities |
| Amazon S3 | Store data and files |
| Application Load Balancer | Distribute traffic when the system scales |

---

## 5. Technical Implementation

### Phase 1: VPC and Network Design

- Create the VPC.
- Create Public and Private Subnets.
- Configure Route Tables.
- Configure the Internet Gateway.
- Deploy a NAT Gateway when required.
- Design Security Groups.

The objective of this phase is to establish a network foundation that clearly separates public-facing and internal resources.

### Phase 2: EC2 Deployment

- Create the Public EC2 instance.
- Create the Private EC2 instance.
- Configure an IAM Role for EC2.
- Verify connectivity between servers.
- Verify outbound Internet connectivity from the Private EC2 instance.

### Phase 3: Centralized Management

- Configure AWS Systems Manager.
- Verify that EC2 instances are registered with Systems Manager.
- Manage servers through SSM.
- Reduce direct SSH exposure to the Internet.

### Phase 4: CloudWatch Deployment

- Configure CloudWatch.
- Collect EC2 metrics.
- Install the CloudWatch Agent when required.
- Collect application and system logs.
- Create a monitoring Dashboard.
- Create CloudWatch Alarms.
- Test alarms by generating load on an EC2 instance.

### Phase 5: CloudTrail Deployment

- Enable CloudTrail.
- Configure log storage.
- Monitor API activities.
- Perform selected resource changes to verify audit logs.
- Analyze important events.

### Phase 6: S3 and Data Security

- Create an S3 Bucket.
- Disable unnecessary Public Access.
- Configure IAM Policies.
- Test access permissions.
- Test data upload and download operations.

### Phase 7: Testing and Cost Optimization

Perform the following tests:

- Public → Private connectivity testing.
- Security Group testing.
- SSM testing.
- CloudWatch Alarm testing.
- CloudTrail testing.
- IAM permission testing.
- S3 access testing.
- Cost analysis for EC2, NAT Gateway, and other resources.

---

## 6. Technical and Security Requirements

### 6.1. Least Privilege Principle

IAM Roles and Policies should provide only the permissions required by each resource or user.

Administrator-level permissions should not be used when a task requires only a limited set of operations.

### 6.2. Public and Private Separation

Resources that do not require direct Internet access should be placed in the Private Subnet.

Private EC2 instances should not use Public IP addresses unless there is a specific requirement.

### 6.3. Security Groups

Security Groups should be configured according to the following principle:

```text
Internet
   |
   | Required ports only
   v
Public Layer
   |
   | Allowed traffic only
   v
Private Layer
```

Unnecessary ports should not be exposed to the Internet.

In particular, the following configuration should be avoided whenever possible:

```text
SSH 22 -> 0.0.0.0/0
```

Instead, administrators can use SSM or restrict access to specific trusted sources.

### 6.4. Proactive Monitoring

CloudWatch is used to detect:

- Abnormally high CPU utilization.
- Sudden increases in network traffic.
- Low available disk space.
- EC2 instance problems.
- Application errors in logs.

### 6.5. Auditing and Traceability

CloudTrail maintains a history of activities within the AWS account.

When an incident occurs, administrators can use CloudTrail to identify the cause and determine which actions were performed.

---

## 7. Deployment Roadmap

```text
+---------------------------------------------------------------+
| Phase 1: Network Design                                       |
| - VPC, Subnets, Route Tables                                  |
| - Internet Gateway, NAT Gateway                              |
| - Security Groups                                               |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Phase 2: Compute Deployment                                   |
| - Public EC2                                                  |
| - Private EC2                                                 |
| - IAM Role                                                    |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Phase 3: Centralized Management                               |
| - AWS Systems Manager                                         |
| - EC2 Management                                               |
| - Reduce Public SSH Exposure                                  |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Phase 4: Monitoring & Audit                                   |
| - CloudWatch                                                  |
| - CloudWatch Agent                                            |
| - CloudTrail                                                   |
| - Alarms & Dashboard                                          |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Phase 5: Storage & Security                                   |
| - Amazon S3                                                   |
| - IAM Policies                                                |
| - Public Access Control                                       |
+---------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------+
| Phase 6: Testing & Cost Optimization                          |
| - Security Testing                                            |
| - Load Testing                                                |
| - Monitoring Testing                                          |
| - Cost Analysis and Optimization                              |
+---------------------------------------------------------------+
```

---

## 8. Estimated Cost

The solution follows the **Pay-as-you-go** model and uses only the resources required by the workload.

The following components require particular attention regarding cost:

- Amazon EC2.
- NAT Gateway.
- Application Load Balancer.
- Data Transfer.
- EBS Volumes.
- Amazon S3.
- CloudWatch.
- CloudTrail.

For learning and testing environments, costs can be reduced by:

1. Using appropriately sized EC2 instances.
2. Stopping or terminating unused EC2 instances.
3. Deleting unused EBS Volumes and Elastic IP addresses.
4. Avoiding a NAT Gateway when it is not required.
5. Avoiding an ALB when there is no load-balancing requirement.
6. Regularly checking AWS Cost Explorer.
7. Using AWS Budgets and cost alerts to detect unexpected spending.

The objective is not only to build a functioning system but also to demonstrate the ability to **control and optimize Cloud infrastructure costs**.

---

## 9. Risk Assessment

| Risk | Impact | Probability | Mitigation Strategy |
|---|---|---|---|
| Security Group is too permissive | High | Medium | Apply Least Privilege and restrict sources |
| IAM credential exposure | High | Low | Use IAM Roles and minimize Access Keys |
| EC2 attacked from the Internet | High | Medium | Private Subnet, SSM, and restricted Security Groups |
| Failure is not detected quickly | High | Medium | CloudWatch Alarms and Dashboard |
| Administrative activity cannot be traced | High | Low | Use CloudTrail |
| Unexpected increase in Cloud costs | Medium | High | Cost monitoring and Budget Alerts |
| High NAT Gateway costs | Medium | High | Use NAT Gateway only when required |
| EC2 instances remain running while unused | Medium | High | Stop/Terminate unused instances and automate management |

---

## 10. Expected Results

### 10.1. Technical Results

Successfully build an AWS Cloud infrastructure capable of:

- Separating Public and Private Subnets.
- Deploying EC2 instances securely.
- Controlling traffic through Security Groups.
- Managing EC2 instances through AWS Systems Manager.
- Monitoring the infrastructure using CloudWatch.
- Auditing administrative activities using CloudTrail.
- Storing data using Amazon S3.
- Applying IAM according to the Least Privilege principle.

### 10.2. Security Results

Reduce the system's attack surface by limiting publicly accessible services, reducing dependence on SSH, and enforcing strict access control.

The system should also be capable of detecting and tracing abnormal events through CloudWatch and CloudTrail.

### 10.3. Operational Results

Administrators can monitor the infrastructure from a centralized environment instead of manually checking each EC2 instance.

CloudWatch provides monitoring and alerting capabilities, while Systems Manager supports centralized server management.

### 10.4. Cost Results

The project aims to demonstrate that infrastructure architecture decisions have a direct impact on Cloud costs.

By appropriately designing Public and Private Subnets and controlling the use of NAT Gateway, EC2, EBS, Load Balancer, and Data Transfer, the system can minimize unnecessary expenses.

### 10.5. Future Scalability

The architecture can be further extended with:

- Application Load Balancer.
- Auto Scaling Group.
- Amazon RDS.
- AWS Lambda.
- Amazon DynamoDB.
- AWS WAF.
- Amazon CloudFront.
- Infrastructure as Code using Terraform or AWS CloudFormation.
- CI/CD Pipeline.

This allows the architecture to evolve from a Cloud testing environment into an infrastructure platform capable of supporting real-world enterprise applications.
