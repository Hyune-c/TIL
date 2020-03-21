# Ground Rule

## # Repository

- FE, BE
  - <https://github.com/Hyune-c/signup>

## # Issue

- 제목
  - 구현 기능 요약
- 내용
  - 체크박스가 포함된 상세 구현 기능
  - 재가공된 참고할 문서
- Label
  - feature
  - 회고 : 키워드와 함께 작성하고, 완성되면 Wiki 로 이동합니다.

## # Branch

|        | Local                  | Orgin                                                                 |
| ------ | ---------------------- | --------------------------------------------------------------------- |
| URL    |                        | <https://github.com/Hyune-c/signup>                                   |  |
| Branch | 개인                     | 개인, dev, master                                                       |
| Rule   | - 개인의 Branch 에서 개발합니다. | - 완성된 feature 를 dev 에 PR 하여 테스트 합니다.<br>- dev 를 통과하면 master 에 PR 합니다. |

## # 커밋 메세지 가이드

> ### Header

- Commit Type
  - feat : 새로운 기능 추가
  - refactor : 코드 리팩토링
  - properties : 설정 변경과 문서 변경

- Subject
  - 변경된 내용 요약

> ### Body

- 변경된 파일명 : 메소드명
  - 변경된 내용 상세

> ### Footer

- #이슈번호

```text
feat : index page 구현

- index.java : returnIndex()
    - return 값으로 /resource/index.html 전달

#1
```

## # PR Guide

> ### Title

### [Hamill&Dan][HTTP 웹서버 구현하기] Step1 Submit

> ### Contents

## HTTP 웹서버 구현하기

### # Step 1 기능 구현 완료

- [x] Index 파일 읽기  
- [x] 회원가입 구현 
- [x] 로그인 구현 
- [x] 사용자 목록 페이지 구현 
- [x] Stylesheet 지원 구현 