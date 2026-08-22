---

title : "SSH to Private EC2"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.3.3 </b> "

---

## SSH to Private EC2 through Public EC2  

### Steps to Perform  

1. Open PowerShell and enter `ssh -V`

2. Enable the Windows SSH Agent

![SSH](/images/05/image_071.png)

3. Navigate to the directory containing the key and add the private key PEM file to the SSH agent on the laptop

![SSH](/images/05/image_072.png)

4. SSH into the Public EC2

![SSH](/images/05/image_073.png)

5. SSH to the Private EC2 using the command `ssh ubuntu@10.10.2.155`

![SSH](/images/05/image_074.png)

![SSH](/images/05/image_075.png)

6. Enter the following commands to check the Private EC2: Hostname; IP addr; IP route

![SSH](/images/05/image_077.png)

7. Check the connectivity of the Private EC2 without a NAT Gateway using the command: `curl -I https://www.google.com`

![SSH](/images/05/image_078.png)

=> Because there is no NAT Gateway yet, the Private EC2 cannot access the Internet, so in the next lesson we will continue with creating a NAT Gateway.