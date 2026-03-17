1. Access PrestaShop Installer:

   - Open web browser
   - Navigate to `http://<public_ip of application server>`




<img width="1180" height="665" alt="Screenshot 2026-03-12 121551" src="https://github.com/user-attachments/assets/b8d7b152-5424-4fdc-8083-83452c35e9d0" />




<img width="1170" height="898" alt="Screenshot 2026-03-12 123419" src="https://github.com/user-attachments/assets/ba126e8c-1949-4f06-8d51-5953b0156195" />





   - Complete the installation wizard
   - At system configuration: set database server address (use database public IP). Do not use localhost or 127.0.0.1. The name, login, and password should be the same as the user created earlier while configuring the database server
   - Test database connection: you should see a message saying `database is connected.` Click next and complete the installation.
     



<img width="1177" height="884" alt="Screenshot 2026-03-12 131215" src="https://github.com/user-attachments/assets/bf77aff6-cf8a-4738-9975-86e61b39979d" />

     

1. Return to SSH terminal on application server
2. Remove installation directory : `sudo rm -rf /var/www/html/install`
3. Rename admin directory: `sudo mv /var/www/html/admin /var/www/html/admin_secure` (if you want to)
4. Open a web browser to access the backend and the storefront.

   - Front End Access Type:` http://<application public_ip>`




<img width="1915" height="982" alt="Screenshot 2026-03-17 120240" src="https://github.com/user-attachments/assets/668d2f9a-9393-42b7-ad23-260c8d19d23f" />


   - Back End Access Type: `http://<application public_ip>/admin`
  
     <img width="1115" height="597" alt="Screenshot 2026-02-19 125517" src="https://github.com/user-attachments/assets/154c4c04-596b-4275-aa55-5c01df0efd4d" />

     You must remove the installation directory before you can access 
the backend. 
