# Handlebars

## Handlebars vs Mustache

- Mustache 

로직 처리를 할 수 있는 코드 가공에 제약이 있습니다.

- Handlebars 

사용자 정의 함수 (Helper) 개념을 도입하여 로직 처리가 가능합니다. (ex. json)

## Setting
- application.properties
```properties
# handelbars 설정
handlebars.suffix=.hbs
handlebars.cache=false
```

- .html 에서 .hbs 로 바꾸기

## 사용법

- Insert Html
```
{{> include/header}}
```

## 참고 자료
https://github.com/jknack/handlebars.java  
https://handlebarsjs.com/guide/expressions.html#whitespace-control
