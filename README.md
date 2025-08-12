# LAMP Stack Deployment on AWS

This guide provides step-by-step instructions for setting up a LAMP (Linux, Apache, MySQL, PHP) stack on AWS using an **EC2 Ubuntu 22.04** instance.

---

## 1. Launching the EC2 Instance

1. Log into your AWS Management Console and navigate to **EC2** → **Launch Instance**.
2. Set the following configurations:
   - **Instance Name:** `Ubuntu-ec2-server`
   - **AMI:** Ubuntu Server 22.04 LTS (64-bit x86/ARM)
   - **Instance Type:** `t2.micro` (Free Tier eligible)
3. Create or select an existing key pair:
   - If creating a new key pair, name it `server-keypair`.
4. Configure networking:
   - Attach the instance to the desired VPC/Subnet.
   - Enable a **Security Group** allowing inbound traffic for:
     - **SSH** (port 22) from your IP.
     - **HTTP** (port 80) from anywhere.
5. Launch the instance.

---

## 2. Connecting to the Instance

```bash
chmod 400 server-keypair.pem
ssh -i server-keypair.pem ubuntu@<EC2-Public-IP>
```

Replace `<EC2-Public-IP>` with your instance's public IP address.

---

## 3. Installing Apache

```bash
sudo apt update
sudo apt install apache2 -y
```

Verify Apache is running by visiting `http://<EC2-Public-IP>` in your browser.

---

## 4. Installing MySQL

```bash
sudo apt install mysql-server -y
sudo mysql_secure_installation
```

During configuration, set a root password and adjust security settings as prompted.

---

## 5. Installing PHP

```bash
sudo apt install php libapache2-mod-php php-mysql -y
```

Check PHP version:

```bash
php -v
```

---

## 6. Testing PHP with Apache

1. Create a PHP info file:

```bash
sudo nano /var/www/html/info.php
```

2. Add the following:

```php
<?php
phpinfo();
?>
```

3. Save and exit.  
4. Access it via: `http://<EC2-Public-IP>/info.php`

---

## 7. Final Steps

- Remove `info.php` after testing for security purposes:
```bash
sudo rm /var/www/html/info.php
```
- Your LAMP stack is now ready for hosting web applications.

---
