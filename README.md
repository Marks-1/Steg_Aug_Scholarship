# LAMP Stack Deployment on AWS
#### A Step-by-Step Guide to Deploying Linux, Apache, MySQL, and PHP on AWS EC2

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Launching EC2 Instance](#1-launching-ec2-instance)
3. [Connecting to Instance](#2-connecting-to-instance)
4. [Installing LAMP Stack](#3-installing-lamp-stack)
5. [Configuring MySQL](#4-configuring-mysql)
6. [Testing PHP](#5-testing-php)
7. [Optional: Domain Setup](#6-optional-domain-setup)
8. [Security Best Practices](#7-security-best-practices)
9. [Maintenance](#8-maintenance)
10. [Troubleshooting](#9-troubleshooting)

---

## Prerequisites
- AWS account (free tier eligible)
- Basic Linux command line knowledge
- SSH client (Terminal on Mac/Linux, PuTTY on Windows)

---

## 1. Launching EC2 Instance

### Step-by-Step:
1. Log in to AWS Management Console
2. Navigate to EC2 Dashboard
3. Click "Launch Instance"
4. Choose an AMI:
   - **Amazon Linux 2 AMI** (recommended)
   - OR **Ubuntu Server 20.04 LTS**
5. Select instance type:
   - `t2.micro` (free tier eligible)
6. Configure instance:
   - Keep default VPC
   - Enable auto-assign public IP
7. Add storage:
   - 8GB SSD (default)
8. Configure Security Group:
   - Add rule: HTTP (port 80)
   - Add rule: SSH (port 22) - restrict to your IP
9. Review and launch
10. Create/download new key pair (.pem file)

---

## 2. Connecting to Instance

### For Linux/Mac:
```bash
chmod 400 your-key.pem
ssh -i "your-key.pem" ec2-user@your-instance-public-ip
