# AWS Project: VPC Setup
## Overview
This project demonstrates creating a secure AWS VPC with public and private subnets, NAT Gateway, EC2 instances, and properly configured security groups.

- One Public Subnet → Public EC2 (SSH/HTTP)
- One Private Subnet → Private EC2 (SSH via Public EC2)
- NAT Gateway → Provides Internet access to Private EC2
- Properly configured Security Groups and Key Pairs

The goal is to learn network isolation, secure access, and cloud resource management in AWS.

## Architecture
- Public Subnet → Public EC2 (SSH/HTTP)
- Private Subnet → Private EC2 (SSH via Public EC2)
- NAT Gateway → Internet access for private EC2
- Database instance isolated in private subnet
![Architecture Diagram](architecture-diagram.png.jfif)
## Key Commands Used
- SSH into Public EC2:
  ssh -i ./Testkeypair.pem ec2-user@Public-IP
- command to install, enable and start Apache respectively:
  - sudo yum install httpd -y
  - sudo systemctl enable httpd
  - sudo systemctl start httpd
- command to change keypair permission:
  chmod 400 "Testkeypair.pem"
- SSH from Public EC2 to Private EC2:
  ssh -i Testkeypair.pem ec2-user@Private-IP
- Update packages on Private EC2:
  sudo yum update -y
- Security Group configurations:
  - Private SG inbound SSH from Public SG
  - Private SG inbound MySQL/Aurora from Public SG
  - 
## Instructions to use commands

# 1️ Connect to Public EC2 from local machine
ssh -i ./Testkeypair.pem ec2-user@Public-IP

# 2️ Copy Key Pair to Public EC2 (for Private EC2 access)
scp -i ./Testkeypair.pem ./Testkeypair.pem ec2-user@Public-IP:~

# 3️ SSH from Public EC2 to Private EC2
ssh -i Testkeypair.pem ec2-user@Private-IP

# 4️ Test connectivity between Public and Private EC2
ping Private-IP

# 5️ Update packages on Private EC2
sudo yum update -y

# 6️ Apache Web Server Setup on Public EC2
 sudo yum install httpd -y
 sudo systemctl enable httpd
 sudo systemctl start httpd
 
## Lessons Learned
- Difference between Security Groups (instance level) and NACLs (subnet level)
- NAT Gateway allows private instances to access the Internet securely
- Proper use of key pairs and SSH access for secure instance management
- Hands-on experience with EC2 setup, Apache installation, and connecting public & private instances
