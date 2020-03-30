# Deploy Script

## Spring main 설정

```java
public static void main(String[] args) {
    SpringApplicationBuilder app = new SpringApplicationBuilder(DustApplication.class);
    app.build().addListeners(new ApplicationPidFileWriter("./bin/shutdown.pid"));
    app.run();
  }
```

## Server Script

```shell script
# 파일 위치
 pwd
/home/ubuntu

# 소스 내용
cat deploy.sh
PID=$(<./dust-5/bin/shutdown.pid)
GIT_REPO="https://github.com/codesquad-member-2020/dust-5.git"
kill $PID
rm -rf dust-5
git clone -b $1 --single-branch $GIT_REPO
cd dust-5
./gradlew build
./gradlew bootRun &

# 사용법
> ./deploy.sh be/dev
```
