# **WEB 105 | Wordpress Install Guide**  

This run-sheet takes you through the steps to manually install Wordpress on Ubuntu 16.04  
This guide assumes that you already have an Ubuntu 16.04 machine set up with Apache2 installed and configured,  
with SSH enabled.  

Wordpress runs an a LAMP stack  
 -Linux  
 -Apache2  
 -MySQL  
 -PHP  


Start with an SSH connection into your Ubuntu machine, now update server packages  

	$ sudo apt-get update  

Enter your sudo password when prompted  
Now navigate to /var directory, and creating a temp folder to work from    

	$ cd /var  
	$ sudo mkdir temp  

Now give yourself full permissions within the temp directory, then navigate to it  

	$ sudo chown -R _your sudo username_ temp  
	$ cd temp  

## **Install MySQL**  

	$ sudo apt-get install mysql-server  

Choose MySQL root password when prompted  
Enter Y when prompted  
  
Now set up a secure installation  

	$ sudo mysql_secure_installation  

Enter your MySQL root password when prompted
Enter Y to set up Validate Password plug-in  
Select desired security level  
Select N to keep password as is, or Y to change password if desired  
You may select Y for remaining prompts  

## **Install PHP**    

Add required repository, and update packages    

	$ sudo add-apt-repository ppa:ondrej/php  

Press Enter when prompted  
update packages to include repository  

	$ sudo apt-get update  

Now install PHP 7.2  

	$ sudo apt-get install php7.2  

Enter Y when prompted  
Add required PHP mods  

	$ sudo apt-get install libApache2-mod-php7.2 php7.2-mysql php7.2-mbstring  

Enter Y when prompted  

## **Download Wordpress**  

	$ sudo curl -O https://wordpress.org/latest.zip  

Install unzip tool  

	$ sudo apt-get install unzip  

Unzip Wordpress Files  

	$ unzip latest.zip  

Move Wordpress files from unzipped folder to web root folder eg: /var/www/html  

	$ sudo rsync -av wordpress/* _your web root folder_  

Set permissions for Wordpress files  

	$ sudo chown -R www-data:www-data _your web root_  
	$ sudo chmod -R 755 _your web root_  

## **Create Wordpress database**  

Access MySQL command line  

	$ mysql -u root -p  

Enter MySQL root password when prompted  
Create database, and set user privileges  

	MySQL>$ CREATE DATABASE _your database name_;  
	MySQL>$ GRANT ALL PRIVILEGES ON _your database name_.* TO '_your database username_'@'localhost' IDENTIFIED BY '_your database password_';  
	MySQL>$ FLUSH PRVILEGES;  
	MySQL>$ EXIT;  

## **Add Wordpress to Domain Name**  

Navigate to your web root directory  eg: /var/www/html  

	$ cd _your web root_  

Change wp-config-sample file to wp-config file

	$ sudo mv wp-config-sample.php wp-config.php  

Enter your sudo password when prompted  
Update mySQL settings in wp-config file  

	$ sudo nano wp-config.php  

Make the following adjustments to the MySQL settings section of the wp-config file  

	define('DB_NAME', '_your database name_');  
	define('DB_USER', '_your database username_');  
	define('DB_PASSWORD', '_your database password_');  

Press ctrl-O to write, then press enter to save  
Press ctrl-X to exit document  

## **Restart web server and MySQL**    

	$ sudo service apache2 restart  
	$ sudo service mysql restart  


**Now you can open your web browser, enter your domain name, and finish up the rest of your installation on  
 your brand new Wordpress website!!**  




  

 

 
