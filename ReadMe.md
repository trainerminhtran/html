-----------
-- Author: Minh Tran
-- Issue: show solution for issues of IT (CE Training Team)
-- HCM: 04.4.2018
-----------
1. Set Up Ubuntu 
    - Create User: 
        + adduser username
        + usermod -aG sudo username
        + su - username
        + sudo ls -la /root
    - Copy folder/file from local to server
        + rsync -avz --progress path/to/local user@ipserver:'part/to/server/'
    - Copy in server
        - Copy: sudo cp -R /opt/moodle /var/www/html/
        - Moodledata: sudo mkdir /var/moodledata
        - sudo chown -R www-data /var/moodledata
        - sudo chmod -R 777 /var/moodledata
        - sudo chmod -R 0755 /var/www/html/moodle
    - Permiss:
        + Enable: sudo chmod -R 777 /var/www/html/moodle
        + Disable: sudo chmod -R 0755 /var/www/html/moodle



2. Set Up Moodle on UbunTu
    - sudo apt-get install vim
    - sudo apt-get update
    - sudo apt-get install apache2 mysql-client mysql-server php7.0 libapache2-mod-php7.0
    - sudo apt-get install graphviz aspell ghostscript clamav php7.0-pspell php7.0-curl php7.0-gd php7.0-intl php7.0-mysql php7.0-xml php7.0-xmlrpc php7.0-ldap php7.0-zip php7.0-soap php7.0-mbstring
    - sudo service apache2 restart
    - sudo apt-get install git-core
    - git clone https://github.com/trainerminhtran/html.git
3. Set up MySql
    - sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
        + default_storage_engine = innodb
        + innodb_file_per_table = 1
        + innodb_file_format = Barracuda
    - sudo service mysql restart
    - mysql -u root -p
        + CREATE DATABASE moodle DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
        + create user 'moodledude'@'localhost' IDENTIFIED BY 'passwordformoodledude';
        + GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,CREATE TEMPORARY TABLES,DROP,INDEX,ALTER ON moodle.* TO moodledude@localhost IDENTIFIED BY 'passwordformoodledude';
        + quit;
        + SELECT password('passwordformoodledude');
    - sudo chmod -R 777 /var/www/html/moodle
4. Use MySQL WorkBrench to remote mysql in server
5. Use Git to backup Source Code
    - new repo at local
        + git init
        + git add .
        + git commit -m 'first commit'
        + git remote add origin https://github.com/trainerminhtran/html.git
        + git push -u origin master
        + user github: trainer.minhtran@gmail.com
        + pass github: trainer.minhtran!@2018
6. Copy config server: 
    - sudo cp 000-default.conf example1.com.conf