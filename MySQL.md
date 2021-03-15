# Managing MySQL 8.0 in Ubuntu 20.10

## Installing
1. `sudo apt-get install mysql-server`
2. **If** you can access root via `sudo mysql -u root` check if the `root` user has a password via its `authentication_string` attribute. `SELECT Host, User, authentication_string FROM mysql.User;`
   1. if the `authentication_string` is *blank* then initialize a password in the terminal via `sudo mysql_secure_installation` then configure the following options:
      - password strength
      - allow/disallow to connect to db remotey
      - remove anonymous users
      - delete test database;
   2. if it has a default password but you don't know the password the reset the password.
      1. change root password to `null`
         1. `sudo dpkg-reconfigure mysql-server`
         2. `sudo cat /etc/mysql/debian.cnf`
         3. check for *user* and *password*
         4. go to terminal
         5. `sudo mysql -u *user* -p`
         6. insert password
         7. `ALTER USER 'root'@'localhost' IDENTIFIED BY '<new_password>';` OR `UPDATE mysql.user SET authentication_string = NULL where User = 'root';`
         8. exit mysql
         9. try logging in to root
         10. `sudo mysql -u root -p`
         11. insert password

## Uninstalling
1. `sudo apt-get remove mysql-server -y`
2. `sudo apt-get purge mysql* -y`
3. `sudo apt-get autoremove -y`
4. `sudo apt-get autoclean`
5. `sudo apt-get dist-upgrade`
6. `sudo rm -rf /etc/mysql`

## Starting the service
1. `sudo systemctl stop mysql`
2. `sudo service mysql stop`

## Stopping the service
1. `sudo systemctl start mysql`
2. `sudo service mysql start`

## Checking the status
1. `sudo systemctl status mysql`
2. `sudo service mysql status`