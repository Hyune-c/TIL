# 스프링 부트로 QA 게시판 구현 2
## step5. XHR과 AJAX

### # 기본 세팅
#### branch 설정

- step5 branch 만들기
- merge 된 upstream 에서 fetch 해오기

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

- [x] AJAX로 답변 추가 기능 구현
- [x] AJAX로 답변 삭제 기능 구현 
- [x] 답변 삭제 기능 버그 해결 
