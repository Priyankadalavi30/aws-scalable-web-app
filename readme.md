AWS Application Load Balancer + Auto Scaling Group
Project Overview

This project demonstrates how to deploy a highly available web application on AWS using:

Amazon EC2 (Apache Web Server)
Launch Template
Auto Scaling Group (ASG)
Application Load Balancer (ALB)
Target Group
Security Groups
Architecture

User → ALB → Target Group → Auto Scaling Group → EC2 Instances

Steps Performed
1. Launch EC2 Instance
Amazon Linux 2023
Installed Apache (httpd)
Created test page
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

echo "<h1>Server 1</h1>" > /var/www/html/index.html
2. Create Launch Template
AMI: Amazon Linux 2023
Instance Type: t3.micro
Security Group: launch-wizard-1
Key Pair: web-key
3. Add User Data
#!/bin/bash
dnf install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Welcome from Auto Scaling Instance</h1>" > /var/www/html/index.html
4. Create Target Group
Protocol: HTTP
Port: 80
Health Check Path: /
5. Create Application Load Balancer
Internet Facing
Listener: HTTP : 80
Attached Target Group: web-target-group
6. Create Auto Scaling Group
Desired Capacity: 2
Min Capacity: 2
Max Capacity: 4
Attached to ALB Target Group
Health Checks: EC2 + ELB
Result

Load Balancer DNS:

web-alb-551443862.ap-south-1.elb.amazonaws.com

Output:

Welcome from Auto Scaling Instance
Key Learning
High Availability using multiple Availability Zones
Automatic instance provisioning with Launch Templates
Traffic distribution using ALB
Health checks with Target Groups
Dynamic scaling with Auto Scaling Groups
