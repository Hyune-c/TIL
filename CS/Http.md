# Http

Http 는 상태를 유지하지 않는 stateless 한 프로토콜 입니다.

## Cookie vs Session  
stateless 의 문제점을 보완하기 위한 방식이지만, 두 방식 모두 보안의 위험이 존재하기에 토큰을 사용하는 OAuth, JWT 방식이 나왔습니다.  

|          | Cookie            | Session       |
| -------- | ----------------- | ------------- |
| Stored   | Browser in Client | Server        |
| Security | 변조의 위험성     | 탈취의 위험성 |

## URI vs URL vs URN

- URI 는 URL 과 URN 을 포함하는 슈퍼셋 입니다.

- URI (Uniform Resource Identifier) 는 통합 자원 식별자로최근에는 URL 과 혼용해서 쓰이기도 합니다.
- URL (Uniform Resource Locator) 은 자원의 위치을 뜻합니다.
- URN (Uniform Resource Name) 은 위치와 상관없이 리소스의 이름값을 이용해서 접근합니다.

#### URI 포맷

> URI
```
http://user:pass@www.example.jp:80/dir/index.htm?uid=1#ch1

scheme:[//[user:password@]host[:port]][/]path[?query][#fragment]
스키마://자격정보@서버주소:서버포트/계층적 파일 패스?쿼리 문자열#프래그먼트 식별자
```
> URL
```
http://user:pass@www.example.jp:80/dir/index.htm 
```

## Request, Response
![](../image/CS/Http%20Reqeust_Response.png)

### HTTP Headers
- 각 값들은 CR(carriage return, 0x0d) + LF(line feed, 0x0a) 를 기준으로 값이 나뉩니다.

### HTTP Body
- `empty line` 을 기준으로 나뉩니다.
- 한줄로 연속된 데이터를 가지고 있습니다. 
 
### # Request
- start line, request line
```
POST / HTTP/1.1
메소드 요청URL 프로토콜버전
```

### # Response
- status line
```
HTTP/1.1 200 OK 
프로토콜버전 상태코드 상태코드설명
```
#### 참고 자료
https://engkimbs.tistory.com/696  
https://velog.io/@pa324/%EA%B0%9C%EB%B0%9C%EC%83%81%EC%8B%9D-URI-URL-%EC%B0%A8%EC%9D%B4-%EC%A0%95%EB%A6%AC  
https://developer.mozilla.org/ko/docs/Web/HTTP/Messages
