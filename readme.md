
run VM machine <br />
ssh -p 2223 user@127.0.0.1 <br />
cd /var/www/mgt-dev/ <br />
docker-compose up -d <br />



ip of host <br />
10.0.2.2 <br />
telnet 10.0.2.2 9003 <br />



mgt: https://www.mgt-commerce.com/docs/mgt-development-environment/installation
<br />


ssh -p 23 root@127.0.0.1 <br />
root <br />
cd /home/cloudpanel/htdocs/ <br />


index.php <br />
echo xdebug_info(); <br />
echo  $_SERVER["REMOTE_ADDR"] . "---"; <br />
echo phpinfo();exit(); <br />


nano /etc/php/8.1/fpm/php.ini <br />


zend_extension=xdebug.so  <br />
xdebug.mode=debug <br />
xdebug.client_host=10.0.2.2 <br />
xdebug.client_port=9003 <br />
xdebug.max_nesting_level=500 <br />


xdebug.start_with_request=yes <br />
xdebug.remote_handler=dbgp <br />
xdebug.discover_client_host=true <br />
xdebug.log="/var/log/xdebug/xdebug.log" <br />

;extension=blackfire.so <br />


supervisorctl restart php-fpm8.1 <br />


email mailhog: <br />


sudo apt install msmtp <br />

nano /etc/php/8.1/cli/php.ini <br />
nano /etc/php/8.1/fpm/php.ini <br />
sendmail_path = "/usr/bin/msmtp --host=mailhog --port=1025 -f test@test.localhost -t " <br />

sudo apt-get install msmtp msmtp-mta <br />


supervisorctl restart php-fpm8.1 <br />

<br />
/////////////
Install magento <br />
See : https://www.mgt-commerce.com/docs/mgt-development-environment/guides/magento2-installation
<br />
1. create doman in https://127.0.0.1:8443/domains
<br />
2. go to project dir
<br />

php8.1 /usr/local/bin/composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
<br /> <br />
php8.1 bin/magento setup:install --backend-frontname='admin' --key='18Av6ITivOZG3gwY1DhMDWtlLfx1spLP' --session-save='files' --db-host='127.0.0.1' --db-name='magento24ce' --db-user='root' --db-password='root' --base-url='https://magento24ce.mgt/' --base-url-secure='https://magento24ce.mgt/' --admin-user='admin' --admin-password='1qwerty' --admin-email='john@doe.com' --admin-firstname='John' --admin-lastname='Doe'
<br /> <br />
php8.1 bin/magento setup:perf:generate-fixtures ./setup/performance-toolkit/profiles/ce/small.xml
<br /> <br />
php8.1 bin/magento module:disable Magento_TwoFactorAuth
<br /> <br />
chmod -R 777 ./*
<br /> <br />


///////////////////////////


First init DB (not required for existing VM):
<br />
http://prntscr.com/lFYQWWU5rpjl
<br />
docker-compose up -d
<br />
ssh -p 23 root@127.0.0.1
<br /><br />


sudo cp -a /etc/nginx/. /etc/nginx1/
<br />
sudo cp -a /var/lib/mysql/. /var/lib/mysql1/
<br />
logout
<br />
docker-compose down
<br />

http://prntscr.com/DSuR9ONO2Bmu
<br />
docker-compose up -d
<br />
https://127.0.0.1:8443/
