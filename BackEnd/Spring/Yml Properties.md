# Yml Properties

## Profile 사용하기

> application.yml
  
- Server 에서 `-Dspring.profiles.active=prod` 환경변수를 통해 분리합니다
  - Local (Dev) 에서는 H2 를, Server (prod) 에서는 MYSQL 을 사용하고 있습니다  
  - Local 과 Server 는 서로 다른 client_id 와 cliendt_screat 을 가지고 있습니다

```gradle
...
---
spring:
  profiles: dev
  datasource:
    driverClassName: org.h2.Driver
    url: jdbc:h2:mem://localhost/sidedish_db;
    username: ******
    password: ******
  h2:
    console:
      enabled: true
auth:
  client-id: 31******
  client-secret: 43de******
jwt:
  salt: ******
---
spring:
  profiles: prod
  datasource:
    driverClassName: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/sidedish_db?autoReconnect=true&useSSL=false&useUnicode=true&characterEncoding=utf8
    username: ******
    password: ******
    ...
auth:
  client-id: 2807******
  client-secret: 62a3b******
jwt:
  salt: ******
```

## Yml 에 값을 저장하여 사용하기

> application.yml

```gradle
auth:
  client-id: ******
  client-secret: ******
```

> AuthProperties.java

```java
@Component
@ConfigurationProperties(prefix = "auth")
public class AuthProperties {

  @Value("${auth.client-id}")
  private String clientId;
  @Value("${auth.client-secret}")
  private String clientSecret;
  ... (Getter)
}
```

> Usage

```java
public class AuthService {

  private final AuthProperties authProperties;

  public AuthService(AuthProperties authProperties) {
    this.authProperties = authProperties;
  }

  public ResponseEntity<String> login() {
        ... authProperties.getClientId()
  }
```

## Yml 파일 나누기

application.yml

```properties
spring:
  profiles:
#    active: log, local, app
    active: log, prod, app
```

application-local.yml

```properties
spring:
  profiles: local
  datasource:
    platform: h2
    driver-class-name: org.h2.Driver
    username:
    password:
    url: jdbc:h2:tcp://localhost:9092/mem:testdb;MVCC=TRUE
    initialization-mode: always
  jpa:
    database-platform: H2
    show-sql: true
    hibernate:
      ddl-auto: create-drop
```

application-prod.yml

```properties
spring:
  profiles: prod
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    username:
    password:
    url: jdbc:mysql://localhost:3306/raider50g_db
    initialization-mode: always
  jpa:
    database: mysql
    database-platform: org.hibernate.dialect.MySQL5InnoDBDialect
    show-sql: true
    hibernate:
      ddl-auto: none
```

application-app.yml

```properties
spring:
  profiles: app
discord:
  token: NzA0Nj**************************
  apiUrl: https://discordapp.com/api
  userAgent: Raiders 50G Bot Agent
```

application-log.yml

```properties
spring:
  profiles: log
logging:
  level:
    root: debug
    sql: trace
  pattern:
    console: "%d{dd-MM-yyyy HH:mm:ss.SSS,Asia/Seoul} %magenta([%thread]) %highlight(%-5level) %logger.%M - %msg%n"
```
