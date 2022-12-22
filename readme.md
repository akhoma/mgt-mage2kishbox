
run VM machine
ssh -p 2223 user@127.0.0.1
cd /var/www/mgt-dev/
docker-compose up -d



ip of host
10.0.2.2
telnet 10.0.2.2 9003



mgt: https://www.mgt-commerce.com/docs/mgt-development-environment/installation


ssh -p 23 root@127.0.0.1
root
cd /home/cloudpanel/htdocs/


index.php
echo xdebug_info();
echo  $_SERVER["REMOTE_ADDR"] . "---";
echo phpinfo();exit();


nano /etc/php/8.1/fpm/php.ini


zend_extension=xdebug.so
xdebug.mode=debug
xdebug.client_host=10.0.2.2
xdebug.client_port=9003
xdebug.max_nesting_level=500


xdebug.start_with_request=yes
xdebug.remote_handler=dbgp
xdebug.discover_client_host=true
xdebug.log="/var/log/xdebug/xdebug.log"

;extension=blackfire.so


supervisorctl restart php-fpm8.1


email mailhog:


sudo apt install msmtp

nano /etc/php/8.1/fpm/php.ini
sendmail_path = "/usr/bin/msmtp --host=mailhog --port=1025 -f test@test.localhost -t "
supervisorctl restart php-fpm8.1

/////////////
Install magento 
See : https://www.mgt-commerce.com/docs/mgt-development-environment/guides/magento2-installation

1. create doman in https://127.0.0.1:8443/domains
2. go to project dir

php8.1 /usr/local/bin/composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
php8.1 bin/magento setup:install --backend-frontname='admin' --key='18Av6ITivOZG3gwY1DhMDWtlLfx1spLP' --session-save='files' --db-host='127.0.0.1' --db-name='magento244ce' --db-user='magento2' --db-password='magento2' --base-url='https://magento244ce.docker/' --base-url-secure='https://magento244ce.docker/' --admin-user='admin' --admin-password='1qwerty' --admin-email='john@doe.com' --admin-firstname='John' --admin-lastname='Doe'
php8.1 bin/magento setup:perf:generate-fixtures ./setup/performance-toolkit/profiles/ce/small.xml
php8.1 bin/magento module:disable Magento_TwoFactorAuth
chmod -R 777 ./*
