## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
#### Steps

Provisioning an ubuntu server on AWS
- Launched an EC2 instance
- I selected the Ubuntu free tier instance
- I set the required configurations (Enabled public IP, security group, and key pair) and finally launched the instance
- Next I SSH into the instance using Putty

### INSTALLING APACHE AND UPDATING THE FIREWALL
#### Steps
- Install Apache using Ubuntu’s package manager ‘apt'
- To update a list of packages in package manager **sudo apt update**
- To run apache2 package installation **sudo apt install apache2**
- verify that Apache2 is running as a service in the OS. run **sudo systemctl status apache2**

![apache running](https://github.com/Aml286/devops-projects/assets/124487792/b02b089b-cd45-4fdf-bf4f-b1ec59979e0c)

- Open port 80 on the Ubuntu instance to allow access from the internet.
-  Access the Apache2 service locally

  ![apache2](https://github.com/Aml286/devops-projects/assets/124487792/426bbd37-ead5-4bad-8322-c2847c5d3cec)

### INSTALLING MYSQL
#### Steps
- run: **sudo apt install mysql-server**
- Confirm intallation by typing Y when prompted
-  log in to the MySQL console by running: **sudo mysql**

  ![mysql](https://github.com/Aml286/devops-projects/assets/124487792/2cd5942a-0537-4fbd-a0e2-5d845e0aaeb8)

 - exit
### STEP 3 — INSTALLING PHP
#### Steps
- install these 3 packages at once, run  **sudo apt install php libapache2-mod-php php-mysql**
  ![php](https://github.com/Aml286/devops-projects/assets/124487792/901b22f3-14df-4db5-bbc6-e169fa564edd)

  ### STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
#### Steps
- Create the directory for projectlamp using ‘mkdir’. Run: **sudo mkdir /var/www/projectlamp**
- assign ownership of the directory with your current system user, run: **sudo chown -R $USER:$USER /var/www/projectlamp**
- create and open a new configuration file in Apache’s sites-available directory **sudo vi /etc/apache2/sites-available/projectlamp.conf**
- This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:
**<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>**
  -  use a2ensite command to enable the new virtual host: **sudo a2ensite projectlamp**
  - Disable the default website that comes installed with Apache. type: **sudo a2dissite 000-default**
  - Esure your configuration file doesn’t contain syntax errors, run: **sudo apache2ctl configtest**
  - reload Apache so these changes take effect: **sudo systemctl reload apache2**

### STEP 5 — ENABLE  WEBSITE

![final static website](https://github.com/Aml286/devops-projects/assets/124487792/e5bf0f4b-0938-4ccb-80c6-8dacc7e6d7e5)

  





