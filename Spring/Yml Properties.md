# Yml Properties

## Dev, Prod 설정 따로 사용하기

> application.yml
  
- Server 에서 `-Dspring.profiles.active=prod` 환경변수를 통해 분리합니다
  - Local (Dev) 에서는 H2 를, Server (prod) 에서는 MYSQL 을 사용하고 있습니다  
  - Local 과 Server 는 서로 다른 client_id 와 cliendt_screat 을 가지고 있습니다

```properties
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

```properties
spring:
  profiles:
    active: dev

auth:
  client-id:
  client-secret:
...
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

생각 중..............
