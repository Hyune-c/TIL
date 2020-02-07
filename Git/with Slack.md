## with Slask

설정 환경 : Mac Catalina 10.15.3, G-mail

## Set up Notifications
나에 관련된 알림에 효율적으로 반응하기 위한 Notification 설정 입니다.   


### E-mail 로 Notifications 관리하기

1. GitHub > Setting > Notifications 에 자신에게 필요한 항목들을 체크해줍니다.   
특히 E-mail 을 정확히 설정해야 합니다.

2. App Store > Mail for Gmail 설치

3. 하단 바에 (Dock) 읽지 않은 메일의 수를 보여주게 설정 합니다.
    - Preferecnces > General > Behavior - Show in Dock 체크
    - Preferecnces > Notifications > Unread Count - Badge Dock Icon 체크
    

### Slack DM 으로 연동하기
1. 좌측 탭 > Recent Apps > Add more apps > GitHub 추가 

2. slack 에서 자기 자신에게 DM 을 보닙니다.

3. 아래의 명령어로 원하는 repo 에 원하는 타입의 알림을 볼 수 있습니다.  
```
/github subscribe code-squad/java-monster-race commits reviews comments  
/github subscribe https://github.com/code-squad/java-monster-race commits reviews comments
```
<img src="https://user-images.githubusercontent.com/55722186/73999574-88ff7d80-49a8-11ea-8cc9-fe8e6bb404ad.png" width="500">

## 참고자료
[GitHub + Slack Integration](https://github.com/integrations/slack)