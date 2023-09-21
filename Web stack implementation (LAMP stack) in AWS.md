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
- 






