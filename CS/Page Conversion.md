# 페이지 전환 Page Conversion

## Forward vs Redirect vs View 전환

|                   |                          Redirect                           |                      Forward                       |                   View 호출                   |
| ----------------- | :---------------------------------------------------------: | :------------------------------------------------: | :-------------------------------------------: |
| 요청 정보의 유지  |                             No                              |                        Yes                         |                      Yes                      |
| 클라이언트로 응답 |                             Yes                             |                         No                         |                      Yes                      |
| URL 의 변경       |                             Yes                             |                         No                         |                      No                       |
| 권장 사용 예시    | 시스템에 변화가 생기는 경우<br />(로그인, 회원가입, 글쓰기) | 시스템에 변화가 생기지 않는 경우<br />(조회, 검색) | 추가 Servlet 으로 이동하지 않고 응답하는 경우 |

### Forward
웹 서버 내에서 로직 처리를 위해 다른 서블릿으로 이동해야 되는 경우에 사용되며 정보를 (request, response) 그대로 전달합니다.

![forward](https://user-images.githubusercontent.com/55722186/75129305-bfa8f800-570b-11ea-9705-3690ca5e2e42.png)

### Redirect 
웹 서버는 클라이언트의 브라우저로 3XX 의 응답코드와 redirect 할 URL 을 알려주고, 브라우저는 해당 URL 로 이동합니다.
![redirect](https://user-images.githubusercontent.com/55722186/75129302-be77cb00-570b-11ea-820e-5b2906678c72.png)

### View 전환 (Response)
클라이언트의 브라우저가 이동할 페이지를 전달합니다.

> Forward 와 View 전환의 차이

Forward 는 웹서버 내에서의 이동을 뜻하며, View 전환은 클라이언트로의 응답을 뜻합니다.

## 참고 자료
https://doublesprogramming.tistory.com/63
