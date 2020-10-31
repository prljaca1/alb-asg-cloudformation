# alb-asg-cloudformation
Applied below commands

#!/bin/bash

yum update -y

wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm

yum localinstall -y mysql57-community-release-el7-8.noarch.rpm

yum install -y mysql-community-server

yum install -y httpd php php-mysqlnd git

cd /var/www/html

wget https://wordpress.org/latest.tar.gz

cp wordpress/wp-config-sample.php wp-config.php

groupadd www

usermod -aG www ec2-user

chown -R root:www /var/www

echo '<?php phpinfo(); ?>' > /var/www/html/phpinfo.php

service httpd start

chkconfig httpd on

service mysqld start

systemctl enable mysqld.service

chkconfig mysqld on

*Problem:
When hit my instance on browser

http://54.198.57.225/index.php

gave error that wordpress required new php

*Solution:
then kept current php verison changed wordpress verion
 
cd /var/www/html

yes | rm -r * ==>with this command remove wordpress version with all                  directory

wget https://wordpress.org/wordpress-5.1.1.tar.gz

tar -xzf wordpress-5.1.1.tar.gz

cp -r wordpress/* /var/www/html/==> with this command under wordpress all folder and files copying under html

rm -rf wordpress==> removing wordpress

rm -rf wordpress-5.1.1.tar.gz==> removing zip file of wordpress

chmod -R 755 wp-content

service httpd start

chkconfig httpd on