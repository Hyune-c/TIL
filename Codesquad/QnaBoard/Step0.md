# 스프링 부트로 QA 게시판 구현 1
## 삽질들

### # MVCC 설정 에러
> MVCC 란

다중 버전 동시성 제어(multiversion concurrency control, MCC, MVCC), 다중 버전 병행 수행 제어는 데이터베이스 관리 시스템이 일반적으로 사용하는 동시성 제어 방식으로, 데이터베이스로의 동시 접근을 제공하고 프로그래밍 언어에서 트랜잭셔널 메모리를 구현한다.

> 에러 메세지
```
org.h2.jdbc.JdbcSQLNonTransientConnectionException: Unsupported connection setting "MVCC" [90113-200]
```

강의자료에 있던 dependency 는 maven 의 설정이어서 gradle 로 바꾸는 과정에서 version 명시하지 않으니 최신 버전인 1.4.200 으로 적용되었습니다. 

> 해결 방법

MVCC 설정은 1.4.200 이후부터는 적용되지 않는 것이기에 삭제하였습니다.

```
# DB Connection 설정 – application.properties
## 1.4.200 이전의 설정
spring.datasource.url=jdbc:h2:mem://localhost/~/java-qna;MVCC=TRUE;DB_CLOSE_ON_EXIT=FALSE
## 1.4.200 이후의 설정
spring.datasource.url=jdbc:h2:mem://localhost/~/java-qna;DB_CLOSE_ON_EXIT=FALSE
```

- 강의자료의 maven dependency
```java
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>1.4.192</version>
</dependency>
```
- 버전을 명시하지 않은 gradel dependencies
```java
dependencies {
    ...
    compile("org.springframework.boot:spring-boot-starter-data-jpa")
    compile("com.h2database:h2")
    ...
}
```

- 참고자료  
https://www.inflearn.com/questions/20296


### # H2 DB connect

> 문제 상황

강의 자료에 있는 `JDBC URL : jdbc:h2:~/java-qna` 로 접근하면 연결은 성공하나 User table 이 존재하지 않음.
 
> 해결 방법

왠지 in-memory 형태일 것 같아서 찍어 맞추기로 해결함.
강의 자료의 URL 은 영구 DB 일 것으로 추측되나 확실하지는 않습니다..

```
# JDBC URL
## 강의 자료
jdbc:h2:~/java-qna
## User table 이 보이는 URL
jdbc:h2:mem://localhost/~/java-qna
```

### # put 이 적용되지 않는 현상

> 문제 상황

put 호출이 되지 않습니다.

> 해결 방법

```
# application.properties
## GET,POST 외의 method 도 지원하게해주는 설정
spring.mvc.hiddenmethod.filter.enabled=true

# 수동으로 하는 방법
@RequestMapping(value = "/users/{id}", method = RequestMethod.PUT) 
```


