# AWS

## Code Deploy 만들기

### # IAM Setting

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

> 아래 과정은 root 가 아닌 ubuntu 계정 (user) 으로 설치합니다.

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

#### Code Deploy 그룹 추가

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

#### Code Deploy 사용자 추가

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

#### Code Deploy Agent 설치

> 아래 과정은 root 가 아닌 ubuntu 계정 (user) 으로 설치합니다.

```shell script
# Install AWS Command Line Interface
sudo apt-get install awscli -y

ubuntu@ip-172-31-39-101:~$ aws --version
aws-cli/1.14.44 Python/3.6.9 Linux/4.15.0-1057-aws botocore/1.8.48

# AWS CLI setting
## Access Key : credentials.csv 에 있음
## Secret Access Key : credentials.csv 에 있음
## region name : ap-northeast-2 (서울)
## output format : json
ubuntu@ip-172-31-39-101:~$ pwd
/home/ubuntu
ubuntu@ip-172-31-39-101:~$ sudo aws configure
AWS Access Key ID [None]: A***************
AWS Secret Access Key [None]: dhVK2y*********
Default region name [None]: ap-northeast-2
Default output format [None]: json

```



## 참고 자료

<https://jojoldu.tistory.com/281>