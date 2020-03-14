# HTTP 웹서버 구현하기

## HTTP 웹 서버 1단계 - 구현

### # 기능 구현
- [ ] http://localhost:8080/index.html 로 접속했을 때 webapp 디렉토리의 index.html 파일을 읽어 클라이언트에 응답합니다.
- [ ] "회원가입" 메뉴를 클릭하면 http://localhost:8080/user/form.html 으로 이동하면서 회원가입할 수 있습니다
    - [ ] 회원가입을 하면 다음과 같은 형태로 사용자가 입력한 값이 서버에 전달됩니다.
        ```  
        /create?userId=javajigi&password=password&name=%EB%B0%95%EC%9E%AC%EC%84%B1&email=javajigi%40slipp.net
        ```
    - [ ] HTML과 URL을 비교해 보고 사용자가 입력한 값을 파싱해 model.User 클래스에 저장합니다.
- [ ] 회원가입 기능이 정상적으로 동작하도록 구현합니다.      
    - [ ] http://localhost:8080/user/form.html 파일의 form 태그 method 를 get 에서 post 로 수정합니다.
    
- [ ] "회원가입"을 완료하면 /index.html 페이지로 이동합니다. 
    - [ ] 브라우저의 URL이 /index.html 로 변경되어야 합니다.
      
- [ ] "로그인" 메뉴를 클릭하면 http://localhost:8080/user/login.html 으로 이동해 로그인할 수 있습니다. 
    - [ ] 로그인이 성공하면 index.html 로 이동합니다.
    - [ ] 로그인이 실패하면 /user/login_failed.html 로 이동합니다.
    
- [ ] 앞에서 회원가입한 사용자로 로그인할 수 있어야 하며, 요청 header 의 Cookie header 값이 변경되어야 합니다.
    - [ ] 로그인 성공시 : logined=true
    - [ ] 로그인 실패시 : logined=false
        
- [ ] 사용자 목록 페이지로의 이동을 구현합니다.  
    - [ ] Cookie 값이 logined=true : http://localhost:8080/user/list 로 접근했을 때 사용자 목록을 출력합니다. 
    - [ ] Cookie 값이 logined=false : login.html 로 이동합니다.
      
- [ ] Stylesheet 파일을 지원하도록 구현합니다.
