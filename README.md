# Access S3 bucket via EC2 Instance with Full access – By using IAM User

## Create New S3 Bucket

Click “S3” service

Type jjkkexpress.online

Click “Create bucket”.

Bucket has been successfully created.


## Create New User

Click “IAM” service

Click “Users”.

Click “Add user”.

Type user name ppp

Click “Next”.

Select attach existing policies directly and provide AmazonS3 Full access.

Select S3 Full Access policy

Click “Create user”.

Select User ppp

Create Access Key

Select CLI 

Create Access Key


## Create EC2 Instance

Click “Launch instance”.

Select “Amazon Linux”.

Select “t2.micro”.

Select VPC and Subnet, then select IAM role as “S3AccesswithEC2”. (can lease as default)

Type Name as Linux Instance.

Create a new security group for access ssh port.

Click “Launch”.

Choose the key and Click Launch instances.

Click “View instances”.

Can use below script in user-data (optional)

```ruby
#! /bin/bash -ex
yum update -y
yum install -y httpd
service httpd start
chkconfig httpd on
echo "<h2>WEBPAGE FROM THE INSTANCE: </h2>" >> /var/www/html/index.html
echo "<h2>Created at : </h2>">> /var/www/html/index.html
date >> /var/www/html/index.html
echo "<h2>IP address is : </h2>" >> /var/www/html/index.html
hostname -i >> /var/www/html/index.html
echo "<h2>Hostname is : </h2>">> /var/www/html/index.html
hostname >> /var/www/html/index.html
```

## Verify Bucket from new EC2 Instance

Login to Linux instance by using SSH.

Type sudo -i

Login to aws configure mode by using access key ID and secret access key.  You must type the region to configure.

Type aws s3 ls command to list the bucket.

Type aws s3 rb s3://jjkkexpress.online

Successfully removed the bucket.

Type aws s3 mb s3://jjkkexpress2.online

Successfully created the bucket.

Type Aws s3 ls

Bucket details listed successfully.

aws s3 cp f1.txt s3://jjkkexpress2.online

upload: ./f1.txt to s3://jjkkexpress2.online/f1.txt

