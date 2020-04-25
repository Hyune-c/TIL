# Yml Properties

## Dev, Prod 설정 따로 사용하기

> application.yml

- Local (Dev) 에서는 H2 를, Server (prod) 에서는 MYSQL 을 사용하고 있습니다  
  - Server 에서는 `-Dspring.profiles.active=prod` 환경변수를 통해 분리합니다

```properties
spring:
  profiles:
    active: dev

---
spring:
  profiles: dev
  datasource:
    driverClassName: org.h2.Driver
    url: jdbc:h2:mem://localhost/sidedish_db;
    ...
  h2:
    console:
      enabled: true
---
spring:
  profiles: prod
  datasource:
    driverClassName: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/sidedish_db?autoReconnect=true&useSSL=false&
    ...
```

## Yml 에 값을 저장하여 사용하기

> application.yml

```properties
spring:
  profiles:
    active: dev

auth:
  client-id: 31ae5169a7dc37e19605
  client-secret: 43debfbf5b584d5a0c7b58d215c5462a29ecd5e1
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
  ... (Getter, Setter)
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

## 환경변수에 따른 호출 값 변경

실패 중..............

## Yml 파일 나누기

생각 중..............
