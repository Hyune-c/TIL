## Access Modifier 접근 한정자, 접근 제어자

| Modifier  | Class | Package | Subclass | World |
| --------- | ----- | ------- | -------- | ----- |
| public    | Y     | Y       | Y        | Y     |
| protected | Y     | Y       | Y        | N     |
| default   | Y     | Y       | N        | N     |
| private   | Y     | N       | N        | N     |

> 허용된 범위 밖에서 접근 시 compile error 가 발생합니다.