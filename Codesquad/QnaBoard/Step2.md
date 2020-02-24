# 스프링 부트로 QA 게시판 구현 1
## step2. 데이터베이스 활용

### # 기본 세팅
#### branch 설정
- step2 branch 만들기
```shell script
 git checkout step2
Switched to branch 'step2'
```
- merge 된 upstream 에서 fetch 해오기
```shell script
 git fetch upstream Hyune-c
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From https://github.com/code-squad/java-qna
 * branch            Hyune-c    -> FETCH_HEAD
 * [new branch]      Hyune-c    -> upstream/Hyune-c
```
- branch step1 삭제
```shell script
 git branch -D step1
Deleted branch step1 (was 45201c2)
```
- branch Hyune-c 를 upstream/Hyune-c 로 rebase
```shell script
 git rebase upstream/Hyune-c
First, rewinding head to replay your work on top of it...
Fast-forwarded Hyune-c to upstream/Hyune-c.
```

#### H2 DB 설정
- build.gradle
```java
dependencies {
    ...
    compile("org.springframework.boot:spring-boot-starter-data-jpa")
    compile("com.h2database:h2")
    ...
}
```
- application.properties
```java
# DB Connection 설정
spring.datasource.url=jdbc:h2:mem://localhost/~/java-qna;DB_CLOSE_ON_EXIT=FALSE
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
# 실행 쿼리 보기 설정
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
# 테이블 자동 생성 설정
## 서버를 시작하는 시점에 DB 테이블을 drop후에 다시 생성하도록 설정하는 방법.
spring.jpa.hibernate.ddl-auto=create-drop
# h2 db console에 접근 설정
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

### # 기능 구현
- User 클래스를 DB 테이블에 매핑 ... complete
- 사용자 데이터에 대한 CRUD 구현 ... complete
- Controller에서 Repository 사용
    - 사용자 데이터 추가 ... complete
    - 사용자 목록 조회 ... complete
    - 사용자 조회 ... complete
    - 질문 데이터 조회 ... complete
    - 질문 목록 조회 ... complete
    - 질문 상세 조회 ... complete
- 회원정보 수정 ... complete

### # step2 Refactoring
- 변수 타입은 String 아닌 원형으로 저장합니다. (LocalDateTime) ... complete
- index 보다는 id 로 변경합니다. ... complete
- log4j2 를 적용합니다. ... complete
- error 페이지에 대한 설정. ... working
- request, forward, view 사용에 대한 변수명 재정의. ... complete 
- 2개의 paht 를 한개의 메소드로 mapping 하고 방법 ... working?
- index.html 에서 welcome.html 로 변경하면서 경로 수정 ... complete
- javadoc 을 활용한 주석 추가와 메소드 순서 변경 ... complete
