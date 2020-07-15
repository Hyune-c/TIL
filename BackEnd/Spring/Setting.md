# Setting

## Spring Initializr

[링크](https://start.spring.io/)

## H2 DB

- build.gradle

```java
dependencies {
    ...
    implementation 'com.h2database:h2:1.4.200'
    ...
}
```

- application.properties

```java
# DB Connection 설정
spring.datasource.url=jdbc:h2:mem://localhost/signup_db;DB_CLOSE_ON_EXIT=FALSE
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# h2 db console에 접근 설정
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

## logback

SpringBoot 에는 기본 설정이 되어 있습니다.

- application.properties

```java
# profile 설정
spring.profiles.active=dev
```

- application-dev.properties

```java
# logging level 설정
logging.level.root=info
logging.level.com.codesquad.signup=debug

# log file path
logging.file.path=./logs
logging.file.name=${logging.file.path}/dev_log.log

# logging pattern
logging.pattern.file=%d{dd-MM-yyyy HH:mm:ss.SSS} [%thread] %-5level %logger{36}.%M - %msg%n
logging.pattern.console=%d{dd-MM-yyyy HH:mm:ss.SSS} %magenta([%thread]) %highlight(%-5level) %logger.%M - %msg%n
```

## Heroku

- Deploy - Automatic deploys enable
- Manual deploy - master
- More - View Logs
  
## 참고 자료

- logback
  - <https://lankydan.dev/2019/01/09/configuring-logback-with-spring-boot>
- log4j2
  - <https://logging.apache.org/log4j/2.x/maven-artifacts.html>
  - <https://howtodoinjava.com/log4j2/log4j2-properties-example/>

-----------------

## 구 설정 (검토 후 삭제될 것 들 입니다.)

- application.properties

```properties
handlebars.suffix=.html
handlebars.cache=false
# debug=true
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
## 서버를 시작하는 시점에 DB 테이블을 drop 후에 다시 생성하도록 설정하는 방법
spring.jpa.hibernate.ddl-auto=create-drop
# h2 db console에 접근 설정
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
# GET,POST 외의 method 도 지원하게해주는 설정
spring.mvc.hiddenmethod.filter.enabled=true
```

### log4j2

- build.gradle

```properties
configurations {
    ...
    all {
        // log4j2 로깅 설정 : 중복되는 logging 제거
        exclude group: 'org.springframework.boot', module: 'spring-boot-starter-logging'
    }
    ...
}

dependencies {
    ...
    // log4j2 로깅 설정
    compile group: 'org.apache.logging.log4j', name: 'log4j-api', version: '2.13.0'
    compile group: 'org.apache.logging.log4j', name: 'log4j-core', version: '2.13.0'

    // slf4j 설정
    compile group: 'org.apache.logging.log4j', name: 'log4j-slf4j-impl', version: '2.13.0'
    ...
}
```

- log4j2.properties

```properties
status=error
name=PropertiesConfig
filters=threshold
filter.threshold.type=ThresholdFilter
filter.threshold.level=debug
appenders=console
appender.console.type=Console
appender.console.name=STDOUT
appender.console.layout.type=PatternLayout
appender.console.layout.pattern=%d{yyyy-MM-dd HH:mm:ss} %-5p %c{1}:%L - %m%n
rootLogger.level=info
rootLogger.appenderRefs=stdout
rootLogger.appenderRef.stdout.ref=STDOUT
```

- 예제

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class WelcomeController {

  private static final Logger log = LoggerFactory.getLogger(WelcomeController.class);

  public String welcome(Model model) {
    log.debug("### welcome debug log message");
    log.info("### welcome info log message");

    return "/welcome";
  }
}
```
