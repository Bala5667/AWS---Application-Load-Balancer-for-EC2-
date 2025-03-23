# AWS---Application-Load-Balancer-for-EC2

Primary Objectives:

Deploy two EC2 instances running Apache web servers.

Host separate web pages for Facebook and Instagram.

Configure Target Groups to monitor the health of instances.

Set up an Application Load Balancer to distribute traffic evenly between the two instances.

Verify functionality by accessing the ALB DNS and confirming traffic redirection.

This solution enhances reliability and performance while ensuring seamless traffic management across multiple instances.

Steps to achieve the Objectives:

1. Created EC2 Instances
I launched two Amazon Linux EC2 instances:

Facebook Instance:

Configured Security Group to allow ports 80, 81, and ALL TCP.

Used the following User Data script to install Apache, create a webpage, and enable the web server:

#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
mkdir -p /var/www/html/facebook
echo "Welcome to my Facebook on EC2" > /var/www/html/facebook/index.html
chmod -R 755 /var/www/html/facebook
systemctl restart httpd

Instagram Instance:

Followed the same setup as Facebook, replacing facebook with instagram in the directory and file names.

2. Created Target Groups
I created two Target Groups for the load balancer:

Facebook Target Group:

Registered the Facebook EC2 instance.

Set the health check path to /facebook/index.html.

Instagram Target Group:

Registered the Instagram EC2 instance.

Set the health check path to /Instagram/index.html.

3. Configured the Application Load Balancer (ALB)
I created an Application Load Balancer and configured it as follows:

Added both target groups (Facebook and Instagram) to port 80.

Ensured equal traffic distribution between both instances.

Verified that the target groups were healthy before proceeding.

4. Testing the Load Balancer
Copied the DNS Name of the ALB and accessed it from my local browser.

The result successfully alternated between the Facebook and Instagram welcome messages.
