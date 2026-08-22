---

title : "Set Up Cloud Watch"  

date : "`r Sys.Date()`"  

weight : 1  

chapter : false  

pre : " <b> 5.7.1 </b> "  

--- 

In this section, we will use **Amazon CloudWatch** to monitor the activity metrics of EC2 and set up a **CloudWatch Alarm** to alert when CPU utilization exceeds the allowed threshold.

### 1. Access CloudWatch Metrics

Go to:

**AWS Console → CloudWatch → Metrics**

![Role](/images/05/image_101.png)

**CloudWatch Metrics** provides metrics for monitoring the activity of AWS resources. For EC2, CloudWatch can collect metrics such as CPU, Network, Disk, and other information related to server activity.

Through Metrics, administrators can monitor the operating status of EC2 and detect abnormalities during operation.

### 2. Check EC2 Metrics

Select:

**EC2 → Per-Instance Metrics**

![Role](/images/05/image_102.png)

In **Per-Instance Metrics**, CloudWatch displays metrics collected separately for each EC2 Instance.

In this section, we focus on monitoring the metric: **CPUUtilization**

This metric represents the **percentage of CPU currently being used on the EC2**.

### 3. Monitor CPUUtilization

From Per-Instance Metrics, we can select the EC2 to monitor and view the **CPUUtilization** graph over time.

![Role](/images/05/image_102.png)

Through this graph, administrators can observe the CPU utilization of the EC2 and identify periods when the server has a high workload.

For example, if CPU utilization remains consistently high, this may indicate that the EC2 is processing many tasks or that the current resources are insufficient for the workload.

### 4. Create a CloudWatch Alarm

To automatically alert when the CPU utilization of the EC2 exceeds the allowed level, we create a **CloudWatch Alarm**.

Go to:

**CloudWatch → Alarms → Create Alarm**

![Role](/images/05/image_103.png)

CloudWatch Alarm allows us to define a condition based on a Metric. When the Metric meets the configured condition, the Alarm will change to an alert state and can send a notification to the administrator.

### 5. Select the Metric to Monitor

Select:

**Select metric → EC2 → Per-Instance Metrics → CPUUtilization**

![Role](/images/05/image_104.png)

Then select the correct **EC2 Instance** to monitor.

Selecting CPUUtilization allows CloudWatch to monitor the CPU utilization of the EC2 and use this value as the basis for triggering the alert.

### 6. Configure the Alarm Condition

We configure the following conditions:

+ **Statistic:** Average

+ **Period:** 5 minutes

+ **Condition:** Greater than 80%

![Role](/images/05/image_105.png)

The above parameters have the following meanings:

+ **Average:** CloudWatch uses the average CPU value over the selected time period.

+ **Period 5 minutes:** CPU data is evaluated over each 5-minute interval.

+ **Greater than 80%:** The Alarm will be triggered when the average CPU value exceeds 80% according to the configured condition.

Simply put:

**CPUUtilization > 80% → CloudWatch Alarm**

Setting the threshold to 80% helps detect situations where the EC2 has high CPU utilization and allows the administrator to promptly investigate the cause.

### 7. Configure Email Notifications

Next, we configure the notification method when the Alarm is triggered.

Select to send notifications via **Email** and enter the email address that should receive the alert.

![Role](/images/05/image_106.png)

When the Alarm changes to the **In alarm** state, CloudWatch will send a notification to the configured email address through **Amazon SNS**.

### 8. Name and Create the Alarm

Set a name and description for the Alarm for easier management.

![Role](/images/05/image_107.png)

After completing the configuration, select **Create alarm** to create the CloudWatch Alarm.

Once created, the Alarm will start monitoring the **CPUUtilization** Metric of the EC2 according to the configured conditions.

### 9. Result

After completing the configuration, the monitoring model is:

**EC2 → CloudWatch Metrics → CPUUtilization → CloudWatch Alarm → Email**

When the CPU of the EC2 is operating normally, the Alarm remains in the **OK** state.

When the average CPU exceeds the **80%** threshold according to the configured condition, the Alarm changes to the **In alarm** state and sends a notification to the administrator's email.

Combining **CloudWatch Metrics** and **CloudWatch Alarm** helps the system proactively detect abnormal resource conditions, supports administrators in monitoring EC2, and enables timely troubleshooting.