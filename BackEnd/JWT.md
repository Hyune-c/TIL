# JWT, Json Web Token

## Cookie, Session 의 문제점

- 정보의 위치
  - Cookie : Client
  - Sesseion : Server
- 서버가 여러 대일 경우 세션 정보의 동기화 문제가 발생합니다
- 세션을 통합 서버 또는 DB 에 저장하는 경우 과부하를 일으킬 수 있습니다
- Client 환경 변화 (앱, 하이브리드) 에 따른 유동적인 처리가 가능해야 합니다

## JWT 구성요소

> `[헤더header].[내용payload].[서명signature]`

### header

- alg : 토큰을 검증하기 위한 해싱 알고리즘
  - default : HS256
- typ : JWT 로 고정

### payload

- claim 이라고 표현되는 데이터가 들어 있습니다

### Signature

- Header 와 Payload 의 데이터 무결성과 변조 방지를 위함
- Header + Payload 를 합친 후, Secret 키와 함께 Header 의 해싱 알고리즘으로 인코딩

## Claim

### Registered Claim

> 필수는 아니지만 사용하기를 권장합니다

- "iss" (Issuer)
- "sub" (Subject)
- "aud" (Audience)
  - 사용 대상
- "exp" (Expiration Time)
  - Type : NumericDate
- "nbf" (Not Before)
  - Type : NumericDate
  - Token 의 유효함이 시작되는 시간입니다
- "iat" (Issued At)
  - Type : NumericDate
- "jti" (JWT ID)
  - 고유 식별자로 일회용 토큰에 사용하면 유용합니다

### Public Claim

- 충돌 방지를 위해 URI 형식으로 작성합니다
- `"https://velopert.com/jwt_claims/is_admin": true`

### Private Claim

- 사용자 정의 Claim

### JWT 의 단점

- Self-contained
  - 토큰 자체에 정보가 있다는 취약점
- 토큰 길이
  - payload 에 Claim set 을 저장하기 때문에 정보가 많아질수록 토큰의 길이가 늘어납니다
- payload 암호화
  - 암호화 되지 않은 payload 의 노출 위험성
  - JWE 를 통한 암호화, 또는 중요 데이터를 넣지 않아야 합니다
- Stateless
  - 토큰에 대한 제어가 불가능하기에 토큰 만료시간을 꼭 넣어주는게 좋습니다

## 참고 자료

- <https://tools.ietf.org/html/rfc7519#section-4.1>
- <https://sanghaklee.tistory.com/47>