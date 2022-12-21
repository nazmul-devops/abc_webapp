# abc_webapp
abc_webapp_deploy_on_aws

# Here we will deploy a php laravel webapp in a ubuntu local machine or aws ec2. 

# Prerequisit - (git, php7.4, mysql-server, composer)

#

#	 Step 01: (Installing php7.4 on ubuntu 22.04)

	$ sudo apt-get update
	
	$ sudo apt -y install software-properties-common

	$ sudo add-apt-repository ppa:ondrej/php

	$ sudo apt-get update

	$ sudo apt -y install php7.4

	$ php -v  (To verify Installation)

	$ sudo apt install -y php7.4-{cli,common,curl,zip,gd,mysql,xml,mbstring,json,intl}


#	Step 02: (Install Composer for dependency management)
	
	$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
	  php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
 	  php composer-setup.php
	  php -r "unlink('composer-setup.php');"

	$ php composer.phar --version

	$ sudo mv composer.phar /usr/local/bin/composer

	$ cd /usr/local/bin

	$ sudo chomd u+x composer

	$ composer --version

	$ composer init


#	 Step 03: (Installing Mysql-server and create demo database for project)

	$ sudo apt update

	$ sudo apt install mysql-server

	$ sudo systemctl start mysql.service

#	 — Configuring MySQL

	$ sudo mysql

	$ ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your-password';

	$ exit

	$ mysql -u root -p

	$ ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;

#	— Creating a Dedicated MySQL User and Granting Privileges

	$ sudo mysql

	$ mysql -u root -p

	$ CREATE USER 'sammy'@'localhost' IDENTIFIED BY 'password';

	$ GRANT PRIVILEGE ON database.table TO 'username'@'host'; (or)

	$ GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;

	$ FLUSH PRIVILEGES;

	$ mysql> exit

	$ mysql -u sammy -p

#	— Testing MySQL

	$ systemctl status mysql.service

	$ sudo mysqladmin -p -u sammy version


#	Step 04: (Cloning git repo to root directory)

	$ cd /var/www/html

	$ sudo git clone https://gitlab.com/niswapan/abcfan-website.git

	$ sudo mv abcfan-website abc

	$ sudo chmod -R 777 /var/www/html/abc/

	$ cd abc

	$ cp .env.example .env
	
	$ sudo nano .env (change the database name as your created database and root user password)

# 	- Configure web server 

	$ cd /etc/apache2/sites-enabled

	$ sudo nano 000-default.conf

	$ paste below texts and save & exit
	 ServerAdmin webmaster@localhost
         DocumentRoot /var/www/html/abc/public

         <Directory /var/www/html/abc/public>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Order allow,deny
                allow from all
         </Directory>

	$ sudo a2enmod rewrite

	$ sudo systemctl restart apache2

	
