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

GRANT ALL ON indextest_db.* TO 'hyunec'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

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
Server characterset: utf8
Db     characterset: utf8
Client characterset: utf8
Conn.  characterset: utf8
...
--------------
```

## PostgreSql

### boot

```shell script
> docker pull mysql:5.7
> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
postgres            latest              b03968f50f0e        5 weeks ago         313MB
> ...
> docker ps -a                                                                                   8m 35s
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                    PORTS                               NAMES
84ede3ccb637        postgres            "docker-entrypoint.s…"   5 weeks ago         Up 11 minutes             0.0.0.0:5432->5432/tcp              albacheck
> docker exec -it albacheck bash
```

### setting

> create DB, User

```shell script
> psql -U postgres
psql (12.3 (Debian 12.3-1.pgdg100+1))
Type "help" for help.

postgres=# CREATE DATABASE albacheck;
CREATE DATABASE
postgres=# CREATE DATABASE albacheck_checklist;
CREATE DATABASE
postgres=# \q

postgres=# CREATE USER hyune WITH SUPERUSER CREATEDB LOGIN ENCRYPTED PASSWORD 'hyunec';
CREATE ROLE
```
