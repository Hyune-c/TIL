# Mutable, Immutable

- Mutable 클래스 : 인스턴스가 생성된 후에 값의 내용이 변할 수 있는 클래스, 주소는 못 바꾼다. ex) String 을 제외한 참조 타입 변수

- Immutable 클래스 : 그 클래스의 인스턴스가 일단 생성된 후에는 인스턴스의 내용이 절대 변하지 않는 특징을 갖는 클래스.






	- 스트링은 이뮤터블
	- 스트링빌더는 뮤터블
	- 람바는 이뮤터블
	- 이뮤터블로 뭔가를 하면 그만큼 객체가 생성되고 gc 가 그것을 처리하기 때문에 속도 이슈가 생깁니다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDg2OTAxNzFdfQ==
-->