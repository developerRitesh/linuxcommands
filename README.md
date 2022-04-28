# linuxcommands

Install apache web server 
========================================
sudo apt-get install apache2
   
Running Mysql 
========================================
/etc/init.d/mysql start

Install php 
========================================
download php tar file from php website 
extract and install through 
    ./configure
    make
    sudo make install
or sudo apt-get install php 

After installing apache2 you have to configure php with apche 
install
sudo apt-get install libapache2-mod-php7.0

apache internal 500 error (go to apache log file and see the actual error from there) 
================================================
sudo a2enmod headers 


installing composer in linux 
==============================================
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer

Copy using rsync
==============================================
sudo rsync -avz /media/ritesh/d7f0c20d-961b-443e-a8b4-1faac1bb63da/opt/lampp /home/ritesh/Ramanand/lampp_setup


installing idea 
==============================================
download tar.gz file and go to that directory
sudo tar xf -*.tar.gz -C /opt/
  
Magento php errors
=========================================
[Class 'IntlDateFormatter' not found in Magento2]
for this error we have to install

 sudo apt-get install php7.0-intl

(this is library for date formatter)
[GD Library extension not found]

Installing mb string 
=========================================
sudo apt-get install php7.0-mbstring

installing xml extension
=============================
sudo apt-get install php7.0-xml


Installing mysql 
========================================
sudo apt-get install mysql-server

granting prevelidge for htacess to work on apache
=================================================
sudo subl /etc/apache2/apache2.conf

search and change 

<Directory /var/www/>
	Options Indexes FollowSymLinks
	AllowOverride None
	Require all granted
</Directory> 

TO
 
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>

but if you have new installation you have to Enable the config file 
sudo a2enconf httpd

Displayinh errors and warning on apache if not shown 
===================================================
sudo subl /etc/php/7.0/apache2/php.ini
set 
display_errors = On
display_startup_errors = On
make sure to set it on all occurence where it is not commented out already

running google-chrome without occupiying the terminal 
====================================================
google-chrome & 


permissions for mysql directives to work if copied from another system 
=======================================================================
WARNING : do not copy lampp directory using root as you screw permissions that way ,use rsync instead
rsync -avz rpmpkgs/ root@192.168.0.101:/home/  (although the permissions were different)
sudo chmod 755 /opt/lampp/etc/my.cnf
sudo chmod -R 777 /opt/lampp/var/mysql
sudo chown -hR root:root /opt/lampp
after that i faced some mysql session permission issues to resolve that from gui i changes the permission of opt/lampp/temp folder to daemon(create and delete and for others daemon-acess files) 
voila everything will work now 

Removing Softwares 
=======================================
sudo apt-get --purge remove gimp

Installing phpmyadmin
========================================
sudo apt-get install phpmyadmin
now phpmyadmin is installed but we also have to configure it with apache server for that we will create symbolic link 
sudo ln -sf /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
if you didnt set password for phpmyadmin , well pity for got to 
/etc/phpmyadmin/config.inc.php

uncomment the configuration 
 $cfg['Servers'][$i]['AllowNoPassword'] = TRUE;

Start apache web server 
========================================
sudo /etc/init.d/apache2 start
sudo service apache2 start (if installed as a service)

Extracting tar packages 
========================================
tar xvzf PACKAGENAME.tar.gz
tar xvjf PACKAGENAME.tar.bz2

Installing Software from tar packages 
========================================
1. extract the files 
    tar xvzf PACKAGENAME.tar.gz
    tar xvjf PACKAGENAME.tar.bz2
2. Go to the extracted directory
    ./configure
    make
    sudo make install


Open Gui from terminal 
=========================================
nemo directory/path/filename.txt (move you to the file highlighted)

In new linux mint setup first you have to activate the root 
==============================================
sudo passwd root

To create a new symlink
============================================
sudo ln -s /existing/directory/path /path/to/symlink    (symlink must not be already present otherwise its not created)

To create or update a symlink
============================================
sudo ln -sf /home/ritesh /opt/lampp/htdocs
sudo ln -sf smb://uday-mint/dropbox/ /home/ritesh/uday_dropbox
sudo mount -t cifs -o username=nicorellius smb://uday-mint/dropbox/ /home/ritesh/uday_dropbox
sudo smbmount //uday-mint/dropbox/ /home/ritesh/uday_dropbox
sudo ln -sf /home/ritesh /var/www/html

To remove A symlink 
===========================================
unlink /path/to/symlink 

To check current path for mysqld service 
===========================================
 ps -aux | grep mysqld

Create a Symlink for mysql (might need root permission)
===========================================
ln -sf /opt/lampp/var/mysql/mysql.sock /var/run/mysqld/mysqld.sock [if not working we have another solution ]
https://www.howtoforge.com/allow-your-applications-to-access-the-xampp-mysql-server-directly
create symlink for the mysql application instead (should take backup of /usr/bin/mysql application before which i didn't mv /usr/bin/mysql /usr/bin/mysql.original)
ln -s  /opt/lampp/bin/mysql /usr/bin/mysql	

Now to add laravel command to your terminal add the run 
============================================ 
composer global require "laravel/installer=~1.1"

now run laravel new youprojectname 

but in my case that stated the error unkonow command laravel (Make sure to place the ~/.composer/vendor/bin directory in your PATH) 
for that i addded following line in home/lavish/.bashrc file 

echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc
and then restarted the console and run the following command  

source ~/.bashrc
and everything worked fine then . laravel command is working now. Although require php version 7 for its modules .


Running phpmyadmin if apache is running 
===========================================
Go to /opt/lampp/phpmyadmin/config.inc.php and find $cfg['Servers'][$i]['host'] = localhost; 
change it to $cfg['Servers'][$i]['host'] = '127.0.0.1'; make sure the line is not commented which was my case .

Hide System tables in phpmyadmin 
============================================
add the following line to /opt/lampp/phpmyadmin/config.inc.php 
$cfg['Servers'][$i]['hide_db'] = '^(information_schema|mysql|test|performance_schema|phpmyadmin)$';


Running phpmyadmin permission issues  
===========================================
Also config.inc.php should not have world written permission , by which pma also fails and at 
Warning: World-writable config file '/opt/lampp/etc/my.cnf' is also ignored
chmod 644 /opt/lampp/etc/my.cnf


To start the xampp control panel (lampp commands)
============================================
/opt/lampp/manager-linux-x64.run
/opt/lampp/lampp status
/opt/lampp/lampp list (to see all available commands)
/opt/lampp/lampp start
/opt/lampp/lampp startapache
/opt/lampp/lampp startmysql
/opt/lampp/lampp stopapache
/opt/lampp/lampp stopmysql

lampp memory commands 
===============================================
free -m  (to check memory usage)
sudo dmidecode -t 17 (to check information about the ram)
df -h (check disk space)
du (dont run list space taken by each file in the whole system)

Installing xDEBUGGER 
===============================================
Had to go to a hell long process 
open this link https://xdebug.org/wizard.php to install xdebugger (need phpinfo for customised instruction)

1.Download xdebug-2.6.0beta1.tgz
2. cd xdebug-2.6.0beta1
3. phpize

i got the following error 
Cannot find autoconf. Please check your autoconf installation and the
$PHP_AUTOCONF environment variable. Then, rerun this script.
so for that install autoconf.
 apt-get install autoconf
while installing it i get another error that  
Setting up mysql-server-5.7 (5.7.20-0ubuntu0.16.04.1) 
var/run/mysqld not found ,  so i created a symlink to link ln -s  /opt/lampp/bin/mysql /usr/bin/mysql which made my mysql run on terminal without specifying its path 

The whole problem was that i was using the command phpsize which is for core mysql service what i was supposed to do instead is run 

/opt/lampp/bin/phpize 

which run without any error

Now after that configure the extension
./configure --enable-xdebug --with-php-config=/opt/lampp/bin/php-config

Run ‘make’ to get the compiled xdebug.so
make

Copy the xdebug.so file to PHP’s extensions directory (you may need root privileges for this)
cp modules/xdebug.so /opt/lampp/lib/php/extensions

after that subl /opt/lampp/etc/php.ini
you could also refer to resource http://www.sanisoft.com/blog/2007/06/23/how-to-install-xdebug-php-extension-for-xampp-on-linux/

Warning: session_start(): failed: Permission denied (13)
==================================================================
cause : happened when i moved to have two lampp setup 
solution : created the user with name daemon and gave it read/write permission , note while giving it all permissionn with user lavish it didnt work. 

To copy directories from server 
================================================================
wget --no-parent -r http://WEBSITE.com/DIRECTORY

note : without --no-parent everything is downloaded 

Launced sublime text with proper character support 
================================================================
LANG=en_US.UTF-8 LC_CTYPE=en_US.UTF-8 sublime_text


idea terminal launcher
==============================
/usr/local/bin/idea

check allowed memory size (while memeory exhausted)
====================================
php -r "echo ini_get('memory_limit').PHP_EOL;"

uninstall macbunto theme
=====================================
To Uninstall themes, icons and cursors
Terminal Commands:
cd /usr/share/icons/mac-cursors && sudo ./uninstall-mac-cursors.sh
sudo apt-get remove macbuntu-os-icons-lts-v7 macbuntu-os-ithemes-lts-v7

