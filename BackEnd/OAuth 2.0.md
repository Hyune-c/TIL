# OAuth 2.0

## 구성

> RFC 에는 Authorization Server 로 인증을 담당하는 서버가 따로 있지만,  
> 아래의 문서에서는 Resource Server 가 같은 역할을 하는 것으로 기록합니다

|     | Resource Owner | Client                                               | Resouce Server                                                                                                                                             |
| --- | -------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 역할  | 사용자            | 개발자, App                                             | 자원을 가지고 있는 서버                                                                                                                                              |
| 정보  |                | - Client ID <br> - Client Secret <br> - Access Token | - Client ID <br> - Client Secret <br> - Authorized redirect URIs <br> - 허용된 권한 (Client ID - user_id - scope) <br> - Authorization code <br> - Access Token |

- Client ID : Client 식별자, 노출되어도 됨
- Client Secret : Client 비밀번호, 노출되면 안됨
- Authorized redirect URIs : Resouce Server 에서 저장하는 Client 주소
  - <https://client/callback>
- Authorization code : Access Token 을 얻기 위한 임시 코드
- Access Token : Client 에서 사용하는 실 Token

## 흐름

> 이하의 문서에서는 Resource Owner 를 Owner 로, Resource Server 를 Server 로 표현합니다

### # Resource Owner 의 승인

1. Client 는 Owner 가 Server 로 접근 가능한 URL 을 제공합니다
    - <https://resource.server/?client_id=1&scope=B,C&redirect_uri=https://client/callback>
2. Owner 는 URL 을 통해 Server 로 접근합니다
   - 로그인이 되어 있지 않다면 Server 는 로그인을 요청합니다
3. Server 는 URL 의 client_id 와 redirect_url 을 검사합니다
   - client_id 가 없거나, redirect_url 과 맞지 않다면 작업을 중지합니다
4. Server 는 Owner 에게 Url 에 있는 scope 를 부여할 것인지 확인 요청을 보냅니다
5. Server 는 Ownere 가 허용시 user_id, Clinet_id, scope 를 저장합니다

> `Resource Server 의 승인` 으로 이어집니다

### # Resource Server 의 승인

1. Server 는 Owner 로 rediect 할 URL 응답합니다
   - Location : <https://client/callback?code=3>
   - 이 때 Authorization code 를 같이 전달합니다
2. Owner 는 인지하지 못하지만 redirect 를 통해 Client 로 Authorization code 가 전달됩니다
3. Client 는 Authorization code 를 포함하여 Access Token 을 얻기 위한 요청을 Server 합니다
    - <https://resource.server/token?grant_type=authorization_code&code=3&redirect_uri=https://client/callback&client_id=1&client_secret=2>
4. Server 는 Authorization code 를 보고 발급한 정보가 맞는지 확인합니다

> `Access Token` 으로 이어집니다

### # Access Token

1. 유효한 Authorization code 인 경우 Server 에서는 사용된 code 를 삭제합니다

2. Server 는 Access Token 을 Client 로 응답합니다

## 질문

- (Client 의 입장에서) Authorization code 까지는 Server 에서 준 값을 redirect 하여 오기 때문에 user_id 와의 매칭이 필요 없지만, Access Token 이 발급된 시점에는 해당 Token 이 어떤 user_id 의 것인지 매칭이 필요할 것으로 예상됩니다  
하지만 강의 자료에는 user_id 와의 매칭이 없었습니다
