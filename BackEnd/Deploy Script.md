# Deploy Script

## deploy.sh

> jar

```shell script
PID=$(jps | grep sidedish-08-0.0.1-SNAPSHOT.jar | awk '{print $1}')
GIT_REPO="https://github.com/codesquad-member-2020/sidedish-08.git"
kill -9 $PID
sleep 1
rm -rf sidedish-08
git clone -b $1 --single-branch $GIT_REPO
sleep 1
cd sidedish-08
cd BE
./gradlew build -x test
sleep 1
nohup java -jar ./build/libs/sidedish-08-0.0.1-SNAPSHOT.jar -Dspring.profiles.active=dev &
```

```shell script
> jps
2112 Jps
2073 sidedish-08-0.0.1-SNAPSHOT.jar
2027 GradleDaemon
```

> war

```shell script
GIT_REPO="https://github.com/codesquad-member-2020/sidedish-08.git"
rm -rf sidedish-08
git clone -b $1 --single-branch $GIT_REPO
cd sidedish-08/BE
./gradlew bootwar -x test
sleep 1
sudo rm -rf /var/lib/tomcat8/webapps/sidedish08*
sleep 1
sudo cp ./build/libs/sidedish08.war /var/lib/tomcat8/webapps
```

```shell script
> ls -lrt /var/lib/tomcat8/webapps/
total 33296
drwxr-xr-x 3 root    root        4096 Apr 21 08:32 ROOT
-rw-r--r-- 1 root    root    34083934 Apr 23 07:54 sidedish08.war
drwxr-x--- 5 tomcat8 tomcat8     4096 Apr 23 07:54 sidedish08
```

## Usage

```shell script
> ./deploy.sh {master}
```
