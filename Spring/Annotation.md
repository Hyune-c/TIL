# Annotation

## @RequestParam vs @RequestBody vs @PathVariable
#### @RequestParam

- GET 방식으로 넘어온 URI의 queryString 을 받을 수 있게 해주는 어노테이션입니다.
 
```java
@GetMapping(path = "/reservations")
public Response<List<String>> getReservations
(@RequestParam(value = "reservationEmail",required = false) String reservationEmail) { ... }
```

#### @RequestBody

- POST 방식으로 넘어온 URI 의 body 부분을 객체로 받을 수 있게 해주는 어노테이션으로 주로 json 을 받을 때 사용됩니다.

```java
@PostMapping(path = "/reservations")
public Reservations setReservations
(@RequestBody ReservationParam reservationParam) { ... }
```

#### @PathVariable 

- URL 경로에 포함된 파라미터를 받을 수 있게 해주는 어노테이션으로 주로 REST API 구성시 사용됩니다. 

```java
@PutMapping(path = "/reservations/{reservationId}")
public Reservations cancleReservations
(@PathVariable(name = "reservationId") Integer reservationInfoId) { .. }
```


## javax.validation 빈 검증
> 실제 DB 에는 모두 not null 로 들어갑니다.

|            | @Notnull      | @NotEmpty     | @NotBlank     |
| :--------- | :------------ | :------------ | ------------- |
| null       | 허용하지 않음 | 허용하지 않음 | 허용하지 않음 |
| ""         | 허용          | 허용하지 않음 | 허용하지 않음 |
| " "(space) | 허용          | 허용          | 허용하지 않음 |

## 참고 자료
https://takeknowledge.tistory.com/39
