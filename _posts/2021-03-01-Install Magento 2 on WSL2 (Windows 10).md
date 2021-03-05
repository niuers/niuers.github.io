---
title: "Install Magento 2 on WSL2 of Windows 10"
date: 2021-03-01
categories:
  - blog
tags:
  - magento2
---

1. Open a terminal window from WSL
2. Install Composer
    1. Follow the instruction [here to install composer][Install Composer].
    2. `sudo apt install php-cli unzip`
    3. `cd ~`: make sure you goto your home directory
    4. Download Composer installer: `curl -sS https://getcomposer.org/installer -o composer-setup.php`
    5. Install composer: `sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer`

3. You need a user name and password form magento marketplace to download repositary there
    1. [Obtain your magento 2 authentication keys][Get your authentication keys]
    2. Magento 2.4 requires php 7.4, so we need [update php to version 7.4][Update PHP]
        * `sudo add-apt-repository ppa:ondrej/php`
        *  `sudo apt update`
        *  `sudo apt install php7.4`
        * If you ever need remove a php version, here's how to do it: `sudo apt purge php8.0\*`
        * You also need install [some PHP extensions][PHP extensions for Magento 2]: `sudo apt install php7.4-curl`
            * Package `php-dom` is provided by `php-xml`, so you can just install the latter: `sudo apt install php7.4-xml`
            * Package `php-pdo_mysql` is provided by `sudo apt install php7.4-mysql`.
        * [Setup PHP configurations][Change PHP settings]
            * Find the config file: `php --ini | grep "Loaded Configuration File"`
            * Modify ALL the files found from above, e.g. `sudo vim /etc/php/7.4/cli/php.ini`
            * Set OPCache options in `php.ini`: `opcache.save_comments=1`
        * You may need install PHP Code Sniffer, otherwise you may see error message at the end of running the composer command (i.e. `Failed to set PHP CodeSniffer installed_paths Config`)
            * `sudo sudo apt install php-codesniffer`
            * `sudo composer global require "squizlabs/php_codesniffer=*"`
            * `phpcs`: check if it's installed
    3. Install MySql
        * `sudo apt install -y mysql-server mysql-client`
        * `sudo service mysql start`
        * `sudo mysql_secure_installation`
            * [When running the security script][Install MySql], you specified a password for root. However, this user is not allowed to connect to MySQL Shell with the same password. You can configure root to use MySQL Shell by changing its authentication method from the default “auth_socket” to “mysql_native_password”.
            * `sudo mysql`
            * `SELECT user,authentication_string,plugin,host FROM mysql.user;`
            * `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';`
            * `FLUSH PRIVILEGES;`
        * `mysql -u root -p` this shall get you into the shell with `root` privilege.
        * Start and stop `mysql` service
            * `sudo service mysql start`
            * `sudo service mysql stop`
            * Check status: `sudo service mysql status`
    4. [Install Apache Modules][Install Apache Modules]
        * List available Apache modules: `sudo apt-cache search libapache2*`
        * Install any desired modules: `sudo apt-get install [module-name]`
        * All mods are located in the `/etc/apache2/mods-avaiable` directory.
    5. Install nginx
        * `sudo apt-get -y install nginx`
        * Install and configure php-fpm
            * `sudo apt-get -y install php7.4-fpm php7.4-cli`
        * Update config: 
            * `sudo vim /etc/php/7.4/fpm/php.ini`
            * `sudo vim /etc/php/7.4/cli/php.ini`
        * Restart pfm service
            * `sudo service php7.4-fpm restart`
    5. Use Composer to download magento 2: `composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .`
        * If prompted to input user name and password, copy the public and private keys obtained from previous step respectively.


    6. Install Magento 2
        ```
        php bin/magento setup:install \--db-host="/Applications/MAMP/tmp/mysql/mysql.sock" \ --db-name=magelicious \--db-user=root --db-password=root \--admin-firstname=John \--admin-lastname=Doe \--admin-email=john@magelicious.loc \--admin-user=john \--admin-password=jrdJ%0i9a69n
        ```
          
 





[Install Composer]: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-20-04
[Get your authentication keys]: https://devdocs.magento.com/guides/v2.3/install-gde/prereq/connect-auth.html
[Update PHP]: https://askubuntu.com/questions/1146109/how-to-update-upgrade-php-7-2-to-latest-version-safely
[PHP extensions for Magento 2]: https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html
[Change PHP settings]: https://devdocs.magento.com/guides/v2.3/install-gde/prereq/php-settings.html
[Install MySql]: https://vitux.com/how-to-install-and-configure-mysql-in-ubuntu/
[Install Apache Modules]: https://www.linode.com/docs/guides/apache-web-server-ubuntu-12-04/