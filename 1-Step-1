Step 1: Install Raspbian
-----
Begin by installing Raspbian onto your SD card, following the usual process you would use for any Raspberry Pi project that runs on Raspbian. 
If you need a reminder on how to set up the operating system, you can search and refer to guide on "How to install Raspbian on a Raspberry Pi" for step-by-step instructions.

Step 2: Install Nginx
-----
In the LEMP stack, the letter "E" actually refers to nginx (pronounced "engine-x"). Now, let’s proceed to install nginx on the Raspberry Pi.

First, open the Terminal, and run the following commands one by one to update the package list and install nginx:

sudo apt-get update  
sudo apt-get install nginx  

If asked for confirmation during installation, just type yes and press Enter to continue.

Nginx is the core web server in this setup — well-known for its high performance and lightweight nature. Once installed, it will handle all the web traffic to and from your Raspberry Pi.

Step 3: Install MySQL
-----
To store and manage data for our website, we need to install MySQL, a popular database management system. Similar to nginx, installing MySQL on your Raspberry Pi is simple and can be done using a few commands in the terminal.

First, open the terminal and run this command to install MySQL:

sudo apt-get install mysql-server

During the installation process, you will be prompted to create a root password. You may choose to leave it blank if you prefer not to set a password at this stage.

Once the installation is complete, it is important to secure your MySQL setup by running the following command:

sudo mysql_secure_installation

Here, you will be given the option to change the root password — since you have just set it (or left it blank), you can choose "No". For the other questions, it is recommended to answer "Yes" to ensure better security.

Step 4: Install PHP
-----
Now we’ve reached the last part of the LEMP stack — PHP! PHP is essential for handling dynamic content on your website. To begin, open your terminal and run the following command to install PHP along with the MySQL extension:

sudo apt-get install php5-fpm php5-mysql

Next, we need to adjust PHP’s configuration to improve security. To do this, open the PHP settings file using this command:

sudo nano /etc/php5/fpm/php.ini

Inside the file, look for this line:

   #cgi.fix_pathinfo=1

   Change it to:

   cgi.fix_pathinfo=0

To search quickly, press Ctrl + W, type part of the line, and hit Enter. After making the change, press Ctrl + X to exit, then press Y to save the file.

Finally, restart PHP to apply the new settings:

sudo systemctl restart php5-fpm

Now PHP is installed and secured, ready to work with your web server!

Step 5: Configure nginx to Work with PHP
-----
Now, let’s configure nginx to work properly with PHP. To do this, we need to edit the nginx configuration file. Open the file using this command:

sudo nano /etc/nginx/sites-available/default

Inside this file, you will need to make some adjustments. Edit the file so that it looks like the following:

server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;

    index index.php index.html index.htm index.nginx-debian.html;

    server_name [your public IP];

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}

⚙️ Note: Replace [your public IP] with your actual public IP address. You can find this by searching "what is my IP" on Google or other search engines.

Once you’ve updated the file, save and close it.

Next, check to make sure the nginx configuration is correct:

sudo nginx -t

If there are no errors, reload nginx to apply the new settings:

sudo systemctl reload nginx

✅ That's it! You’ve successfully configured nginx to handle PHP on your Raspberry Pi.


Step 6: Configure Port Forwarding
-----
To make your Raspberry Pi web server accessible from the internet, you need to set up port forwarding on your router. Here’s how to do it:

1. First, log in to your router’s admin page. To do this, open a web browser and type in your router’s private IP address (check your router label or manual if you are unsure). Enter your username and password when prompted.

2. Look for the Port Forwarding or Virtual Server section in the router settings.

3. Create a new port forwarding rule with the following details:

Service Port: 80
Internal Port: 80
IP Address: (Your Raspberry Pi’s IP address)
Protocol: TCP
Common Service Port: HTTP

Make sure to replace (Your Raspberry Pi’s IP address) with the actual IP address of your Pi. You can find this IP address by typing the command hostname -I in your Raspberry Pi terminal.

Note: The options or wording in your router’s settings may vary slightly, but the basic idea remains the same — forward port 80 (HTTP) to your Raspberry Pi's local IP address using the TCP protocol.

Once done, your web server should be reachable from outside your local network using your public IP address.
