# 스프링 부트로 QA 게시판 구현 2
## step4. 로그인 구현

### # 기본 세팅
#### branch 설정

- step4 branch 만들기
- merge 된 upstream 에서 fetch 해오기
- branch step3 삭제
- branch Hyune-c 를 upstream/Hyune-c 로 rebase

### # step3 Refactoring

- CommonUtils 변경
    - 로직의 명시성 강화를 위해 각 get 메소드에 OrError() 를 추가 ... complete
    - 각 소스에 static import 를 추가 ... complete

### # 기능 구현

- 회원과 질문간의 관계 매핑 및 생성일 추가
    - User와 Question 간의 관계를 매핑한다.   
        - 기존 userId 를 사용하던 방법에서 User 객체로 변경 ... complete
        - hidden input 추가로 userId, id 분리 ... complete
    - Question에 생성일을 추가한다. ... complete

-  질문 상세보기 기능
    - 질문 상세보기 기능 구현 ... complete

-  질문 수정, 삭제 기능 구현
    - PUT(수정), DELETE(삭제) HTTP method를 활용해 수정, 삭제 기능을 구현 ... complete

-  수정/삭제 기능에 대한 보안 처리 및 LocalDateTime 설정
    - Back End 프로그래밍에서 정말 중요한 보안 관련된 기능 구현 ... compelte
    - JPA에서 LocalDateTime을 DB 데이터타입과 제대로 매핑하지 못하는 이슈 해결 ... compelte

- 답변 추가 및 목록 기능 구현
    - 답변 기능을 담당할 Answer를 추가하고, Question, User와 매핑 ... compelete
    - Question에 Answer를 @OneToMany로 매핑. 이와 같이 매핑함으로써 질문 상세보기 화면에서 답변 목록이 동작하는 과정 공유 ... compelete

- QuestionController 중복 코드 제거 리팩토링
    - QuestionController에서 보안 처리를 위해 구현한 중복 코드를 제거 ... compelete
    - 중복을 Exception을 활용한 제거와 Result와 같은 새로운 클래스르 추가해 제거 ... compelete

- 질문 삭제하기 실습(선택)
    - 질문 데이터를 완전히 삭제하는 것이 아니라 데이터의 상태를 삭제 상태(deleted - boolean type)로 변경한다. ... complete
    - 질문을 삭제할 때 답변 또한 삭제해야 하며, 답변의 삭제 또한 삭제 상태(deleted)를 변경한다. ... complete
    - 로그인 사용자와 질문한 사람이 같은 경우 삭제 가능하다. ... complete
    - 답변이 없는 경우 삭제가 가능하다. ... complete
    - 질문자와 답변 글의 모든 답변자 같은 경우 삭제가 가능하다. ... complete
    - 질문자와 답변자가 다른 경우 답변을 삭제할 수 없다. ... complete

### # 질문
- 삭제 로직 중 댓글의 작성자 체크/삭제를 동시에 해야되다보니 answers 를 2번 불러오고 loop 도 2번 도는 형태가 되었습니다.   
    - 1개의 loop 에서 삭제를 처리하게 되면 rollback 이 힘들어 아래와 같은 로직을 선택하였는데 어떻게 하면 개선할 수 있을까요?  
    (혹시 여기에 @Transactional 을 사용하는 것인가요?)
    - answer 의 delete 마다 save 를 하게되면서 DB 접근이 많을 것으로 추정됩니다. 어떻게 줄여야될까요?

```java
Iterator<Answer> answers = getAnswersOrError(answerRepository, question).iterator();

// 댓글 중 작성자와 sessionedUser 가 다른 건이 있는지 체크합니다.
answers.forEachRemaining(answer -> {
  if (!answer.getUser().equals(sessionedUser)) {
    throw new QuestionException(CustomErrorCode.USER_NOT_MATCHED);
  }
});

// answers 를 다시 불러온 후 삭제를 진행합니다.
answers = getAnswersOrError(answerRepository, question).iterator();
answers.forEachRemaining(answer -> {
  answer.delete();
  answerRepository.save(answer);
});
```
