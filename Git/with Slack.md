# with Slask

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

### 남은 문제

slack DM 으로의 알림 설정을 통해 뷰 포인트가 줄어든 것은 매우 만족스러운데, 다른 멤버의 것까지 보이는 이슈가 있습니다.  
멤버들의 코드를 모두 리뷰한다는 관점에서 보면 괜찮지만, `나에 대한 모든 것`, `merge 된 모든 멤버의 소스` 을 보려던 초기의 생각에 비교하면 뜨는 알림의 수가 공해에 가깝게 되어 버렸습니다.

좀 더 찾은 내용으로는 label 을 filter 하는 기능이 있지만 이것은 마스터가 개인에 대한 label 을 만들어줘야되는 것이라 일을 위한 일이 되어버릴 것 같네요..

결론적으로는 그냥 삽질 이었다............................

당연히 보완책이 있을 것 같지만 이미 반나절 이상을 소비해버린 관계로 e-mail 알림이라도 제대로 설정한 것에 위안을 삼고 좋은 의견을 기다립니다. ㅠㅠ

## 참고자료

[GitHub + Slack Integration](https://github.com/integrations/slack)