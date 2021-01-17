# Design Guidelines

## 배경

> Google 에서는 프로그래밍 언어, 운영체제 또는 네트워크 프로토콜에 관계없이 다양한 API 형태를 지원하기 위해서는 리소스 중심 디자인를 지향합니다.  
하지만 이 경우 커스텀 메소드 등, 구현의 난이도가 올라갑니다.

본 가이드는 HTTP 기반의 REST API 을 중심으로 작성하였지만, 리소스 중심 디자인의 철학도 고려하였습니다.

### REST API 란?

- 개별적으로 주소 지정이 가능한 리소스의 컬렉션으로 모델링됩니다.
- 이미 알려진 메소드를 사용함으로서 리소스와 리소스 관계에만 집중할 수 있습니다.
  - POST, GET, PUT, PATCH, DELETE

## 리소스 중심 디자인. Resource Oriented Design

### 리소스. Resource

리소스는 단순 리소스 (이하 리소스) 와 단순 리소스의 집합 (이하 컬렉션) 으로 구분됩니다.

- 리소스는 상태와 0개 이상의 하위 리소스를 갖습니다.
- 각 하위 리소스는 리소스 또는 컬렉션이 될 수 있습니다.
- 유연성을 위해 DB 테이블과 일치하지 않아도 됩니다.
- 메소드 (기능) 보다 리소스 (데이터 모델) 를 강조합니다.

### 컨벤션. Convention

> 공통

- 정확한 미국 영어로 단순, 직관, 일관적이어야합니다.
- 컬렉션은 복수형, lowerCamelCase 를 사용합니다.
  - 적절한 복수 형태가 없거나, 불가산 명사의 경우 단수를 사용합니다.
- 전치사를 포함하지 않습니다.
- 예약어와 지나치게 일반적인 용어는 사용하지 않습니다.
  - 지나치게 일반적인 용어의 예: elements, entries, instances, items, objects, resources, types, values
  - ex) values 보다 rowValues
  - ex) name 보다 title, full_name
  
> 시간

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

> 수량

- 필드 이름은 suffix 로 count 를 가집니다.

### Resource Name vs URL

- 리소스 네임에 API 버전, API 프로토콜이 매핑됨으로서 URL 이 됩니다.
- 리소스 중심 디자인에서는, API 세분화를 위해 커스텀 메소드를 구현합니다.
  - 하지만 리소스 네임에 동사를 포함시켜 구현 난이도를 낮출 수 있습니다. 이 경우 리소스 네임보다는 API 구조라고 표현합니다.

```text
// Resource Name
//calendar.googleapis.com/users/john smith/events/123

// REST API HTTP URL, End Point
https://calendar.googleapis.com/v3/users/john%20smith/events/123
```
  
## 메소드. Method

|    Name    | Resource Type  | Request Body(Payload) | Response Body(Payload) |
| ---------- | -------------- | --------------------- | ---------------------- |
| GET        | 리소스, 컬렉션 | 없음                  | 리소스, 컬렉션 또는 ID |
| POST       | 컬렉션         | 리소스                | 리소스, 컬렉션 또는 ID |
| PUT, PATCH | 리소스         | 리소스                | 리소스 또는 ID         |
| DELETE     | 리소스         | 없음                  | 없음                   |

### 수정. PUT, PATCH

- 역할을 세분화할 수 있습니다.
  - 내용을 수정하는 것과, 순서만 바꾸는 것을 서로 다른 API 로 세분화할 수 있습니다.
- 멱등성을 위해 리소스 ID 가 존재해야합니다.

## 오류. Error

> Http response code 만으로 표현되지 않는 오류는 payload 에 오류 세부 정보 등을 내려보낼 수 있습니다.

HTTP 와 RPC 는 서로 다른 프로토콜임으로 오류 정보도 달리 표현됩니다.

### 오류 세부 정보. Error Details

- 약속된 상세 오류 코드를 통해 클라이언트의 로직을 작성할 수 있습니다.
- 오류 메세지를 통해 클라이언트에서 사용자에게 보여줄 수도 있습니다.
