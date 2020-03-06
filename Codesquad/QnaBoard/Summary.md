# Summary

1. spring boot로 로컬 개발 환경을 세팅할 수 있는가?
    - Spring Initializr 를 통해 세팅합니다.  
    https://start.spring.io/
    
2. mustache, handlebars와 같은 template engine의 역할을 이해했는가?
    - 템플릿 양식과 특정 데이터 모델에 따른 입력 자료를 합성하여 결과 문서를 출력하는 소프트웨어 또는 소프트웨어 컴포넌트를 말합니다.
    - mustache 는 logic-less 를 지향하며, handlebars 는 mustache 의 문법을 수용하며 helper 개념을 통해 로직 처리를 가능하게 해줍니다.
    
3.  MVC 패턴에서 model view controller 각각의 역할을 이해했는가?
    - model 은 로직 (무엇을), view 는 보여주는 화면, controller 는 요청에 적합한 컴포넌트 호출을 (어떻게) 합니다.
    - 각각의 개념은 서로의 영역을 침범하지 않습니다.
    
4. 웹 클라이언트에서 웹 서버에 요청을 보내고, 응답을 받는 흐름을 이해했는가?  
    - https://github.com/Hyune-c/TIL/blob/master/Spring/Http%20Request%20Flow.md

5. Spring MVC 기반으로 CRUD 기본 기능을 구현할 수 있는가?
    - CrudRepository 를 상속받는 interface 를 통해 구현할 수 있습니다.
    ```
    public interface QuestionRepository extends CrudRepository<Question, Long> {}
    ```

6.  javabean 표준에 대해 알고 있는가?
    - https://github.com/Hyune-c/TIL/blob/master/Java/JavaBean.md

7. ORM의 역할에 대해 이해했는가?
    - ORM (Object Relational Mapping)    
    - 사물을 추상화시켜 이해하려는 OOP 사고방식과 DataModel 을 정형화하여 관리하려는 RDB 사이를 연결할 계층의 역할로 제시된 패러다임으로 RDB 의 모델을 OOP 에 Entity 형태로 투영시키는 방식을 사용한다. 
    
- ORM 기반으로 CRUD 기능을 구현할 수 있는가?
    - CrudRepository 를 상속받는 Repository 를 만들어 @autowired 를 통해 할당하고 사용합니다.

- HTTP는 무상태 프로토콜이라는 말의 의미를 이해했는가?
    - HTTP 1.0 은 비연결성을 특징으로 가지고 있으며, 이 때문에 클라이언트의 상태를 알 수 없기에 stateless 입니다.

- HTTP는 상태를 유지하기 위해 cookie를 사용한다. cookie의 동작 방식을 이해했는가?
    - https://github.com/Hyune-c/TIL/blob/master/CS/Http.md

- cookie와 session의 차이점은 무엇인지 이해했는가?
    - https://github.com/Hyune-c/TIL/blob/master/CS/Http.md

- Spring MVC에서 Session을 활용해 로그인 기반 개발이 가능한가?
    - HttpSession 을 활용합니다.

- Logging 라이브러리 필요성을 이해했는가?
    - 네.

- Logging 라이브러리를 설정할 수 있는가?
    - https://github.com/Hyune-c/TIL/blob/master/Spring/Logging.md
