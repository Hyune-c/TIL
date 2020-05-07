# Docker

## mysql 5.7

### install & boot

```shell script
> docker pull mysql:5.7
> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mysql               5.7                 f965319e89de        9 days ago          448MB
> docker run -d --name baseball_mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
> docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                               NAMES
070ab2bff1b6        mysql:5.7           "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:3306->3306/tcp, 33060/tcp   baseball_mysql
> docker exec -it baseball_mysql /bin/bash
```

### setting

> vim

```sheell script
> apt-get update
> apt-get install vim -y
```

> create DB, User

```shell script
> mysql -u root -p
mysql> update mysql.user set plugin='mysql_native_password' where user='root';
mysql> update mysql.user set authentication_string=PASSWORD('root') where user='root';
mysql> flush privileges;

mysql> CREATE USER 'baseball06'@`%` IDENTIFIED BY 'baseball06';
mysql> create database baseball06_db;
mysql> show databases;
mysql> GRANT ALL ON baseball06_db.* TO 'baseball06'@'%' WITH GRANT OPTION;
mysql> FLUSH PRIVILEGES;
```

> /etc/mysql/my.cnf

```shell script
[client]
default-character-set = utf8

[mysqld]
init_connect = SET collation_connection = utf8_general_ci
init_connect = SET NAMES utf8
character-set-server = utf8
collation-server = utf8_general_ci
lower_case_table_names = 1

[mysqldump]
default-character-set = utf8

[mysql]
default-character-set = utf8
```

```shell script
mysql> status
--------------
...
Server characterset:	utf8
Db     characterset:	utf8
Client characterset:	utf8
Conn.  characterset:	utf8
...
--------------
```
