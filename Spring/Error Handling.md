# Error Handling

## ErrorController 를 implements 하는 방식
ErrorController 를 구현하는 CustomErrorController 를 만들어 에러에 동적으로 대응할 수 있습니다. 

### # CustomErrorController 예제
 ErrorController 를 구현하여 HttpStatus 에 동적으로 대응할 수 있는 로직을 가지고 있습니다.

```java
@Controller
@RequestMapping("/error")
public class CustomErrorController implements ErrorController {

  private static final String ERROR_PATH = "/error";

  @Override
  public String getErrorPath() {
    return ERROR_PATH;
  }

  @RequestMapping("")
  public String handleError(HttpServletRequest request, Model model) {
    Object status = request.getAttribute(RequestDispatcher.ERROR_STATUS_CODE);
    ...
  }
}
```

### # Exception() 발생 예제

- ForbiddenException   
 403 HTTP 에러를 나타내는 클래스 입니다.

```java
@ResponseStatus(value = HttpStatus.FORBIDDEN, reason = "잘못된 접근입니다.")
public class ForbiddenException extends RuntimeException {
}
```

```java
@PutMapping("/{id}")
public String update(@PathVariable long id, User newUser) {
  ...
  throw new ForbiddenException();
  ...
}
```  

## @ControllerAdvice 를 통해 구현하는 방식
@ControllerAdvice 와 @ExceptionHandler 를 통해 프로그램 전체의 에러를 처리할 수 있습니다.

```java
@ControllerAdvice
public class CustomErrorController {

  // 사용자 정의 에러 처리
  @ExceptionHandler(UserException.class)
  public String userException(Exception e, Model model) {
    ...
  }
    
  // 디폴트 에러 처리
  @ExceptionHandler(Exception.class)
  public String defaultException(Exception e, HttpStatus httpStatus, Model model) {
    ... 
  }
}
```

## 참고 자료
https://velog.io/@godori/spring-boot-error  
https://supawer0728.github.io/2019/04/04/spring-error-handling/
https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc
https://springboot.tistory.com/25
