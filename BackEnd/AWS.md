# AWS

## Practice Todo

### # 루트 계정 2중 잠금 설정

Google OTP 로 설정 완료

### # admin 계정 만들기

[참고자료](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/getting-started_create-admin-group.html)

1. 페이지 상단의 내 ID > 내 계정 > 결제 정보에 대한 IAM 사용자 및 역할 액세스 `활성화`

2. 서비스 > IAM > 엑세스 관리 > 사용자 > 사용자 추가
    - 세부 정보
      - 사용자 이름 : Administrator
      - AWS 액세스 유형 선택
        - 액세스 유형 : AWS Management Console 액세스
    - 권한
      - 권한 설정 > 그룹 생성
        - AdministratorAccess 정책 선택하여 그룹 생성
    - 태그
      - Name : Administrator
    - credentials.csv 다운로드

### # power user 계정 만들기

[참고자료](https://kc.mcafee.com/corporate/index?page=content&id=KB83814)

1. PowerUser 로 그룹 생성
   - PowerUserAccess 정책 선택
2. PowerUser 로 사용자 생성
   - Administrator 와 동일
   - 사용자 이름 : PowerUser
   - Name : PowerUser

### # ec2 생성 (우분투로) 및 ssh 접속 성공하기

> Code Deploy 에 같이 설명

## 수동 배포

### # 인스턴스 생성

1. Amazon Machine Image 선택
   - Ubuntu Server 18.04 LTS (HVM), SSD Volume Type
2. 인스턴스 유형 선택
   - 유형 : t2.micro (프리 티어 사용 가능)
3. 인스턴스 구성
   - IAM 역할 : Dust-5_EC2_Deploy
4. 태그 추가
   - name : Dust-5
5. 보안 그룹 구성

| 유형            | 프로토콜 | 포트 범위 | 소스        | 설명          |
| ------------- | ---- | ----- | --------- | ----------- |
| SSH           | TCP  | 22    | (Default) | SSH         |
| HTTP          | TCP  | 80    | (Default) | HTTP        |
| 사용자 지정 TCP 규칙 | TCP  | 8080  | (Default) | Spring Boot |

5. 키 생성
    - Dust-5
    - Dust-5.pem 다운로드

### # Server Setting

- root Setting

> 아래 작업 root 접속이 가능합니다.  
> ssh -i "Dust-5.pem" root@ec2-3-34-46-140.ap-northeast-2.compute.amazonaws.com

```shell script
# root passwd setting
> sudo passwd root
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# root sshd active
> sudo vi /etc/ssh/sshd_config
PasswordAuthentication yes
PermitEmptyPasswords yes

# user 의 인증 key 를 복사해줍니다.
> sudo cp /home/ubuntu/.ssh/authorized_keys /root/.ssh

# sshd service restart
> sudo service sshd restart
```

- java8 install

```shell script
> sudo apt-get update
> sudo apt-get install openjdk-8-jdk -y
> java -version
openjdk version "1.8.0_242"
OpenJDK Runtime Environment (build 1.8.0_242-8u242-b08-0ubuntu3~18.04-b08)
OpenJDK 64-Bit Server VM (build 25.242-b08, mixed mode)
```

- Time

```shell script
> sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
```

### # 배포

```shell script
# git clone
> git clone https://github.com/Hyune-c/signup.git

# gradle 설치
> sudo apt install gradle

# 서버 시작 (백그라운드에서 시작)
> ./gradlew build
> ./gradlew bootRun &
Downloading https://services.gradle.org/distributions/gradle-6.2.2-bin.zip
.........10%.........20%.........30%..........40%.........50%.........60%..........70%.........80%.........90%..........100%

Welcome to Gradle 6.2.2!

Here are the highlights of this release:
 - Dependency checksum and signature verification
 - Shareable read-only dependency cache
 - Documentation links in deprecation messages

For more details see https://docs.gradle.org/6.2.2/release-notes.html

Starting a Gradle Daemon (subsequent builds will be faster)

> Task :test
29-03-2020 08:54:45.904 [SpringContextShutdownHook] INFO  com.zaxxer.hikari.HikariDataSource.close - HikariPool-1 - Shutdown initiated...
29-03-2020 08:54:45.922 [SpringContextShutdownHook] INFO  com.zaxxer.hikari.HikariDataSource.close - HikariPool-1 - Shutdown completed.
29-03-2020 08:54:45.924 [SpringContextShutdownHook] INFO  org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor.shutdown - Shutting down ExecutorService 'applicationTaskExecutor'

BUILD SUCCESSFUL in 2m 2s
5 actionable tasks: 5 executed
ubuntu@ip-172-31-45-252:~/build/signup$ ./gradlew bootRun

> Task :bootRun
LOGBACK: No context given for c.q.l.core.rolling.SizeAndTimeBasedRollingPolicy@1318180415

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.2.5.RELEASE)

29-03-2020 08:56:34.148 [main] INFO  com.codesquad.signup.SignupApplication.logStarting - Starting SignupApplication on ip-172-31-45-252 with PID 10317 (/home/ubuntu/build/signup/build/classes/java/main started by ubuntu in /home/ubuntu/build/signup)
```

> # 아래는 검토 후 수정해야 되는 내용들입니다.

> IAM > 엑세스 관리 > 역할

### # EC 에 할당할 역할 생성

1. 신뢰
    - AWS 서비스 - EC2
2. 권한
    - AmazonS3FullAccess
    - AWSCodeDeployFullAccess
    - AWSCodeDeployRole
    - CloudWatchLogsFullAccess
3. 태그
    - Name : Dust-5_EC2_Deploy
4. 검토
    - Dust-5_EC2_Deploy


### # Code Deploy 그룹 추가

> IAM > 엑세스 관리 > 그룹 > 새로운 그룹 생성

- 그룹 이름 : Devops
- 정책 없음

> IAM > 그룹 > Devops > 권한 > 인라인 정책 > "여기" > 사용자 지정 정책

- 정책 검토 : Deploy

```shell script
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "autoscaling:*",
                "codedeploy:*",
                "ec2:*",
                "lambda:*",
                "elasticloadbalancing:*",
                "s3:*",
                "cloudwatch:*",
                "logs:*",
                "sns:*"
            ],
            "Resource": "*"
        }
    ]
}
```

### # Code Deploy 사용자 추가

> IAM > 엑세스 관리 > 사용자 > 사용자 추가

- Devops_Administrator 사용자 추가
  - 액세스 유형 : 프로그래밍 방식 액세스
- Devops 그룹에 추가
- Tag
  - Name : Devops_Administrator

> credentials.csv 파일을 다운 받습니다.

### # Code Deploy Agent 설치

1. Install AWS Command Line Interface

```shell script
> sudo apt-get install awscli -y
> aws --version
aws-cli/1.14.44 Python/3.6.9 Linux/4.15.0-1057-aws botocore/1.8.48
```

2. AWS CLI Configure

```shell script
# Devops_Administrator 의 정보를 입력
# Access Key : credentials.csv 에 있음
# Secret Access Key : credentials.csv 에 있음
# region name : ap-northeast-2 (서울)
# output format : json
> pwd
/home/ubuntu
> sudo aws configure
AWS Access Key ID [None]: A***************
AWS Secret Access Key [None]: dhVK2y*********
Default region name [None]: ap-northeast-2
Default output format [None]: json
```

3. AWS Agent 설치

```shell script
# install file download
> wget https://aws-codedeploy-ap-northeast-2.s3.amazonaws.com/latest/install

# `/usr/bin/env: ruby: No such file or directory` 가 뜨는 경우 ruby 설치
> sudo apt-get install ruby -y

# install
> sudo ./install auto

# ubuntu 계정으로는 실행되지 않습니다.
# root 계정으로 실행시 정상 작동 합니다.
> sudo service codedeploy-agent status
> ps -ef | grep codedeploy
root      8414     1  0 16:12 pts/0    00:00:00 codedeploy-agent: master 8414
root      8420  8414  0 16:12 pts/0    00:00:00 codedeploy-agent: InstanceAgent::Plugins::CodeDeployPlugin::CommandPoller of master 8414

# build 가 저장될 위치를 생성합니다.
> pwd
/home/ubuntu
> ls -lrt
total 4
drwxrwxr-x 2 ubuntu ubuntu 4096 Mar 28 15:11 build
```

4. intellij gradle project 에 생성

> /appspec.yml

```shell script
version: 0.0
os: linux
files:
  - source:  /
    destination: /home/ubuntu/build/
```

### # IAM Setting (Code Deploy)

> IAM > 엑세스 관리 > 역할

1. 신뢰
    - AWS 서비스 - Code Deploy
2. 권한
    - AWSCodeDeployRole
3. 태그
    - Name : CodeDeploy
4. 검토
    - CodeDeploy

### # Code Deploy Application 생성

> 개발자 도구 > CodeDeploy > 애플리케이션 > 애플리케이션 생성

1. 애플리케이션 이름 : Dust-5_Application
2. 컴퓨팅 플랫폼 : EC2/온프레미스

### # Code Deploy 배포 그룹 생성

> 개발자 도구 > CodeDeploy > 애플리케이션 > Dust-5_Application > 배포 그룹 생성

 1. 배포 그룹 이름 : Dust-5_DeployGroup
 2. 서비스 역할 : arn:aws:iam::040326442355:role/CodeDeploy
    1. 자동 완성 됩니다.
 3. 환경 구성 : Amazon EC2 인스턴스
    1. `Name : Dust-5` 태그를 입력하여 `1개의 일치하는 고유한 인스턴스.` 가 나옴을 확인합니다.
 4. 배포 설정 : OneAtTime
 5. 로드 밸런서 해제

### # Code Deploy 배포 생성

> 개발자 도구 > CodeDeploy > 애플리케이션 > Dust-5_Application
 > 배포 생성

1. Git Token 을 만들고 (구글링) 배포하고자 하는 커밋 ID 를 가져옵니다.

### # 배포 성공 후 gradle build 하기

1. 배포된 소스

```shell script
> ls -lrt
total 40
-rw-rw-r-- 1 root root   28 Mar 24 02:48 settings.gradle
-rw-rw-r-- 1 root root 2942 Mar 24 02:48 gradlew.bat
-rwxrwxr-x 1 root root 5764 Mar 24 02:48 gradlew
-rw-rw-r-- 1 root root  820 Mar 24 02:48 build.gradle
-rw-rw-r-- 1 root root   82 Mar 24 02:48 appspec.yml
-rw-rw-r-- 1 root root  403 Mar 24 02:48 README.md
-rw-rw-r-- 1 root root 1138 Mar 24 02:48 HELP.md
drwxr-xr-x 4 root root 4096 Mar 24 02:50 src
drwxr-xr-x 3 root root 4096 Mar 24 02:50 gradle
```

2. gradle build

```shell script
ubuntu@ip-172-31-39-101:~/build$ ./gradlew build
Downloading https://services.gradle.org/distributions/gradle-6.2.2-bin.zip
.........10%.........20%.........30%..........40%.........50%.........60%..........70%.........80%.........90%..........100%

Welcome to Gradle 6.2.2!

Here are the highlights of this release:
 - Dependency checksum and signature verification
 - Shareable read-only dependency cache
 - Documentation links in deprecation messages

For more details see https://docs.gradle.org/6.2.2/release-notes.html

Starting a Gradle Daemon (subsequent builds will be faster)

> Task :test
23-03-2020 17:54:11.292 [SpringContextShutdownHook] INFO  com.zaxxer.hikari.HikariDataSource.close - HikariPool-1 - Shutdown initiated...
23-03-2020 17:54:11.309 [SpringContextShutdownHook] INFO  com.zaxxer.hikari.HikariDataSource.close - HikariPool-1 - Shutdown completed.
23-03-2020 17:54:11.310 [SpringContextShutdownHook] INFO  org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor.shutdown - Shutting down ExecutorService 'applicationTaskExecutor'

BUILD SUCCESSFUL in 2m 24s
5 actionable tasks: 5 executed
ubuntu@ip-172-31-39-101:~/build$
```

3. Tree 를 통해 class 파일이 생성됨을 확인

```shell script
ubuntu@ip-172-31-39-101:~/build$ tree
.
├── HELP.md
├── README.md
├── appspec.yml
├── build
│   ├── classes
│   │   └── java
│   │       ├── main
│   │       │   └── com
│   │       │       └── codesquad
│   │       │           └── signup
│   │       │               ├── SignupApplication.class
│   │       │               ├── api
│   │       │               │   └── UserApi.class
│   │       │               └── common
│   │       │                   └── Result.class
...
```

4. 실행

```shell script
ubuntu@ip-172-31-39-101:~/build$ ./gradlew bootRun

> Task :bootRun
LOGBACK: No context given for c.q.l.core.rolling.SizeAndTimeBasedRollingPolicy@1318180415

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.2.5.RELEASE)

23-03-2020 18:08:44.063 [main] INFO  com.codesquad.signup.SignupApplication.logStarting - Starting SignupApplication on ip-172-31-39-101 with PID 2227 (/home/ubuntu/build/build/classes/java/main started by ubuntu in /home/ubuntu/build)
```

5. Test Url

<http://ec2-52-79-241-239.ap-northeast-2.compute.amazonaws.com:8080/api/users/testOk>  
<http://ec2-52-79-241-239.ap-northeast-2.compute.amazonaws.com:8080/api/users/testFail>
## 참고 자료

<https://jojoldu.tistory.com/281>




-- 누락?

> IAM > 엑세스 관리 > 역할

1. 신뢰
    - AWS 서비스 - EC2
2. 권한
    - AmazonS3FullAccess
    - AWSCodeDeployFullAccess
    - AWSCodeDeployRole
    - CloudWatchLogsFullAccess
3. 태그
    - Name : Devops
4. 검토
    - Devops