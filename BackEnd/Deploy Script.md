# Deploy Script

## deploy.sh

```shell script
PID=$(jps | grep TodoApplication | awk '{print $1}')
GIT_REPO="https://github.com/codesquad-member-2020/todo-11.git"
kill -9 $PID
sleep 1
rm -rf todo-11
git clone -b $1 --single-branch $GIT_REPO
sleep 1
cd todo-11
./gradle build -x test
sleep 1
nohup ./gradlew bootRun &
```

## Usage

```shell script
> ./deploy.sh devㅊ
```






Hamill  1:34 PM
1. 아파치 서버에 정적 파일 업로드하기
FE/build/ 안에 있는 파일들을 sudo cp -a * /var/www/html/ 로 보내면 아파치 서버에서 볼 수 있다.
node.js 설치 (sunny)
$ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - # ppa node.js가져오기
$ sudo apt-get install -y nodejs # node.js 설치
$ sudo apt-get install build-essential # npm 기능 install
fe 폴더 안에서 다음과 같은 명령어를 사용하면 dist 폴더를 얻을 수 있다.
$ npm install
$ npm run build
dist 폴더를sudo cp -a * /var/www/html/ 로 파일이동 해주면 된다.