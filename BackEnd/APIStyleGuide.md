- [배경](#배경)
  - [REST API 란?](#rest-api-란)
- [리소스 중심 디자인. Resource Oriented Design](#리소스-중심-디자인-resource-oriented-design)
  - [리소스](#리소스)
  - [컨벤션](#컨벤션)
    - [공통](#공통)
    - [시간](#시간)
    - [수량](#수량)
- [API 설계](#api-설계)
  - [메소드](#메소드)
    - [권장되는 HTTP response code](#권장되는-http-response-code)
  - [API 설계](#api-설계-1)
    - [경로 중첩](#경로-중첩)
  - [페이지네이션](#페이지네이션)
  - [오류](#오류)
    - [오류 세부 정보](#오류-세부-정보)
- [기타](#기타)
  - [요청 번호. Request_Id](#요청-번호-request_id)

# 배경

> 본 가이드는 좋은 API 를 만들기 위한 철학을 유명 기업들의 가이드를 참고하고, 리소스 중심 디자인의 사고를 통해 HTTP 기반의 REST API 중심으로 작성하였습니다.  
제가 경험하고 고민한 것을 위주로 정리한 것이기에 일부 내용은 의도적으로 작성하지 않았습니다.

- Google 에서는 프로그래밍 언어, 운영체제 또는 네트워크 프로토콜에 관계없이 다양한 API 형태를 지원하기 위해 리소스 중심 디자인를 지향하지만, 이 경우 커스텀 메소드 구현 등, 난이도가 높습니다.
- 세부적인 Header, 스키마 관리, 버전 관리, HATEOAS 등은 필요할 때 더 공부합니다.
- 참고 <http://apistylebook.com>

## REST API 란?

- 개별적으로 주소 지정이 가능한 리소스의 컬렉션으로 모델링됩니다.
- 이미 알려진 메소드를 사용함으로서 리소스와 리소스 관계에만 집중할 수 있습니다.
  - POST, GET, PUT, PATCH, DELETE

# 리소스 중심 디자인. Resource Oriented Design

## 리소스

리소스는 단순 리소스 (이하 리소스) 와 단순 리소스의 집합 (이하 컬렉션) 으로 구분됩니다.

- 리소스는 상태와 0개 이상의 하위 리소스를 갖습니다.
- 각 하위 리소스는 리소스 또는 컬렉션이 될 수 있습니다.
- 유연성을 위해 DB 테이블과 일치하지 않아도 됩니다.
- 메소드 (기능) 보다 리소스 (데이터 모델) 를 강조합니다.

## 컨벤션

### 공통

- 정확한 미국 영어로 단순, 직관, 일관적이어야합니다.
- 컬렉션은 복수형, lowerCamelCase 를 사용합니다.
  - 적절한 복수 형태가 없거나, 불가산 명사의 경우 단수를 사용합니다.
- 전치사를 포함하지 않습니다.
- 예약어와 지나치게 일반적인 용어는 사용하지 않습니다.
  - 지나치게 일반적인 용어의 예: elements, entries, instances, items, objects, resources, types, values
  - ex) values 보다 rowValues
  - ex) name 보다 title, full_name
  
### 시간

- 이름
  - 필드 이름은 suffix 로 time 을 가집니다.
  - 필요한 경우 verb_time 형태를 가지며, 시제를 사용하지 않습니다.
    - created_time -> create_time
    - last_updated_time -> update_time
- 값
  - RFC, ISO 표준을 따릅니다.
    - 연월일시분초: RFC 3339 (2014-07-30T10:43:17Z)
    - 연월일: ISO 8601 (YYYY-MM-DD, 2014-07-30)
    - 시분초: ISO 8601 (HH:MM:SS[.FFF], 14:55:01.672)

### 수량

- 필드 이름은 suffix 로 count 를 가집니다.

# API 설계

## 메소드

|  Name  | Resource Type  | Request Body(Payload) | Response Body(Payload) | 안전한 | 멱등성 |
| ------ | -------------- | --------------------- | ---------------------- | ------ | ------ |
| GET    | 리소스, 컬렉션 | 없음                  | 리소스, 컬렉션 또는 ID | O      | O      |
| POST   | 컬렉션         | 리소스                | 리소스, 컬렉션 또는 ID | X      | X      |
| PUT    | 리소스         | 리소스                | 리소스 또는 ID         | X      | O      |
| PATCH  | 리소스         | 리소스                | 리소스 또는 ID         | X      | X      |
| DELETE | 리소스         | 없음                  | 없음                   | X      | O      |

- 공통
  - Response 에는 리소스 전체를 내려줄 수도 있지만, 성능 최적화를 위해 리소스 ID 만, 또는 NO_CONTENTS 를 응답할 수도 있습니다.

- PATCH
  - 필요한 리소스의 값만 수정함으로서 역할을 세분화할 수 있습니다.
  - 부분적인 리소스 값만 받기에 PUT 과 달리 리소스를 생성할 수 없습니다.  
  따라서 멱등하지 않습니다.

### 권장되는 HTTP response code

| Method | 200 | 201 | 204 | 400 | 404 | 5XX |
| ------ | --- | --- | --- | --- | --- | --- |
| GET    | O   |     |     | O   | O   | O   |
| POST   | O   | O   |     | O   |     | O   |
| PUT    | O   |     | O   | O   | O   | O   |
| PATCH  | O   |     | O   | O   | O   | O   |
| DELETE | O   |     | O   | O   | O   | O   |

## API 설계

```text
// REST API HTTP URI, End Point
https://calendar.googleapis.com/v3/users/john%20smith/events/123
```

### 경로 중첩

중첩된 부모/자식 리소스 관계의 경로 중첩을 최소화 합니다.

```java
// Bad
/orgs/{org_id}/apps/{app_id}/dynos/{dyno_id}

// Good
/orgs/{org_id}
/orgs/{org_id}/apps
/apps/{app_id}
/apps/{app_id}/dynos
/dynos/{dyno_id}
```

## 페이지네이션

- 기술보다는 사용자의 경험을 먼저 생각해야됩니다.
- 장단점이 뚜렷하기에 선택적으로 사용해야합니다.

|                    |                     Offset                     |                   Cursor                   |           설명            |
| ------------------ | ---------------------------------------------- | ------------------------------------------ | ------------------------- |
| 효율성             | 나쁘다                                         | 좋다                                       | 특히 NoSQL, 대용량 처리시 |
| 범용성, 사용성     | 보편적                                         | 선별적                                     |                          |
| 특정 페이지로 이동 | 가능                                           | 불가능                                     |                           |
| 오류 가능성        | 리소스 삽입/삭제시 중복/누락이 될 수 있습니다. | Cursor 삭제시 오류가 발생할 수 있습니다. |                           |

## 오류

> Http response code 만으로 표현되지 않는 오류는 payload 에 오류 세부 정보 등을 내려보낼 수 있습니다.

HTTP 와 RPC 는 서로 다른 프로토콜임으로 오류 정보도 달리 표현됩니다.

### 오류 세부 정보

- 약속된 상세 오류 코드를 통해 클라이언트의 로직을 작성할 수 있습니다.
- 오류 메세지를 통해 클라이언트에서 사용자에게 보여줄 수도 있습니다.

# 기타

## 요청 번호. Request_Id

- 주로 결제에서 많이 쓰이는 방법으로 중복 결제를 방지합니다.
  1. 클라이언트는 결제 준비 API 호출을 통해 요청 번호를 발급받습니다.
  2. 클라이언트는 요청 번호를 포함한 실 결제 API 호출을 통해 결제를 합니다.
- 일반 서비스 API 호출에서도 응답 값에 넣어줌으로서 로그 추적을 용이하게 할 수 있습니다.
