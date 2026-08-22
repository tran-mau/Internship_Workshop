---

title : "Create Amazon S3"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.8.1 </b> "

---

### Steps:

1. Go to AWS Console → S3 → Create bucket

![Role](/images/05/image_113.png)

2. Select the following S3 settings:

+ AWS Region: Asia Pacific (Singapore) ap-southeast-1

+ Bucket type: General purpose

+ Bucket namespace: Global namespace

+ Bucket name: mini-company-storage-1

![Role](/images/05/image_114.png)

+ Object Ownership: ACLs disabled (recommended)

![Role](/images/05/image_115.png)

+ Encryption type: Server-side encryption with Amazon S3 managed keys (SSE-S3)

+ Bucket Key: Disable

![Role](/images/05/image_116.png)

3. Create bucket

![Role](/images/05/image_117.png)

4. Upload a test file

+ Select: Upload → Add files

![Role](/images/05/image_118.png)

+ To allow the Private EC2 to access S3 without an Access Key or Secret Key, we will use the IAM Role created earlier.

+ Add S3 permissions to the EC2 Role

  + Go to: IAM → Policies → Create policy

  ![Role](/images/05/image_119.png)

  + Select: JSON → Enter the policy

  ![Role](/images/05/image_120.png)

  -> This policy allows EC2 to: List bucket; Download object; Upload object and does not allow Delete object.

  + Set a name and description for the Policy

  ![Role](/images/05/image_122.png)

+ Attach the Policy to the Role

  + IAM → Roles → MiniProject-EC2-Role

  ![Role](/images/05/image_123.png)

  + Select Add permissions → Attach policies

  ![Role](/images/05/image_124.png)

  + Select MiniProject-S3-Access

  ![Role](/images/05/image_125.png)

  + These are the Policies that have been created.

5. Check S3 from the Private EC2

+ Open an SSM Session to the Private EC2.

+ Install AWS CLI on the Private EC2.

+ Check the IAM Role.

![Role](/images/05/image_126.png)

+ The Private EC2 is using the IAM Role instead of using a personal Access Key.

+ Test S3 using the command `aws s3 ls s3://mini-company-storage-1`

![Role](/images/05/image_127.png)

(This command is used to list the files and subdirectories inside S3.)

+ Test Upload

![Role](/images/05/image_128.png)

  + `$ echo "Hello from Private EC2" > test.txt`

  + `$ aws s3 cp test.txt s3://mini-company-storage-1`

  -> These two commands are used to create a text file and upload the file to S3.

  + Then run the command `aws s3 ls s3://mini-company-storage-1` and the uploaded text file should appear in S3 successfully.

  + Try to delete the created test file using the command: `aws s3 rm s3://mini-company-storage-1/test.txt`

  ![Role](/images/05/image_129.png)

  -> The result is failed, as expected according to the configured policy.
  