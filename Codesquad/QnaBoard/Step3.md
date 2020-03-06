# 스프링 부트로 QA 게시판 구현 1
## step3. 로그인 구현

### # 기본 세팅
#### branch 설정

- step3 branch 만들기
- merge 된 upstream 에서 fetch 해오기
- branch step1 삭제
- branch Hyune-c 를 upstream/Hyune-c 로 rebase

### # step2 Refactoring
- 2개의 path 를 한개의 메소드로 mapping 하는 방법 ... working?
- error 처리/페이지에 대한 설정. ... complete
    - CustomErrorController 추가
    - 403 처리 Exception 추가 (ForiddenException)
    - errorPage.html 추가
    - 400, 403, 404, 500 에러에 대한 이미지 추가
- DateTimeFormatter 한번만 선언 ... complete
- Controller returnView 의 변수 선언 지양 ... complete
- Optional 사용시 get() 사용 지양 (강제 Unwrapping) ... complete
- lombok 을 통한 logging 간소화 ... complete


### # Handlebars
https://github.com/Hyune-c/TIL/blob/master/Spring/Handlebars.md

### # log 가독성 높이기
- log4j2.properties
```
appender.console.layout.pattern=%style{%d{yyyy-MM-dd hh:mm:ss:SSS}} %highlight{%-5level }[%style{%t}{bright,blue}] %style{%C{1.}}{bright,yellow}: %msg%n%throwable"
```

- Grep Console 
    - 커스텀 하이라이트 가능

### # 기능 구현
- Handlebars 전환 ... compelte
- 초기 데이터 만들기 
    - .../resource/data.sql 생성 ... complete
- 로그인 기능 구현
    - 로그인 상태이면 상단 메뉴에 “로그아웃”, “개인정보수정” 이 나타나야 합니다. ... complete
    - 로그아웃 상태이면 상단 메뉴에 “로그인”, “회원가입” 이 나타나야 한다. ... complete
- 개인정보 수정
    - 이름, 이메일은 수정할 수 있으며, 아이디는 수정할 수 없습니다. ... complete
    - 글 수정은 비밀번호가 일치하는 경우에만 가능합니다. ... complete
- 질문 기능 구현 실습
    - 질문은 모두가 볼 수 있습니다. ... complete
    - 질문 작성은 로그인한 사용자만 가능합니다. ... complete
    - 글 수정/삭제는 자신의 것만 가능합니다. ... compelte
- User와 Question 연결 실습(선택) ... compelte
    - 현재 Question의 글쓴이는 User의 name 값을 가지는 것으로 구현했다.  
    이와 같이 구현하는 경우 User의 name을 수정하는 경우 Question의 글쓴이와 다른 값을 가지는 문제가 발생한다.  
    이 문제를 해결하기 위해 User의 name이 변경될 때마다 Question의 writer 값을 수정할 수도 있지만 이와 같이 구현할 경우 writer가 같은 이름을 가지는 경우 문제가 될 수 있다.  
    이 같은 문제 상황에 대해 원론적으로 문제가 발생하지 않도록 해결한다.
- Answer 구현하기 실습(선택)
    - 답변 목록은 모두가 볼 수 있습니다.
    - 답변 작성은 로그인한 사용자만 가능합니다.
    - 답변 삭제는 자신의 것만 가능합니다.    

### # 질문

- 글 작성 날짜를 처리함에 있어 get() 메소드의 수정과 return 값을 변경하는 것이 걸려 @DateTimeFormat 를 활용해보려 했습니다.
    - 검색을 해보니 mvc configuration 을 만들어주어야 된다는 내용이 있던데.. 시도해보다 실패했습니다.      
    컴파일 에러는 발생하지 않는데, 필수적으로 설정해야되는 것이 맞나요?
- 최종적인 목표는 bean 과 DB 안에는 LocalDateTime 형태이고, .hbs 로 출력할때는 지정된 format 으로 나가는 것 입니다. (get 메소드의 조작 없이) 
    - 아래의 방법은 json 처리를 위한 직렬화 작업이라고 나오던데, 제가 필요없는 접근을 하고 있는 걸까요?   

```java
  // 원래 소스
  private LocalDateTime createdDateTime;

  public String getCreatedDateTime() {
    DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");
    return createdDateTime.format(dateTimeFormatter);
  }
```
```java
  // 의도한 소스
  @DateTimeFormat(iso = DateTimeFormat.ISO.NONE)
  private LocalDateTime createdDateTime;
```
```java
  // 검색하여 찾은 get() 메소드 formatting 의 다른 방법
  @JsonFormat(shape=JsonFormat.Shape.STRING, pattern="dd/MM/yyyy")
  public LocalDateTime getCreatedDateTime() {
    return createdDateTime;
  }
```
