# External Properties

> 민감 정보를 관리할 수 있는 방법 중 외부 파일을 참조하는 것에 대해 작성하였습니다

## Source

> resources/application.properties

```properties
discord.token={your token}
```

application.properties 를 gitignore 함으로서 민감정보를 보호할 수 있습니다

> com/hyune/raider50g/config/Properties.java

```java
@Component
public class Properties {

  private static String BOT_TOKEN;

  public static String getBotToken() {
    return BOT_TOKEN;
  }

  @Value("${discord.token}")
  public void setBotToken(String botToken) {
    BOT_TOKEN = botToken;
  }
}
```

> com/hyune/raider50g/Raider50gApplication.java

```java
@SpringBootApplication
public class Raider50gApplication {

  public static void main(String[] args) {
    SpringApplication.run(Raider50gApplication.class, args);

    String token = Properties.getBotToken();
    log.debug("### token : {} ", token);
  }
}

```

## 참고 자료

<https://www.baeldung.com/spring-inject-static-field>