# 🚀 PHP Image Upload Project with Nginx, PHP 8.3, RDS & Amazon S3


📄 form.html for uploading images

🧩 upload.php for saving files & metadata

🗂️ Uploads folder in EC2 server

☁️ Image storage on Amazon S3 using AWS SDK for PHP

🐬 RDS MySQL (php8.3-mysql)

📦 nginx + php8.3-fpm

-----
## 📌 1. 🔧 Install Required Packages (Ubuntu Server)
```
sudo apt update -y
sudo apt upgrade -y
sudo apt install nginx -y
sudo apt install php8.3 php8.3-fpm php8.3-mysql -y
sudo systemctl enable nginx
sudo systemctl start nginx
```
-----
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
-----
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
-----
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
-----
## 📌 5. 📦 Install Composer & AWS SDK for PHP
```
sudo curl -sS https://getcomposer.org/installer | sudo php
sudo mv composer.phar /usr/local/bin/composer
sudo ln -s /usr/local/bin/composer /usr/bin/composer
sudo composer require aws/aws-sdk-php
```
-----
## 📌 6. 🛠️ Configure AWS Credentials (Using IAM Role)
```
Instead of creating an IAM User and storing Access Keys, use an IAM Role attached directly to the EC2 instance.
```
✅ Step 1: Create IAM Role
```
Go to AWS Console → IAM → Roles
Click Create Role
Select AWS service → Choose EC2
Attach policy:
AmazonS3FullAccess (or least‑privilege policy for specific bucket)
Name the role:
EC2-S3-Access-Role
Create the role.
```
✅ Step 2: Attach IAM Role to EC2 Instance
```
Go to EC2 → Instances
Select your instance
Click Actions → Security → Modify IAM Role
Select EC2-S3-Access-Role
Save
```
-----
## 📌 7. Create files and Add Code: 

1) 📝 form.html,
2) 🧩 upload.php
```
sudo nano form.html
sudo nano upload.php
```
-----
## 📌 8. 🧪 Test Your Application:
```
Open browser:
http://YOUR-EC2-PUBLIC-IP/form.html
Try uploading an image.
Your file should:
save temporarily inside EC2 uploads/
upload to Amazon S3 bucket
save name + image URL into RDS MySQL
```
-----

🎉 DONE!

You now have a professional, production-ready PHP + Nginx + S3 upload application running on AWS EC2.

-----

📸 Recommended Screenshots to Include

1️⃣ AWS EC2

2️⃣ Nginx & Server Setup

3️⃣ RDS

4️⃣ S3 Bucket

5️⃣ Application Output

6️⃣ Project Structure

-----
## 👨‍💻 Author

## Prasad 
Cloud & DevOps Engineer

## 🤝 Connect With Me

- 🔗 [LinkedIn](http://linkedin.com/in/prasad-bhoite-a38a64223)  
- 🔗 [GitHub](https://github.com/Prasad-bhoite19)  
- 🔗 [Portfolio](https://prasad-bhoite19.github.io/prasad-portfolio/)
