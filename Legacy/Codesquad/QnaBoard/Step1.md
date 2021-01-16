# 스프링 부트로 QA 게시판 구현 1
## step1. 회원 가입 및 사용자 목록 기능 구현

### # 기본 세팅 
- fork 된 git 주소를 clone 으로 가져옵니다. 
```shell script
 ls 
DesignPattern     MastersLvTest     java-monster-race
 git clone -b Hyune-c --single-branch https://github.com/Hyune-c/java-qna.git
Cloning into 'java-qna'...
remote: Enumerating objects: 26, done.
remote: Counting objects: 100% (26/26), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 110 (delta 0), reused 23 (delta 0), pack-reused 84
Receiving objects: 100% (110/110), 350.03 KiB | 591.00 KiB/s, done.
Resolving deltas: 100% (22/22), done.
 ls
DesignPattern     MastersLvTest     java-monster-race java-qna
```
- step1 branch 를 만듭니다.
```shell script
 git checkout -b step1
Switched to a new branch 'step1'
```
- remote repository 추가하기
```shell script
 git remote -v
origin  https://github.com/Hyune-c/java-qna.git (fetch)
origin  https://github.com/Hyune-c/java-qna.git (push)
 git remote add -t Hyune-c upstream https://github.com/code-squad/java-qna.git
 git remote -v                                                                
origin  https://github.com/Hyune-c/java-qna.git (fetch)
origin  https://github.com/Hyune-c/java-qna.git (push)
upstream        https://github.com/code-squad/java-qna.git (fetch)
upstream        https://github.com/code-squad/java-qna.git (push)
```

### # 기능 구현
#### 회원가입 기능 구현
- 회원하기 페이지는 static/user/form.html을 사용한다. ... complete
- static에 있는 html을 templates로 이동한다. ... complete
    - /user/form.html 파일을 이동해줍니다.
    - UserController 에 form 매핑을 추가해줍니다. 
- 사용자 관리 기능 구현을 담당할 UserController를 추가하고 애노테이션 매핑한다. ... complete
- @Controller 애노테이션 추가 ... complete
- 회원가입하기 요청(POST 요청)을 처리할 메소드를 추가하고 매핑한다. ... complete
    - /user/form.html 의 question form method 를 get 에서 post 로 바꿔줍니다.
- @PostMapping 추가하고 URL 매핑한다. ... complete
    - UserController 에 /user/create 매핑을 추가해줍니다. 
- 사용자가 전달한 값을 User 클래스를 생성해 저장한다. ... complete
- 회원가입할 때 전달한 값을 저장할 수 있는 필드를 생성한 후 setter와 getter 메소드를 생성한다. ... complete
- 사용자 목록을 관리하는 ArrayList를 생성한 후 앞에서 생성한 User 인스턴스를 ArrayList에 저장한다. ... complete
    - userList 를 만들어 관리합니다.
- 사용자 추가를 완료한 후 사용자 목록 페이지("redirect:/users")로 이동한다. ... complete

#### 회원목록 기능 구현
- 회원목록 페이지는 static/user/list.html을 사용한다. ... complete
- static에 있는 html을 templates로 이동한다. ... complete
- Controller 클래스는 회원가입하기 과정에서 추가한 UserController를 그대로 사용한다. ... complete
- 회원목록 요청(GET 요청)을 처리할 메소드를 추가하고 매핑한다. ... complete
- @GetMapping을 추가하고 URL 매핑한다. ... complete
    - UserController 에 user/list 매핑을 추가해줍니다.
- Model을 메소드의 인자로 받은 후 Model에 사용자 목록을 users라는 이름으로 전달한다. ... complete
- 사용자 목록을 user/list.html로 전달하기 위해 메소드 반환 값을 "user/list"로 한다. ... complete
- user/list.html 에서 사용자 목록을 출력한다. ... complete
- user/list.html 에서 사용자 목록 전체를 조회하는 방법은 다음과 같다. ... complete

#### 회원 프로필 정보보기
- 회원 프로필 정보 보기의 구현 흐름은 다음과 같다. ... complete
- 회원 프로필 보기 페이지는 static/user/profile.html을 사용한다. ... complete
- static에 있는 html을 templates로 이동한다. ... complete
- 앞 단계의 사용자 목록 html인 user/list.html 파일에 닉네임을 클릭하면 프로필 페이지로 이동하도록 한다. ... complete
- html에서 페이지 이동은 <a /> 태그를 이용해 가능하다. ... complete
- `<a href="/users/{{userId}}" />` 와 같이 구현한다. ... complete
- Controller 클래스는 앞 단계에서 사용한 UserController를 그대로 사용한다. ... complete
- 회원프로필 요청(GET 요청)을 처리할 메소드를 추가하고 매핑한다. ... complete
- @GetMapping을 추가하고 URL 매핑한다. ... complete
- URL은 "/users/{userId}"와 같이 매핑한다. ... complete
- URL을 통해 전달한 사용자 아이디 값은 @PathVariable 애노테이션을 활용해 전달 받을 수 있다. ... complete
- ArrayList에 저장되어 있는 사용자 중 사용자 아이디와 일치하는 User 데이터를 Model에 저장한다. ... complete
- user/profile.html 에서는 Controller에서 전달한 User 데이터를 활용해 사용자 정보를 출력한다. ... complete

#### HTML의 중복 제거
- index.html, /user/form.html, /qna/form.html 코드를 보면 header, navigation bar, footer 부분에 많은 중복 코드가 있다. 중복 코드를 제거한다. ... complete
    - templates 에 base.html 을 만들어 처리하였습니다. 
- URL과 html 쉽게 연결하기 ... working
    - base package 아래에 config와 같은 새로운 패키지 생성한다.
    - MvcConfig 이름으로 클래스를 생성해 다음과 같은 형태로 구현한다.

#### 질문하기 요구사항
- 사용자는 질문을 할 수 있어야 한다. ... complete

#### 질문목록 요구사항
- 모든 사용자는 질문 목록을 볼 수 있어야 한다. ... complete

#### 질문상세보기 요구사항
- 모든 사용자는 질문 상세 내용을 볼 수 있어야 한다. ... complete

### # step1 Refactoring
- 메소드명 정상화 ... complete
- @RequestMapping 대신 명시적인 @GetMapping @PostMapping 사용.  ... complete
- href 가 "#" 인 a tag 제거.  ... complete
- 저장 시 newline 이 붙도록 설정.  ... complete
- 코드의 일관성 정리 ... complete

### Heroku 배포
https://codesquad-qnaboard.herokuapp.com/
