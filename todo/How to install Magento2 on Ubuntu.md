
[[Magento]] 是一個用PHP編寫的電商平臺，

我選用ubuntu、apache、MySQL、elast

![](https://experienceleague.adobe.com/docs/commerce-operations/assets/install-diagram-24.svg?lang=en)

### How to install

1. Install Apache2 as Web Server
2. Install MySQL and Create a datebase for Magento
3. Install PHP 8.1 and the extensions
4. Elasticsearch
5. PHP Composer
6. Install Magento 2.4.5

#### Install Apache2 as Web Server

```
sudo apt update
sudo apt install apache2
sudo apache2ctl -v
systemctl enabled apache2
```

#### Install MySQL and Create a datebase for Magento

```
sudo apt install mysql-server
sudo mysql
SELECT user,authentication_string,plugin,host FROM mysql.user;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
exit
mysql -u root -p
SELECT user,authentication_string,plugin,host FROM mysql.user;
CREATE USER 'magento2'@'localhost' IDENTIFIED BY 'your_secure_password';
ALTER USER 'magento2'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_secure_password';
GRANT ALL PRIVILEGES ON *.* TO 'magento2'@'localhost' WITH GRANT OPTION;
exit
mysql -u magento2 -p
CREATE DATABASE magento2;
exit
```

#### Install PHP and required extensions

Update your APT repositories.

sudo apt update
Install PHP 8.1 and packages with command:

sudo apt install php8.1 libapache2-mod-php php-mysql
Next, verify your PHP version: it should be 8.1

php -v


https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/composer.html?lang=zh-Hant

https://www.cybrosys.com/blog/how-to-install-magento-2-4-5-in-ubuntu-22-04

https://www.thecoachsmb.com/install-magento-2-4-5-on-ubuntu-22-04-complete-guide/

https://magento.stackexchange.com/questions/318831/magento-2-4-0-getting-error-could-not-validate-a-connection-to-elasticsearch

https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/overview.html