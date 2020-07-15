# Test

## Spring 에서 지원하는 Test 종류
- `@SpringBootTest` 를 통해 한번에 선언할 수 있으며, 목적에 맞게 Annotation 을 분리할 수도 있습니다
- Test 는 모든 단위가 독립적으로 수행되어야 합니다.
    - `@BeforeEach` 와 `@AfterEach` 를 통해 필요한 내용을 설정하고 원상 복구 시켜야 합니다. 

### @DataJpaTest
- JPA 테스트에 관련된 설정을 로드합니다.
- 기본적으로 인메모리 데이터베이스를 이용합니다.
- 초기 데이터는 Data.sql 을 통해 일괄적으로 추가합니다.

```java
package com.codessquad.qna.user;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import java.util.List;

import static org.junit.jupiter.api.Assertions.assertTrue;

@SpringBootTest
class UserJPATest {
  @Autowired
  private UserRepository userRepository;

  @Test
  void GET_USERS() {
    List<User> users = userRepository.findAll();
    assertTrue(users.size() == 2);
  }
}
``` 

### @RestClientTest
- REST API 테스트에 관련된 설정을 로드합니다.
- 키워드 : MockRestServiceServer, MockMvc

## 참고 자료
https://cheese10yun.github.io/spring-boot-test/  
https://daddyprogrammer.org/post/938/springboot2-restapi-unit-test/  
https://wedul.site/131  
https://jdm.kr/blog/165
