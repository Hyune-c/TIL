# Mysql

> MySql 5.7

## mysql 설치하기

1. mysql version 확인

   ```shell script
   dan@dan_ubuntu:~$ sudo apt-cache search mysql-server
   ...
   mysql-server-5.7 - MySQL database server binaries and system database setup
   ...
   ```

2. 설치

   ```shell script
   sudo apt-get install mysql-server-5.7
   ```

3. root 비밀번호 설정

> mysql 접속 방법이 기존 패스워드 방식에서 우분투 18.04 부터 auth_socket 플러그인을 이용하는 방식으로 변경되었습니다.
아래는 이를 패스워드 방식으로 변경하고 기본 비밀번호를 'root' 로 설정하는 스크립트입니다.

   ```shell script
   dan@dan_ubuntu:~$ sudo mysql
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 4
   Server version: 5.7.29-0ubuntu0.18.04.1 (Ubuntu)

   Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.

   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

   mysql> update mysql.user set plugin='mysql_native_password' where user='root';
   Query OK, 1 row affected (0.00 sec)
   Rows matched: 1  Changed: 1  Warnings: 0

   mysql> update mysql.user set authentication_string=PASSWORD('root') where user='root';
   Query OK, 1 row affected, 1 warning (0.00 sec)
   Rows matched: 1  Changed: 1  Warnings: 1

   mysql> flush privileges;
   Query OK, 0 rows affected (0.01 sec)

   mysql> quit;
   Bye
   ```

4. root 접속 확인

   ```shell script
   dan@dan_ubuntu:~$ mysql -u root -p
   Enter password:
   ...
   mysql>
   ```

## mysql 한글 설정하기

1. characterset 확인

   ```shell script
   mysql> status
   --------------
   ...
   Server characterset:	latin1
   Db     characterset:	latin1
   Client characterset:	utf8
   Conn.  characterset:	utf8
   ...
   ```

2. /etc/mysql/my.cnf 에 설정 추가

   ```shell script
   [client]
   default-character-set = utf8

   [mysqld]
   init_connect = SET collation_connection = utf8_general_ci
   init_connect = SET NAMES utf8
   character-set-server = utf8
   collation-server = utf8_general_ci

   [mysqldump]
   default-character-set = utf8

   [mysql]
   default-character-set = utf8
   ```

3. characterset 확인

   ```shell script
   mysql> status
   --------------
   ...
   Server characterset:	utf8
   Db     characterset:	utf8
   Client characterset:	utf8
   Conn.  characterset:	utf8
   ...
   ```

## WorkBeanch 로 접속하기

- remote Ubuntu 에서 설정

```shell script
# mysql 접속
mysql -u root -p

# Create User & Grant PRIVILEGES
CREATE USER 'dan'@`%` IDENTIFIED BY 'dan;
CREATE DATABSE dan_db;
GRANT ALL ON dan_db.* TO 'dan'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

# local 외에서 접속이 필요한 경우 bind-address 를 주석 처리
vi /etc/mysql/mysql.conf.d/mysqld.cnf

# mysql restart
sudo service mysql restart;
netstat -an | grep 3306
```
