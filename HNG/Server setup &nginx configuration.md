## Server Setup & Nginx Configuration
---
## Overview

This project involves provisioning a Linux server on AWS EC2, create a non-root user called hngdevops with sudo privileges, disabling root SSH login, Configure UFW to allow only ports 22, 80, and 443 (all other ports closed) configuring Nginx as a web server, securing it with SSL and hardening it following security best practices.

## What Was Built

- A live server running on **AWS EC2** (Ubuntu 22.04 LTS)
- **Nginx** configured to serve two endpoints:
  - `GET /` → Static HTML page displaying HNG username
  - `GET /api` → JSON response with track and username info
- **HTTPS** secured with a valid Let's Encrypt SSL certificate
- **HTTP → HTTPS** redirect with 301 status code
- **UFW Firewall** configured to allow only ports 22, 80 and 443
- **SSH hardened** — root login disabled, password auth disabled
- Non-root user `hngoyinyimika` with sudo privileges configured

## Tools used

- AWS EC2 - Cloud Servie Provider
- Ubuntu 22.04 LTS - Server Operating Syatem
- Nginx - Web Server
- Certbot + Let's Encrypt - SSL certificate
- UFW - Firewall
- DuckDns - Free Domain name.

## Procedures
---
1. Create an AWS Account
2. Launch EC2 instance

   - Name server - hng-sever
   - Applicatin and OS image - Ubunu Server
   - Instance type - t2.micro
   - Create SSH key pair

     - Under key pair, click edit
     - give it a name (hng-key)
     - key pair type: RSA
     - Private key format (.pem)
     - create key pair
    - configure network settings

      - Allow ssh traffic from anywhere (port 22)
      - Allow HTTP traffic from anywhere (port 80)
      - Allow HTTPs traffic from anywhere (port 443)

<img width="1919" height="890" alt="Screenshot 2026-04-14 121902" src="https://github.com/user-attachments/assets/45d280be-1a65-44dc-b15f-9f6dc7b423bc" />


    - storage - 8 GiB gp2
    - Launch the instance

2. Connect to the server from laptop cmd

   - on EC2 dashboard
   - Click on the created instance
   - click connect
   - click ssh-client
   - copy the example you find on the page
   - open your cmd
   - go into the folder where you stored the key-pair
   - paste the ssh command

<img width="1110" height="619" alt="Screenshot 2026-04-14 122810" src="https://github.com/user-attachments/assets/92298d7e-6194-42aa-8371-c14b80093adc" />
     

  3. update the server `sudo apt update && sudo apt upgrade -y`
  4. Create the new user `sudo useradd hngoyinyimika`




<img width="945" height="328" alt="Screenshot 2026-04-15 162703" src="https://github.com/user-attachments/assets/ced509c0-6ad6-442c-a9bf-f705bf495264" />


  6. GIve the user sudo privilege `sudo usermod -aG sudo hngoyinyimika`
  7. Give the user SSH Access

     - create .ssh directory for the user `sudo mkdir -p /home/hngoyinyimika/.ssh`
     - Copy the authorized key from the ubuntu user `sudo cp /home/ubuntu/.ssh/authorized_key /home/hngoyinyimika/.ssh/authorized_keys`
     - Give the user ownership of these files `sudo chown -R hngoyinyimika:hngoyinyimika /home/hngoyinyimika/.ssh`
     - set correct permissions `sudo chmod 700 /home/hngoyinyimika/.ssh` `sudo chmod 600 /home/hngoyinyimika/.ssh/authorized_keys`

       <img width="1019" height="259" alt="Screenshot 2026-04-15 162731" src="https://github.com/user-attachments/assets/ce5252f0-fc97-4613-a09b-7b9a65158c4e" />

 
  
  
  8. Configure Passwordless sudo for specific commands `sudo visudo -f /etc/sudoers.d/hngoyinyimika`

     - This opens a text editor in the terminal and type
       `hngoyinyimika ALL=(root) NOPASSWD:/usr/sbin/sshd, /usr/sbin/ufw`
      save and exit
       <img width="1098" height="576" alt="Screenshot 2026-04-14 134341" src="https://github.com/user-attachments/assets/2e7507f2-fe23-42c6-9832-c54b60822c6d" />

 
   9. Harden SSH security `sudo nano /etc/ssh/sshd_config`

      - search `PermitROOTlogin` and set to no
      - serach `Password Authentication` and set to no
      - search `PubkeyAuthentication` and set to Yes
        
<img width="1095" height="605" alt="Screenshot 2026-04-14 135033" src="https://github.com/user-attachments/assets/aa88ba4b-e6cc-4ae9-96bd-9e7cb87e7792" />
<img width="1106" height="611" alt="Screenshot 2026-04-14 134526" src="https://github.com/user-attachments/assets/693635b7-a471-420d-bab9-80e47d1a6e66" />


     - Restart SSH to apply changes `sudo systemctl restart sshd`
   9. Open a new terminal and test logging in as the new user
   10. While logged in as the user, configure UFW firewall

       ```
       sudo ufw allow 22
       sudo ufw allow 80
       sudo ufw allow 443
       sudo ufw enable
       ```
       
<img width="798" height="176" alt="Screenshot 2026-04-15 163309" src="https://github.com/user-attachments/assets/251f4af2-922d-4948-a154-53b84eb276a3" />




       
   11. Get a domain. I got a free domain from duckdns.org
   12. Point your domain to the server. (for duckdns.org, just copy your server public ip from aws and update it with the ip given by duckdns)
   13. Confirm your domain resolves to your ip by doing `nslookup hngoyinyimika.duckdns.org`
   14. Install Nginx. Back on the server as hngoluwaferanmi

       - `sudo apt install nginx -y`
       - check if it is running `sudo systemctl status nginx`




<img width="1110" height="377" alt="Screenshot 2026-04-14 142307" src="https://github.com/user-attachments/assets/e4b8abbe-e357-4c5e-83cb-1fe64d6ffb3a" />


       - Open browser and visit `http://hngoyinyimika.duckdns.org` This should show the defaault welcome to nginx page.
      



         <img width="1887" height="1007" alt="Screenshot 2026-04-14 144540" src="https://github.com/user-attachments/assets/3791b439-12b2-4be9-8aad-482751abdd62" />


  14. Create HTML page

      - create the folder `sudo mkdir -p /var/www/mysite`
      - create and open the HTML file `sudo nano /var/www/mysite/index.html`
      - fill with your html code
   ```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>server setup</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .card {
            background: white;
            padding: 40px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h1 { color: #333; }
        p { color: #666; }
    </style>
</head>
<body>
    <div class="card">
        <h1>HNG DevOps Track</h1>
        <p>Username: <strong>I am Oyinyimika Devops specialits strong></p>
        <p>Stage 0 - Server Setup & Nginx Configuration</p>
    </div>
</body>
</html>
```
<img width="780" height="500" alt="Screenshot 2026-04-14 145527" src="https://github.com/user-attachments/assets/d0cec048-9957-4733-9cd2-719fa794dff1" />

  17. Configure nginx `sudo nano /etc/nginx/sites-available/mysite` fill it with
```
server {
    listen 80;
    server_name hngoyinyimika.duckdns.org;

    root /var/www/mysite;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Return JSON at /api
    location /api {
        default_type application/json;
        return 200 '{"message": "HNGI14 Stage 0", "track": "DevOps", "username": "OyinyimikaAdefehinti"}';
    }
}
```



<img width="1109" height="623" alt="Screenshot 2026-04-14 151232" src="https://github.com/user-attachments/assets/11f92099-015d-414b-8f52-4e00cd8d8f9d" />


  18. Enable the new config `sudo ln -s /etc/nginx/sites-available/mysite /etc/nginx/sites-enabled/`
  19. Disable the default site `sudo rm /etc/nginx/sites-enabled/default`
  20. Test config for errors `sudo nginx -t` --> you should see test is successful
  21. Get SSL certificate from let's encrypt

      - Install certbot `sudo apt install certbot python3-certbot-nginx -y`
      - get certificate `sudo certbot --nginx -d hngoyinyimika.duckdns.iorg`
      - Enter your email
      - Agree to terns (Y)
      - Shere email with EFF (N)
        Certbot will automatically get your certificate and update nginx config. you should see successfully received certificate
  22. Reload nginx `sudo systemctl reload nginx`
  23. Test setup

      - test HTTPS homepage `https://hngoyinyimika.duckdns.org` - should show your HTML page



<img width="1918" height="985" alt="Screenshot 2026-04-14 161301" src="https://github.com/user-attachments/assets/6973deb5-c7d3-4af6-93a6-c733b63a0b48" />

        
      - test API endpoint `https://hngoluwaferanmi.duckdns.org/api` - should return json file

        

      -  test HTTP redirect `http://hngoluwaferanmi.duckdns.org` -should automatically redirect to `https://`
      
      


         




    
       

       
