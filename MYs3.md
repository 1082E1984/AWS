# AWS
this is my AWS Cloud Journey 
Today is March 31, 2019
BAsic things will be S3 pic upload, and EC2 instance sign on with SSH thru putty from a windows machine.
and next will be loading CLI proram for AWS on my windows machine, so I can run API commands for AWS from my Wn10 machine
also, I am going to list all my hardware in this file
3-31-2019 1:32pm
loaded up a image to S3-- and  found the syntax so you can put the string in a web browser and see the pic anywhere in the world
https://s3.amazonaws.com/bucketname/pathtofile 
had problems to get public access, and had to write a policy (googled it, and tailored it to my account specifics)
here is the code I used

{"Version": "2008-10-17",
"Statement": [{"Sid": "AllowPublicRead",
"Effect": "Allow",
"Principal": {
"AWS": "*"
},
"Action": "s3:GetObject",
"Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
}]}

and I made the imgage public thru setting on the bucket, so I had to make some adjustments at the bucket level
end of this section


#april 4th 2019 
#create lambda function to shut down an EC2 instance==need the Labda code===need IAM policy for a role that has the ability to 
#shut down an EC2 instance 


import boto3
#This simple lambda function is available from AWS with instructions on starting and stopping an instance at regular intervals using Lambda and CloudWatch: https://aws.amazon.com/premiumsupport/knowledge-center/start-stop-lambda-cloudwatch/
# Enter the region your instances are in. Include only the region without specifying Availability Zone; e.g., 'us-east-1'
region = 'us-east-1'
# Enter your instances here: ex. ['X-XXXXXXXX'] you can comma separate the instance IDs for more than one instance: i.e. ['X-XXXXXXXXX', 'X-XXXXXXXXX"]
instances = ['i-0902effe70a087ae7']

def lambda_handler(event, context):
    ec2 = boto3.client('ec2', region_name=region)
    ec2.stop_instances(InstanceIds=instances)
    
    
    #
#
#
#
#
july 7th 
ping instance--run code on user data at ec2 startup--- igw--nacls-security groups--  ssh and key pairs--- putty 3 items --- user data--private key--host name---

#
#
#
this is the code I have been using for the user data on an ec2 startup
#
#
#!/bin/bash
  yum update -y
  yum install -y httpd
  systemctl start httpd.service
  systemctl enable httpd.service
  EC2_AVAIL_ZONE=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
  echo "<h1>Hello World from $(hostname -f) in AZ $EC2_AVAIL_ZONE </h1>" > /var/www/html/index.html
  ##
  
  updates patches to linux, and starts apache, and reads metadata from 169.254.169.254 which is amazons metadata endpoint on instances.
  #
  #
#
#
https://github.com/jlevy/the-art-of-command-line

# super info on the linux command line on that link above   july 7th 2019

#
#
#
#
remote servier provided by matt kirk===  username uname -a   and hostname hostname -i and -d
#
#
#
what version and distro am I running on this gnu/linux machine--- dmsg | head -1
#
#
#
machine is running ubuntu 4.15.18 or 4.15.0.-60.67-generic 
uname -a will also display gnu/unix info, and username and ip address
#
#
