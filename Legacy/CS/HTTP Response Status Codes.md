# HTTP Response Status Codes

HTTP 응답 상태 코드는 특정 HTTP 요청이 성공적으로 완료되었는지 알려줍니다.

| Status Code | Name                    | Class        | Desc                                                              |
| ----------- | ----------------------- | ------------ | ----------------------------------------------------------------- |
| 1XX         | Informational responses | Inforational | the request was received, continuing process                      |
| 2XX         | Successful responses    | Success      | the request was successfully received, understood, and accepted   |
| 3XX         | Redirects               | Redirection  | further action needs to be taken in order to complete the request |
| 4XX         | Client errors           | Client Error | the request contains bad syntax or cannot be fulfilled            |
| 5XX         | Server errors           | Server Error | the server failed to fulfil an apparently valid request           |

### Successful Responses

| Status Code | Reason Message  | Name   | Desc                                | Desc2 |
| ----------- | --------------- | ------ | ----------------------------------- | ----- |
| 200         | OK              | 성공     |                                     |       |
| 204         | No Content      | 콘텐츠 없음 | 서버가 요청을 성공적으로 처리했지만 콘텐츠를 제공하지 않습니다. |       |
| 206         | Partial Content | 일부 콘텐츠 | 서버가 GET 요청의 일부만 성공적으로 처리했습니다.       |       |

### Redirects

| Status Code | Reason Message     | Name     | Desc                                                                                         | Desc2    |
| ----------- | ------------------ | -------- | -------------------------------------------------------------------------------------------- | -------- |
| 301         | Moved Permanently  | 영구 이동    | 요청한 페이지가 새 위치로 영구적으로 이동했습니다.                                                                 | Redirect |
| 302         | Found              | 임시 이동    | 현재 서버가 다른 위치의 페이지로 요청에 응답하고 있지만 요청자는 향후 요청 시 원래 위치를 계속 사용해야 합니다.                             | Redirect |
| 303         | See Other          | 기타 위치 보기 | 요청자가 다른 위치에 별도의 GET 요청을 하여 응답을 검색할 경우 서버는 이 코드를 표시합니다. HEAD 요청 이외의 모든 요청을 다른 위치로 자동으로 전달합니다. |          |
| 304         | Not Modified       | 수정되지 않음  | 마지막 요청 이후 요청한 페이지는 수정되지 않았습니다.                                                               |          |
| 307         | Temporary Redirect | 임시 리다이렉션 | 현재 서버가 다른 위치의 페이지로 요청에 응답하고 있지만 요청자는 향후 요청 시 원래 위치를 계속 사용해야 합니다.                             |          |

### Client errors

| Status Code | Reason Message | Name    | Desc                                   | Desc2 |
| ----------- | -------------- | ------- | -------------------------------------- | ----- |
| 400         | Bad Request    | 잘못된 요청  | Request 가 해석되지 않는 경우                   |       |
| 401         | Unauthorized   | 권한 없음   | 실제 뜻은 인증 안됨(Unauthenticated)에 더 가깝습니다. |       |
| 403         | Foebidden      | 금지됨     | Request 는 정상이지만 권한이 없는 경우              |       |
| 404         | Not Found      | 찾을 수 없음 |                                        |       |

### Server errors

| Status Code | Reason Message        | Name          | Desc | Desc2 |
| ----------- | --------------------- | ------------- | ---- | ----- |
| 500         | Internal Server Error | 내부 서버 오류      |      |       |
| 503         | Service Unavailable   | 서비스를 사용할 수 없음 |      |       |
