# 스프링 부트로 QA 게시판 구현 2
## step 6. 페이지 나누기

### # 기본 세팅
#### branch 설정

- [x] step6 branch 만들기

### # step4 refactoring 
- [x] Iterator 의 형태보다는 Collection 의 형태를 가지도록 수정 
- [x] orError() 메소드명에 대한 개선
- [x] checkLoginOrError() 메소드 추가
- [x] Question 삭제 시 Answer 삭제 로직에 대한 개선
- [x] oldPassword 사용에 대한 개선 
    - update form 의 input tag 에서 바로 가져오기 위함으로 유지합니다.
- [ ] Bean 의 Equal() 오버라이딩시 id 값의 비교 개선
    - 개선 방법을 찾지 못해 다음 step 으로 넘깁니다.
- [ ] 매개변수로 Bean 넣지 않기 
    - 개선 방법을 찾지 못해 다음 step 으로 넘깁니다.
  
### # 기능 구현

- [ ] 질문을 한 페이지에 15개씩 가져오도록 구현합니다.
- [ ] 질문 목록은 생성일 기준 내림 차순으로 구현합니다.
- [ ] 시작 번호, 끝 번호 등을 구하고, 동적으로 html을 생성하는 로직 구현을 TDD로 구현해야 합니다.

### # 질문
 
