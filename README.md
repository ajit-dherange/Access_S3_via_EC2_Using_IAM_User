# Access S3 via EC2 with Full access – By using IAM User

## Create New S3 Bucket
Click “S3” service
Click “Create bucket”.
Type sansboundd3.com
Bucket has been successfully created.

## Create New User
Click “IAM” service
Click “Users”.
Click “Add user”.
Provide user name
Click “Next”.
Select attach existing policies directly and provide AmazonS3 Full access.
Select S3 Full Access policy
Click “Create user”.
Create Access Key
Select CLI 
Create Access Key

## Create EC2 Instance
Click “Launch instance”.
Select “Amazon Linux”.
Select “t2.micro”.
Select VPC and Subnet, then select IAM role as “S3AccesswithEC2”.
Type Name as Linux Instance.
Create a new security group for access ssh port.
Click “Launch”.
Choose the key and Click Launch instances.
Click “View instances”.
Can use below script in user-data (optional)
#! /bin/bash -ex
yum update -y
yum install -y httpd
service httpd start
chkconfig httpd on
echo "<h2>WEBPAGE FROM THE INSTANCE: </h2>" >> /var/www/html/index.html
echo "<h2>Created at : </h2>">> /var/www/html/index.html
date >> /var/www/html/index.html
echo "<h2>IP address is : </h2>" >> /var/www/html/index.html
curl http://18.188.209.216/latest/meta-data/public-ipv4 >> /var/www/html/index.html
echo "<h2>Instance id is : </h2>">> /var/www/html/index.html
curl http://169.254.169.254/latest/meta-data/instance-id >> /var/www/html/index.html
echo "<h2>Hostname is : </h2>">> /var/www/html/index.html
curl http://169.254.169.254/latest/meta-data/public-hostnsme >> /var/www/html/index.html
echo "<h2>Created at : </h2>">> /var/www/html/index.html
date >> /var/www/html/index.html

## Verify Bucket from new EC2 Instance
Login to Linux instance by using SSH.
Type sudo -i
Login to aws configure mode by using access key ID and secret access key.  You must type the region to configure.
Type aws s3 ls command to list the bucket.
Type aws s3 rb s3://sansboundd3.com
Successfully removed the bucket.
Type aws s3 mb s3://aws.sansbound4.com
Successfully created the bucket.
Type Aws s3 ls
Bucket details listed successfully.
aws s3 cp f1.txt s3://aws.sansbound4.com
upload: ./f1.txt to s3://aws.sansbound4.com/f1.txt
Click “S3” service
