# AWS

## Code Deploy 만들기

### # IAM Setting (인스턴스)

> IAM 역할은 신뢰하는 개체에 권한을 부여하는 안전한 방법입니다.

#### 역할 만들기

1. 신뢰
    - AWS 서비스 - EC2
2. 권한
    - AmazonS3FullAccess
    - AWSCodeDeployFullAccess
    - AWSCodeDeployRole
    - CloudWatchLogsFullAccess
3. 태그
    - Dan : Dan
4. 검토
    - codesquad Signup-5

### # 인스턴스 생성

> 인스턴스 시작 선택

1. AMI 선택
   - Ubuntu Server 18.04 LTS (HVM), SSD Volume Type
2. 인스턴스 유형 선택
   - 유형 : t2.micro (프리 티어 사용 가능)
3. 인스턴스 구성
    - IAM 역할 : Signup-5
4. 스토리지 추가
5. 태그 추가
   - name : Signup-5
6. 보안 그룹 구성

| 유형            | 프로토콜 | 포트 범위 | 소스        | 설명          |
| ------------- | ---- | ----- | --------- | ----------- |
| SSH           | TCP  | 22    | (Default) | vpn         |
| HTTP          | TCP  | 80    | (Default) | http        |
| 사용자 지정 TCP 규칙 | TCP  | 8080  | (Default) | spring boot |

7. 키 생성
    - singup-5

### # Server Setting

- Connect Instance  

```shell script
ssh -i "signup-5.pem" ubuntu@ec2-52-79-241-239.ap-northeast-2.compute.amazonaws.com
```

1. root Setting

```shell script
# root passwd setting
ubuntu@ip-172-31-39-101:~$ sudo passwd root
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# root sshd active
sudo vi /etc/ssh/sshd_config
## PermitEmptyPasswords yes

# user 의 인증 key 를 복사해줍니다.
sudo cp /home/ubuntu/.ssh/authorized_keys /root/.ssh

# sshd service restart
sudo service sshd restart

# exit 후 root 로 접속
ssh -i "signup-5.pem" root@ec2-52-79-241-239.ap-northeast-2.compute.amazonaws.com
```

2. java8 설치

> 아래 과정은 ubuntu 계정 (user) 으로 진행합니다.

```shell script
# apt-get update
sudo apt-get update

# java8 install
sudo apt-get install openjdk-8-jdk

ubuntu@ip-172-31-39-101:~$ java -version
openjdk version "1.8.0_242"
OpenJDK Runtime Environment (build 1.8.0_242-8u242-b08-0ubuntu3~18.04-b08)
OpenJDK 64-Bit Server VM (build 25.242-b08, mixed mode)
```

### # Code Deploy 그룹 추가

1. IAM > 엑세스 관리 > 그룹 > 새로운 그룹 생성
   1. 단계 1 : 그룹 이름
      1. signup-5
   2. 단계 2 : 정책 연결
   3. 단계 3 : 검토
2. IAM > 그룹 > signup-5 > 권한 > 인라인 정책 > "여기" > 사용자 지정 정책
   1. 정책 검토

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

1. IAM > 엑세스 관리 > 사용자 > 사용자 추가
   1. 세부 정보
      1. 사용자 이름 : Dan
      2. 액세스 유형 : 프로그래밍 방식 액세스
   2. 권한
      1. signup-5 그룹에 추가
   3. 태그
   4. 검토
   5. 완료

> credentials.csv 파일을 다운 받습니다.

### # Code Deploy Agent 설치

> 아래 과정은 ubuntu 계정 (user) 으로 진행합니다.

1. Install AWS Command Line Interface

```shell script
sudo apt-get install awscli -y

ubuntu@ip-172-31-39-101:~$ aws --version
aws-cli/1.14.44 Python/3.6.9 Linux/4.15.0-1057-aws botocore/1.8.48
```

2. AWS CLI Configure

```shell script
# Access Key : credentials.csv 에 있음
# Secret Access Key : credentials.csv 에 있음
# region name : ap-northeast-2 (서울)
# output format : json
ubuntu@ip-172-31-39-101:~$ pwd
/home/ubuntu
ubuntu@ip-172-31-39-101:~$ sudo aws configure
AWS Access Key ID [None]: A***************
AWS Secret Access Key [None]: dhVK2y*********
Default region name [None]: ap-northeast-2
Default output format [None]: json
```

3. AWS Agent 설치

```shell script
# install file download
wget https://aws-codedeploy-ap-northeast-2.s3.amazonaws.com/latest/install--2020-03-23 16:02:24--  https://aws-codedeploy-ap-northeast-2.s3.amazonaws.com/latest/install

# `/usr/bin/env: ruby: No such file or directory` 가 뜨는 경우 ruby 설치
sudo apt-get install ruby

# install
sudo ./install auto

# ubuntu 계정으로는 실행되지 않습니다.
# root 계정으로 실행시 정상 작동 합니다.
root@ip-172-31-39-101:/var/log/aws/codedeploy-agent# sudo service codedeploy-agent restart
root@ip-172-31-39-101:/var/log/aws/codedeploy-agent# ps -ef | grep codedeploy-agen
root      1521     1  0 01:43 ?        00:00:00 codedeploy-agent: master 1521
root      1526  1521  0 01:43 ?        00:00:00 codedeploy-agent: InstanceAgent::Plugins::CodeDeployPlugin::CommandPoller of master 1521
root      1543  1396  0 01:43 pts/0    00:00:00 grep --color=auto codedeploy-agen

# build 가 저장될 위치를 생성합니다.
ubuntu@ip-172-31-39-101:~$ pwd
/home/ubuntu
ubuntu@ip-172-31-39-101:~$ ls -lrt
total 20
drwxrwxr-x 2 ubuntu ubuntu  4096 Mar 24 01:48 build
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

#### 역할 만들기

1. 신뢰
    - AWS 서비스 - Code Deploy
2. 권한
    - AmazonS3FullAccess
    - AWSCodeDeployFullAccess
    - AWSCodeDeployRole
    - CloudWatchLogsFullAccess
3. 태그
4. 검토
    - signup-5_deploy

### # Code Deploy Application 생성

1. 개발자 도구 > CodeDeploy > 애플리케이션 > 애플리케이션 생성
   1. 애플리케이션 이름 : signup-5
   2. 컴퓨팅 플랫폼 : EC2/온프레미스
2. 개발자 도구 > CodeDeploy > 애플리케이션 > signup-5 > 배포 그룹 생성
    1. 배포 그룹 이름 : signup-5_Deploy_Group
    2. 서비스 역할 : arn:aws:iam::040326442355:role/signup-5_deploy
       1. 자동 완성 됩니다.
    3. 환경 구성 : Amazon EC2 인스턴스
       1. 태그를 입력하여 `1개의 일치하는 고유한 인스턴스.` 가 나옴을 확인합니다.
3. 개발자 도구 > CodeDeploy > 애플리케이션 > signup-5 > 배포 생성

## 참고 자료

<https://jojoldu.tistory.com/281>