### APPLICATION SERVER DEPLOYMENT
---
### METHODOLOGY USED
1. Launch Application EC2 Instance
2. Return to EC2 Dashboard
3. Launch Instance
4. Configure Instance

   - Name and tags: PrestaShop-Application
   - Application and OS Images (AMI): Ubuntu Server 24.04 LTS
  

     

     <img width="1914" height="886" alt="Screenshot 2026-03-11 111004" src="https://github.com/user-attachments/assets/03a99e37-f92d-43fa-a948-8f9dd0345e31" />


   - Instance type: t3.micro
   - Key pair: Select prestashop-key (same key as database)
   - Network settings: Click "Edit."
   - Security group name: application-sg
   - Description: Application security group
   - Inbound security group rules: 
Rule 1: SSH, Port 22, Source: My IP
Rule 2: HTTP, Port 80, Source: Anywhere (0.0.0.0/0) 
Rule 3: HTTPS, Port 443, Source: Anywhere (0.0.0.0/0)
   - Configure storage: 8 GB gp3
   -  Launch the instance and wait until the instance state says "Running."
5. Update Security Groups Configure

   - Go to EC2 and navigate to Security Groups
   - Select database-sg (It was created earlier)
   - Right-click and click "Edit inbound rule."
   - Delete the initial rule that allowed MySQL from "Anywhere."
   - Click "Add rule." 
   Type: MySQL/Aurora  
   Port Range: 3306  
   Source: Custom - Select application-sg
   - Save rules (The updated rule ensures my application server can access the database.)
  



<img width="1913" height="728" alt="Screenshot 2026-03-11 112124" src="https://github.com/user-attachments/assets/9ab0472a-fada-4755-afd8-bea1d6a9915b" />










6. Connect to Application Server On Windows: windows key + R, cd to the folder of the key pair and enter `ssh -i "Prestashop-key.pem" ubuntu@ec2<your application server publicip>.eu-north-1.compute.amazonaws.com`
7. Install Apache Web Server

    - `sudo apt update`
    - ` sudo apt upgrade -y`
    - `sudo apt install apache2 -y`

8.  Enable and start Apache: `sudo systemctl enable apache2 sudo systemctl start apache2`
9.  Check apache status: “sudo systemctl status apache2”





<img width="943" height="774" alt="Screenshot 2026-03-11 170511" src="https://github.com/user-attachments/assets/cb074e04-7d04-48ba-91a1-3b36272bccb6" />

    

11.  Test Apache: Open browser and go to `http://<public-ip>` You should see the Apache default page.

      <img width="1856" height="894" alt="Screenshot 2026-03-11 170854" src="https://github.com/user-attachments/assets/056ecd96-53eb-4b0e-a73e-8d8236543219" />


12.  Install PHP and all required extensions:
 ```
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd
php-intl php-mbstring php-xml php-zip php-bcmath php-json php-soap unzip -y”
```
12. Verify PHP installation: `Php -v`
13. Configure Apache for PrestaShop
       
    - Enable Apache rewrite module: `sudo a2enmod rewrite`
    - Restart Apache: `sudo systemctl restart apache2`
    - Install MySQL client : `sudo apt install mysql-client -y`
    - Test connection: `“mysql -h <your database server publicip> -u oluwaferanmi` (the user created earlier) -p
    - If successful, you'll see MySQL prompt.

      
14. Download PrestaShop

    - Go to web directory: cd /var/www/html
    - Download PrestaShop: `sudo wget https://github.com/PrestaShop/PrestaShop/releases/download/8.1.7/prestashop_8.1.7.zip`
    - Unzip main file : `sudo unzip prestashop_8.1.7.zip`
    - If it returns an error saying “zip command not found,” that means the zip tool is missing. Install the zip tools: `sudo apt install zip tools`
    - Unzip inner prestashop.zip: `sudo unzip prestashop.zip`
    - When prompted: replace index.php? [y]es, [n]o, [A]ll, [N]one, [r]ename: A # Type A and press Enter
    - Remove Apache default page: `sudo rm index.htmL`
    - Set correct permissions:
    ```
    sudo chown -R www-data:www-data /var/www/html 
    sudo chmod -R 755 /var/www/html

    ```
15. Configure Apache Virtual Host

    - Create virtual host configuration : `sudo nano /etc/apache2/sites-available/prestashop.conf`
    - Copy and paste this configuration 
```
<VirtualHost *:80>  
         ServerAdmin admin@localhost  
         DocumentRoot /var/www/html 
 
  <Directory /var/www/html> 
         Options FollowSymLinks  
          AllowOverride All 
         Require all granted 
  </Directory> 
ErrorLog ${APACHE_LOG_DIR}/error.log  
CustomLog ${APACHE_LOG_DIR}/access.log combined 
</VirtualHost>
```

<img width="835" height="313" alt="Screenshot 2026-03-12 105247" src="https://github.com/user-attachments/assets/4d328fe6-f132-4014-bba2-4dc15b6a1a21" />


16. Disable default site : `sudo a2dissite 000-default.conf`
17. Enable PrestaShop site: `sudo a2ensite prestashop.conf`
18. Test configuration : `sudo apache2ctl configtest`
19. Restart Apache: `sudo systemctl restart apache2`

    
