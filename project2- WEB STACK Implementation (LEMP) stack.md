## WEB STACK IMPLEMENTATION (LEMP STACK)
### STEP 1 – INSTALLING THE NGINX WEB SERVER
#### Steps
- To start the server update run: **Sudo apt update**
- install Nginx by running: **sudo apt install nginx**
- To confirm that nginx was successfully installed and is running as a service in Ubuntu, run: **sudo systemctl status nginx**
  
![Nginx running](https://github.com/Aml286/devops-projects/assets/124487792/3264eeab-35e8-43e2-9c9b-9eeb24a9cde2)

* Green indicator shows that the server was successfully install and running.
  - To test that the server can be accessed locally from the instance run the curl command: **curl http://localhost:80**
    ![nginx up](https://github.com/Aml286/devops-projects/assets/124487792/46bf7e52-4bcb-4446-9784-52fd663c7f32

### STEP 2 — INSTALLING MYSQL
#### Steps
- install SQL run: **sudo apt install mysql-server**
- log into MySQL: **sudo mysql**

### STEP 3 – INSTALLING PHP
#### Steps

- To install the 2 pacakages at once, run: **sudo apt install php-fpm php-mysql**

### STEP 4 — CONFIGURING NGINX TO USE PHP PROCESSOR
#### Steps
-  Now that we have PHP components installed. Next, I will configure Nginx to use them.
-  Create the root web directory for your_domain as follows:**sudo mkdir /var/www/projectLEMP**
-   **sudo chown -R $USER:$USER /var/www/projectLEMP**
-  Then, open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here, we’ll use nano: **sudo nano /etc/nginx/sites-available/projectLEMP**
- This will create a new blank file. Paste in the following bare-bones configuration:
  
```
server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }
}
```
- Activate the configuration by linking to the config file from Nginx’s sites-enabled directory, run: **sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/**
-  test your configuration for syntax errors by typing: **sudo nginx -t**
-   We need to disable default Nginx host that is currently configured to listen on port 80, for this run: **sudo unlink /etc/nginx/sites-enabled/default**
- Next, reload Nginx to apply the changes: **sudo systemctl reload nginx**
- Create an index.html file in that location so that we can test that the new server block works as expected: **sudo echo 'Hello LEMP from hostname
 ### STEP 5 – RETRIEVING DATA FROM MYSQL DATABASE WITH PHP (CONTINUED)
#### Steps 
-  The goal in this step is to create a test database (DB) with simple "To do list" and configure access to it
-  I will be creating a database named example_database and a user named example_user
-  Connect to the MySQL console using the root account: **sudo mysql**
-  To create a new database, run the following command from your MySQL console: **CREATE DATABASE `example_database`;**
-  Next, create a new user and grant him full privileges on the database. The following command creates a new user named example_user, using mysql_native_password as default authentication method. Run: **CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord1@';**
-  Next, give this user permission over the example_database database: **GRANT ALL ON example_database.* TO 'example_user'@'%';**
-  Exit the console: **exit**
-  Now test if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials: **mysql -u example_user -p**
-  After logging in to the MySQL console, confirm that you have access to the example_database database: **SHOW DATABASES;**
-  * Next, we’ll create a test table named todo_list. From the MySQL console, run the following statement:
``` 
CREATE TABLE example_database.todo_list (
item_id INT AUTO_INCREMENT,
content VARCHAR(255),
PRIMARY KEY(item_id)
);
```
![show database step6](https://github.com/Aml286/devops-projects/assets/124487792/3df52cec-4467-434f-8960-f86fcf569f93)
- Insert a few rows of content in the test table. Repeat the next command a few times, using different VALUES: **INSERT INTO example_database.todo_list (content) VALUES ("My first important item");**
-   To confirm that the data was successfully saved to your table, run: **SELECT * FROM example_database.todo_list;**
-  After confirming, exit the console: **exit**
-  Next, create a PHP script that will connect to MySQL and query for your content. Create a new PHP file in your custom web root directory using your preferred editor. We’ll use vi for that: **nano /var/www/projectLEMP/todo_list.php**
- Copy this content into your todo_list.php script:
```
<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```
- Access this page in the web browser by visiting the domain name or public IP address configured for the website, followed by /todo_list.php: **http://<Public_domain_or_IP>/todo_list.php**
  
 ![final](https://github.com/Aml286/devops-projects/assets/124487792/d8667678-5c0e-4c0f-bf5a-ea9f724625cf)









