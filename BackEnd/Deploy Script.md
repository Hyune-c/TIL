# Deploy Script

## deploy.sh

```shell script
PID=$(jps | grep Sidedish08Application | awk '{print $1}')
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
nohup ./gradlew bootRun &
```

## Usage

```shell script
> ./deploy.sh dev
```
