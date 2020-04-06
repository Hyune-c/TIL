# Deploy Script

## deploy.sh

```shell script
PID=$(jps | grep TodoApplication | awk '{print $1}')
GIT_REPO="https://github.com/codesquad-member-2020/todo-11.git"
kill $PID
sleep .5
rm -rf todo-11
git clone -b $1 --single-branch $GIT_REPO
cd todo-11
./gradlew build
nohup ./gradlew bootRun &
```

## Usage

```shell script
> ./deploy.sh dev
```
