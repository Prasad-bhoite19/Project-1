# 🚀 PHP Image Upload Project with Nginx, PHP 8.3, RDS & Amazon S3

A fully production-ready Cloud & DevOps project demonstrating PHP 8.3, Nginx, MySQL (RDS), S3 Image Storage, Linux commands, IAM role setup, AWS deployment, troubleshooting, Docker, CI/CD, architecture diagrams (placeholder), screenshots section, author section, and more.

📄 form.html for uploading images

🧩 upload.php for saving files & metadata

🗂️ Uploads folder in EC2 server

☁️ Image storage on Amazon S3 using AWS SDK for PHP

🐬 RDS MySQL (php8.3-mysql)

📦 nginx + php8.3-fpm


## 📌 Project Overview

This project uploads an image using a PHP form. The image is stored in Amazon S3, and metadata (name, filename, timestamp) is stored in Amazon RDS. Nginx is used as a web server on an Ubuntu EC2 instance.



## 🎯 Objectives / Goals

Learn PHP 8.3 with Nginx

Upload files securely to Amazon S3

Store data in Amazon RDS (MySQL)

Configure IAM role for S3 access

Build Cloud Architecture

Deploy on EC2 Ubuntu

Practice real workflow

Improve resume with a real Cloud project



## ⚙️ Architecture Diagram
~~~
User -> Nginx -> PHP 8.3 -> RDS (MySQL)
                    \
                      -> S3 Bucket

~~~
## 🛠️ Technologies Used


AWS (EC2, S3, RDS, IAM, VPC)

PHP 8.3

Nginx

MySQL

Ubuntu Linux

Composer + AWS SDK


## 🧰 Prerequisites

AWS Account

EC2 Ubuntu Instance

IAM Role for S3

RDS MySQL Instance

S3 Bucket

PHP 8.3 + Extensions

Composer


## 📌 1. 🔧 Install Required Packages (Ubuntu Server)
```
sudo apt update -y
sudo apt upgrade -y
sudo apt install nginx -y
sudo apt install php8.3 php8.3-fpm php8.3-mysql -y
sudo systemctl enable nginx
sudo systemctl start nginx
```

## 📌 2. 🗃️ Install & Configure MariaDB / MySQL
```
sudo apt install mariadb-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb
```
Create Database
```
sudo mysql -u admin -p -h (Paste Your RDS endpoint here)
CREATE DATABASE facebook;
USE facebook;

CREATE TABLE posts (
  pid INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  url VARCHAR(500)
);
```

## 📌 3. 🌐 Configure Nginx for PHP
```
Edit Nginx config:
sudo nano /etc/nginx/sites-available/default
```
Replace with:
```
server {
    listen 80;
    server_name _;
    
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.3-fpm.sock;
    }

```
Restart nginx:
```
sudo systemctl restart nginx
```

## 📌 4. 📁 Create Project Structure
```
/var/www/html/
 ├── form.html
 ├── upload.php
 └── uploads/  (folder for temporary images)
```
Create uploads directory:
```
sudo mkdir /var/www/html/uploads
sudo chmod 777 /var/www/html/uploads
```

## 📌 5. 📦 Install Composer & AWS SDK for PHP
```
sudo curl -sS https://getcomposer.org/installer | sudo php
sudo mv composer.phar /usr/local/bin/composer
sudo ln -s /usr/local/bin/composer /usr/bin/composer
sudo composer require aws/aws-sdk-php
```

## 📌 6. 🛠️ Configure AWS Credentials (Using IAM Role)

Instead of creating an IAM User and storing Access Keys, use an IAM Role attached directly to the EC2 instance.

**✅ Step 1: Create IAM Role**

➡️ Go to AWS Console → IAM → Roles

➡️ Click Create Role

➡️ Select AWS service → Choose EC2

Attach policy:

➡️ AmazonS3FullAccess (or least‑privilege policy for specific bucket)

➡️ Name the role:

➡️ EC2-S3-Access-Role

➡️ Create the role.

**✅ Step 2: Attach IAM Role to EC2 Instance**

➡️ Go to EC2 → Instances

➡️ Select your instance

➡️ Click Actions → Security → Modify IAM Role

➡️ Select EC2-S3-Access-Role

➡️ Save


## 📌 7. Create files and Add Code: 

1) 📝 form.html
2) 🧩 upload.php
   
```
sudo nano form.html
sudo nano upload.php
```

## 📌 8. 🧪 Test Your Application:

➡️ Open browser:

http://YOUR-EC2-PUBLIC-IP/form.html

➡️ Try uploading an image.

Your file should:

save temporarily inside EC2 uploads/

upload to Amazon S3 bucket

save name + image URL into RDS MySQL


🎉 DONE!

You now have a professional, production-ready PHP + Nginx + S3 upload application running on AWS EC2.


## 🌥️ AWS Deployment Guide

Launch EC2

Install PHP, Nginx, Composer

Connect RDS

Attach IAM Role

Deploy files

Restart services



## 🔐 Security Best Practices

Use IAM Roles instead of access keys

Restrict Security Groups

Use HTTPS with Certbot

Disable public RDS access


## 📸 Recommended Screenshots to Include

1️⃣ AWS EC2

2️⃣ Nginx & Server Setup

3️⃣ RDS

4️⃣ S3 Bucket

5️⃣ Application Output

6️⃣ Project Structure


## 🧪 Testing

Upload different file sizes

Test invalid formats

Test RDS connection failure


## 🧹 Troubleshooting

404 error → Check Nginx root path

RDS timeout → Check SG inbound rules

S3 upload fail → Check IAM role permissions


## 👨‍💻 Author

## Prasad 
Cloud & DevOps 

- 🔗 [LinkedIn](http://linkedin.com/in/prasad-bhoite-a38a64223)  
- 🔗 [GitHub](https://github.com/Prasad-bhoite19)  
- 🔗 [Portfolio](https://prasad-bhoite19.github.io/prasad-portfolio/)
