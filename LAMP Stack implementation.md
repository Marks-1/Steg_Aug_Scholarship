# LAMP Stack Implementation on AWS

## Introduction
The LAMP stack—**Linux, Apache, MySQL, and PHP**—is a popular open-source web development platform for hosting dynamic websites and applications. On AWS, it can be implemented by provisioning an **EC2 instance** (Linux-based) and configuring it with Apache (web server), MySQL/MariaDB (database), and PHP (server-side scripting). AWS offers flexibility to deploy LAMP using manual installation on EC2, Amazon RDS for managed databases, or pre-configured Amazon Machine Images (AMIs). This setup leverages AWS’s scalability, security, and availability, making it ideal for hosting modern, database-driven web applications.

---

## Step-by-Step LAMP Setup on AWS

### 1. **Launch an EC2 Instance**
- Log in to the [AWS Management Console](https://aws.amazon.com/console/).
- Navigate to **EC2 → Launch Instance**.
- Choose an **Ubuntu Server** (e.g., Ubuntu 22.04 LTS) AMI.
- Select an instance type (e.g., `t2.micro` for Free Tier).
- Create/choose a key pair for SSH access.

<img width="574" height="494" alt="image" src="https://github.com/user-attachments/assets/cbc3f1de-e92c-462f-8a14-10353426a8bf" />

- Configure security groups:
  - Allow inbound traffic on ports **22** (SSH), **80** (HTTP), and **443** (HTTPS).
- Launch the instance.

<img width="664" height="481" alt="image" src="https://github.com/user-attachments/assets/443f46b3-0488-47dc-a337-52a443e7840b" />

### 2. **Connect to the EC2 Instance**
```bash
ssh -i /path/to/keypair.pem ubuntu@<EC2_Public_IP>
```
<img width="539" height="347" alt="image" src="https://github.com/user-attachments/assets/250cbb50-c75f-473b-91d4-5c6702f8a080" />

### 3. **Update packages**
```bash
sudo apt update && sudo apt upgrade -y
```
<img width="685" height="156" alt="image" src="https://github.com/user-attachments/assets/dec9ba14-ab51-41f7-9eb1-fcefdcf7b94c" />

<img width="1697" height="371" alt="image" src="https://github.com/user-attachments/assets/2902f3e2-97d6-48e9-8b67-6394ee1a7b67" />

### 4. **Install Apache and confirm status**
```bash
sudo apt install apache2 -y
sudo systemctl status apache2
```

<img width="875" height="172" alt="image" src="https://github.com/user-attachments/assets/4aacf69f-2f92-41ae-93a1-c8eb81b7f3dd" />

<img width="610" height="182" alt="image" src="https://github.com/user-attachments/assets/d37c2302-ea37-46ac-adba-268d8d411266" />

Testing the server for both local and internet connection requests

Local server test
```bash
curl http://localhost:80
```
<img width="706" height="152" alt="image" src="https://github.com/user-attachments/assets/0b9ec5cc-27a8-4506-a866-bdc9ff1e0a19" />

Requests from the internet
```bash
http://3.80.31.125:80
```
<img width="719" height="445" alt="image" src="https://github.com/user-attachments/assets/9c9094a4-fdf7-4e50-aca3-cf2247554ddf" />

### 5. **Install MySQL**
Once your web server is running, you’ll need to set up a Database Management System (DBMS) to store and manage your site’s data in a relational database. 
In this project, we’ll use MySQL, a popular relational database system commonly used with PHP.

To install MySQL, run:
```bash
$ sudo apt install mysql-server
```
<img width="691" height="110" alt="image" src="https://github.com/user-attachments/assets/a97f6c61-bc00-4c8f-93c8-52aed537f4ba" />

After the installation is complete, access the MySQL console by running:
```bash
$ sudo mysql
```

This connects you as the root administrative user via sudo. You should see the MySQL welcome prompt appear.
<img width="505" height="130" alt="image" src="https://github.com/user-attachments/assets/c39170f6-adfd-4776-8839-5c52e1ddc54e" />

It’s advisable to run the built-in MySQL security script to remove insecure defaults and protect your database. Before running it, set a password for the root user, using mysql_native_password as the authentication method:

<img width="509" height="55" alt="image" src="https://github.com/user-attachments/assets/f2bbe936-b285-404e-88f9-8d5666af1b12" />

When done, exit the MySQL shell:
```bash
mysql> exit
```
Run the MySQL security setup tool by entering:
```bash
$ sudo mysql_secure_installation
```
You’ll be prompted about enabling the VALIDATE PASSWORD PLUGIN, which checks and enforces password strength.

Enabling it ensures only strong passwords are accepted.

If disabled, MySQL won’t enforce complexity, but you should still use secure, unique passwords.

Press y to enable or any other key to skip.

If enabled, you’ll need to choose a password validation policy:

0 – Low: At least 8 characters.

1 – Medium: At least 8 characters, including numbers, uppercase and lowercase letters, and special characters.

2 – Strong: Same as Medium, plus checks against dictionary words.
<img width="556" height="298" alt="image" src="https://github.com/user-attachments/assets/9e166b7c-5117-4650-b1ce-bfb9b3e58844" />

When done, you can test if able to log in to the MySQL console using:
```bash
$ sudo mysql -p
```

N/B: The ```-p``` flag will prompt for the password after changing the **root** user password.

Exit MySQL using:
```bash
mysql> exit
```

### 6. **Install PHP**
Having successfully set up a LAMP stack, which includes Apache to serve web content, MySQL for database management, and PHP to handle dynamic content. To enable PHP to interact with MySQL and allow Apache to process PHP files, you'll need to install the php, php-mysql, and libapache2-mod-php packages. These can be installed simultaneously with the following command:

```bash
$ sudo apt install php libapache2-mod-php php-mysql
```
<img width="792" height="155" alt="image" src="https://github.com/user-attachments/assets/b2357799-8e06-49ae-8a4d-78c133633c4b" />

After installation, verify your PHP version by running:
```bash
$ php -v
```
<img width="434" height="50" alt="image" src="https://github.com/user-attachments/assets/728fefa0-19bc-41fc-83a4-f78a3ed19aab" />

With these components installed, your LAMP stack is fully functional:

Linux (Ubuntu)

Apache HTTP Server

MySQL

PHP

To further test your setup, consider configuring an Apache Virtual Host. This allows you to host multiple websites on a single server seamlessly, ensuring an organized and professional web hosting environment.

### 7. **Creating a VirtualHost for your website using Apache**
By default, Apache on Ubuntu 20.04 serves content from /var/www/html. We’ll keep this default setup while adding a new directory for our project alongside it.

First, create the directory for projectlamp:
```bash
$ sudo mkdir /var/www/projectlamp
```
Next, assign ownership of the directory to your current system user using the $USER environment variable:

```bash
$ sudo chown -R $USER:$USER /var/www/projectlamp
```
Then, create and edit a new Apache configuration file in the sites-available directory. You can use vi or vim (which are essentially the same):

```bash
$ sudo vi /etc/apache2/sites-available/projectlamp.conf
```
This will open a blank file. Press `i` to enter insert mode, then you need to add the basic configuration as shared

<img width="617" height="212" alt="image" src="https://github.com/user-attachments/assets/db3b2695-f3c4-4f0a-aa6a-a1fd1da375ba" />

Press `Esc` and then type `:` followed by `wq` to close and save the vi file.

Run the below command to confirm the available sites:
```bash
$ sudo ls /etc/apache2/sites-available
```
<img width="571" height="38" alt="image" src="https://github.com/user-attachments/assets/e55a49e8-0aac-4486-9dfc-1f2564a76858" />

To enable the new projectlamp site, run the following command:
```bash
$ sudo a2ensite projectlamp
```
<img width="461" height="62" alt="image" src="https://github.com/user-attachments/assets/e8c44709-f47c-4b39-939f-7190692e6cac" />


To disable the default website content that comes installed with Apache, run the following command:
```bash
$ sudo a2dissite 000-default
```
<img width="460" height="52" alt="image" src="https://github.com/user-attachments/assets/582d5e05-7dbd-4a51-8cda-2fb5736b79d0" />

Confirm if the configuration file has no syntax errors by running:
```bash
$ sudo apachectl2 configtest
```
<img width="462" height="52" alt="image" src="https://github.com/user-attachments/assets/2af47d4d-f927-4a9e-ab66-8393b5971683" />

Once confirmed to be error-free, you need to reload the Apache2 server for the changes to take effect:
```bash
$ sudo systemctl reload apache2
```
To test the VirtualHost and the Apache2 server, we'll create an index.html file in the projectlamp folder, since it is still empty.
```bash
$ sudo echo '<h1>Hello, World!</h1>' > /var/www/projectlamp/index.html
```
<img width="551" height="79" alt="image" src="https://github.com/user-attachments/assets/acbe75d1-7806-45fc-817c-bf5ecc8a3914" />

Then, with the EC2 public IP, go to the browser to test if the index.html file will load its content. Should show the Hello, World.
```bash
http://<Public_ip>:80
```
<img width="740" height="172" alt="image" src="https://github.com/user-attachments/assets/697cfcd1-259b-4a10-a145-099d0ce5ff6f" />

### 8. **Enable PHP on the website**
## Configuring PHP Priority and Testing
By default, Apache prioritizes index.html over index.php. This is useful for maintenance pages—simply add an index.html file, and it will temporarily replace your PHP application. To change this behavior, modify the DirectoryIndex directive in /etc/apache2/mods-enabled/dir.conf:
```bash
$ sudo vi /etc/apache2/mods-enabled/dir-conf
```
You only need to have the `index.php` precede the `index.html` by updating the file as below.
<img width="612" height="253" alt="image" src="https://github.com/user-attachments/assets/6d101697-63b0-4e85-be17-f593a33ceefd" />

Once done, press `Esc` and then `:wq` to save and quit the vi mode.

Then reload the Apache for the changes to take effect.
```bash
$ sudo systemctl reload apache2
```

## Testing PHP
To verify PHP works, create a test file in your project's root directory:
```bash
$ sudo vi /var/www/projectlamp/index.php
```
Add the following PHP code:
```bash
<?php phpinfo();
```
<img width="595" height="253" alt="image" src="https://github.com/user-attachments/assets/add263a1-c492-43af-9f2c-fc845d1489b2" />

This will display server PHP information when accessed via a browser, confirming proper setup.

<img width="851" height="319" alt="image" src="https://github.com/user-attachments/assets/d38b2ef4-48b7-44c9-9468-76a30fb11a1d" />

