# Work Log #3

## 작업 내용

<https://github.com/Hyune-c/raider50g/pull/10>

> Object

- [x] `Booking`: 레이드 예약 Entity
- [x] `BookingCommand`: 예약을 위한 Input DTO

> API

- [x] /api/booking
  - `BookingCommand` 를 입력받아 `레이드 예약` 을 합니다
- [x] /api/channel/{channelName}
  - `channelName`, `raidDate` 를 입력 받습니다
  - `raidDate` 의 예약 인원을 `channelName` 에 게시합니다

## 다음 작업

- 예약 취소
- 초대 매크로
- 테스트 전략에 대한 생각
  - `H2 DB` 설정
  
## 회고

코드스쿼드 교육을 통해 시행 착오를 겪고나서야 프로젝트의 흐름이 머리속으로 그려지기 시작했습니다  
(기존의 구조와 흐름을 보니 심히 말도 안되는.. 또 시간이 지나면 같은 생각이 반복 되겠지만 ㅎㅎ)

그래서 이번 토이 프로젝트의 목표를 `Spring 에 대한 이해`와 `JPA, queryDSL 사용`, `테스트 전략` 으로 잡고, 관리 포인트가 많은 `Project` 대신 `Issue` 만 관리하면서 당장 필요한 목표만 하기로 방향을 바꿧습니다

이번 작업을 통해 드디어 실제 Discord 에 의미 있는 메세지를 보내는데 성공했고, 이제 발전시켜나갈 생각입니다
