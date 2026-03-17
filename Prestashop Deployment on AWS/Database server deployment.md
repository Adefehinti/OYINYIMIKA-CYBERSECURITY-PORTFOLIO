### DATABASE SERVER DEPLOYMENT
---

### METHODOLOGY USED

1. Log in to AWS Management Console
2. Go to EC2 Dashboard
3. In the search box, type EC2. Select it and click "Launch Instance."
4. Configure Instance

   - Name and tags: PrestaShop-Database
   - Application and OS Images (AMI): Ubuntu Server 24.04 LTS (Free tier eligible)
  

<img width="1912" height="819" alt="Screenshot 2026-03-11 152740" src="https://github.com/user-attachments/assets/f2442b62-c2ad-4803-aa6d-b829e4327a46" />


   - Instance type: t3.micro
   - Key pair: Click "Create new key pair";  Key pair name: prestashop-key; Key pair type: RSA;  Private key file format: .pem ○   "Create key pair" (file will download—save it safely!)
   - Network settings: Click "Edit"; security group name: database-sg; Description: Database security group; Inbound security group rules:  
   Rule 1: SSH, Port 22, Source: My IP  
   Rule 2: MySQL/Aurora, Port 3306, Source: application-server


<img width="1919" height="837" alt="Screenshot 2026-03-11 152804" src="https://github.com/user-attachments/assets/07a28292-3765-452c-817e-9afb54fb1f82" />

    
<img width="1908" height="811" alt="Screenshot 2026-03-11 152854" src="https://github.com/user-attachments/assets/bc83535e-6c51-4d5c-b179-ff7af5912d6c" />

   - Configure storage: 8 GB gp3 (default)
   - Launch Instance
5. Click on view all instances
6. Wait until Instance State = Running
7. Select your instance and note: Instance ID;  Public IPv4 address (for SSH access) Private IPv4 address (for database connection)
8. Connect to Database Server

   - Go to EC2 Instance Connect.
   - Click on SSH Client
   - Copy the SSH example you find on the page

<img width="1908" height="824" alt="Screenshot 2026-03-11 153308" src="https://github.com/user-attachments/assets/13a6807e-3fa0-4bd0-a5f1-7b87b95d736d" />

     
   - On windows, click the Windows key + R
   - Type `cmd`
   - Run `Cd` into the folder where you saved the key pair you downloaded earlier
   -  Paste the SSH : `ssh -i "Prestashop-key.pem" ubuntu@ec2<yourpublicip>.eu-north-1.compute.amazonaws.com`
  
  <img width="1100" height="595" alt="Screenshot 2026-03-11 153627" src="https://github.com/user-attachments/assets/adf95b6a-ab19-4c86-97db-f31717f127ad" />


   -  If you see "Are you sure you want to continue connecting?" type “yes”
9.  Install MySQL on Database Server

    - Update package list: `sudo apt update`
    - Upgrade existing packages:`sudo apt upgrade -y`
    - Install MySQL Server: `sudo apt install mysql-server -y`
    - Verify MySQL is running:`sudo systemctl status mysql`
    - Answer the prompts: Validate Password Component? N (or Y if you want strong password enforcement)
    -  Remove anonymous users? Y
    -  Disallow root login remotely? N (remote access is needed)
    -  Remove test database? Y
    -  Reload privilege tables? Y
11. Configure MySQL for Remote Access

    - run `sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`
    - Find the line: bind-address = 127.0.0.1 Change it to bind-address = 0.0.0.0

<img width="940" height="962" alt="Screenshot 2026-03-11 155458" src="https://github.com/user-attachments/assets/20f74d9a-8321-45f8-9bd9-e43b37d020d9" />



    - Save and Exit
11. Restart MySQL: `sudo systemctl restart mysql`
12. Verify it's running: `sudo systemctl status mysql`
13. Login to MySQL:

    - run `sudo mysql -u root -p `

<img width="959" height="995" alt="Screenshot 2026-03-11 160057" src="https://github.com/user-attachments/assets/fe4e9df2-79ac-4632-a843-4add9ac8fff4" />


    - Enter the password set earlier if you set one. if not, just press enter
    - Run the following command

      - `CREATE DATABASE prestashop;`
      - `CREATE USER 'prestashoptest'@'%' IDENTIFIED BY '<put password here>'; `
      - `GRANT ALL PRIVILEGES ON prestashop. * TO prestashoptest’@'%';` - This is trying to give all rights on the database to the user 
      - `FLUSH PRIVILEGES;`: Applies the changes immediately.
      - `SHOW DATABASES;`
