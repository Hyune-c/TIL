# Deploy Script

## deploy.sh

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
nohup java -jar ./build/libs/sidedish-08-0.0.1-SNAPSHOT.jar &
```

## Usage

```shell script
> ./deploy.sh {master}
```
