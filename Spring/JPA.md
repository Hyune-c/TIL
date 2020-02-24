# Data JPA (Java Persistence API)
자바 플랫폼 SE와 자바 플랫폼 EE를 사용하는 응용프로그램에서 관계형 데이터베이스의 관리를 표현하는 자바 API로 기존 EJB에서 제공되던 엔터티 빈(Entity Bean)을 대체하는 기술입니다.

## 데이터베이스 스키마 자동 생성

application.properties 에 설정

> spring.jpa.hibernate.ddl-auto=`option`

| option      | desc                                                         | 용도                                                |
| ----------- | ------------------------------------------------------------ | --------------------------------------------------- |
| create      | 기존 테이블 삭제 후 다시 생성 (DROP + CREATE)                | 개발 초기 단계<br />로컬 개발 서버                  |
| create-drop | create와 같으나 종료 시점에 테이블 DROP (테스트에서 사용하면 도움됨) | 개발 초기 단계<br />로컬 개발 서버                  |
| update      | 변경 분만 반영 (운영 DB에서는 사용하면 안됨) `alter table ~` | 개발 초기 단계<br />로컬 개발 서버<br />테스트 서버 |
| validate    | 엔티티와 테이블이 정상 매핑되었는지만 확인                   | 테스트 서버<br />스테이징<br />운영 서버            |
| none        | 아무 속성도 사용하지 않음                                    | 스테이징<br />운영 서버                             |


## 객체와 테이블 매핑
### @Entity
- JPA가 관리하며 테이블과 매핑할 클래스는 반드시 @Entity 를 붙여야 합니다.
- 매개변수가 없는 public 또는 protected 생성자가 반드시 필요합니다. 
- JPA spec 으로 규정되어 있습니다.
- final, enum, interface, inner 클래스는 엔티티로 사용할 수 없습니다.
- DB에 저장하고 싶은 필드에는 final 을 사용할 수 없습니다.

###### @Entity(name = "Member")

기본값은 클래스 이름이며 JPA에서 사용할 엔티티 이름을 지정합니다.  
가급적 기본값을 사용하도록 합니다.

### @Table
@Table은 엔티티와 매핑할 테이블을 지정합니다.

###### @Table(name = "MBR")
기본값은 엔티티의 이름을 사용하며 매핑할 테이블 이름을 지정합니다.
###### catalog
데이터베이스 catalog 매핑
###### schema
데이터베이스 schema 매핑
###### uniqueConstraints(DDL)
DDL 생성 시에 유니크 제약 조건 생성


### @id

@Entity의 고유한 아이디를 식별하기 위해 사용하며 자동 생성이 가능합니다.

```java
@Entity
public class Question {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long questionId;
}
```

| 생성 방식 | DESC                                                         |
| --------- | ------------------------------------------------------------ |
| IDENTITY  | 기본 키 생성을 데이터베이스에 위임                           |
| SEQUENCE  | DB 시퀀스를 사용해 기본 키 할당                              |
| TABLE     | 키 생성 테이블 사용                                          |
| AUTO      | DB에 따라 위 3가지 옵션(IDENTITY, SEQUENCE, TABLE) 중 하나를 자동으로 선택 |

###  @Column

| property         | desc                                                         | desc2 |
| ---------------- | ------------------------------------------------------------ | ----- |
| name             | 컬럼 명                                                      |       |
| insertable       | false : DB 에 저장되지 않습니다. (읽기 전용)                 |       |
| updatable        | false : DB 에 수정되지 않습니다.                             |       |
| nullable         | false : not null 제약 조건이 설정됩니다.                     | DDL   |
| unique           | unique 제약 조건을 설정합니다.<br />2개 이상을 설정하고 싶은 경우 @Table.uniqueConstraints 를 사용합니다. | DDL   |
| columnDefinition | 직접 컬럼 정보를 입력할 수 있습니다.                         | DDL   |
| length           | 문자 길이 제약 조건으로 String 만 해당합니다.                |       |
| precision, scale | BigDecimal, BigInteger 에서 사용됩니다                       | DDL   |

```java
@Column(columnDefinition = "varchar(100) default 'EMPTY'")
```

### @Enumerated

자바의 enum 타입을 테이블과 매핑합니다.

- EnumType.ORDINAL : enum의 순서를 DB에 저장
- EnumType.STRING : enum 이름 값 자체를 DB에 저장

### @Temporal

날짜 타입을 매핑할 때 사용합니다.

### @Lob

DB에서 varchar를 넘어서는 큰 내용을 넣고 싶은 경우에 사용합니다.

CLOB : String, char[], java.sql.CLOB  
BLOB : byte[], java.sql.BLOB

### @Transient

필드 중 테이블 칼럼과 매핑하고 싶지 않은 경우 사용합니다.


## JPA 활용

### 기본 CRUD 구현 
> CRUD : 기본적인 데이터 처리 기능인 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 를 뜻합니다.
>
```java
public interface CrudRepository<T, ID extends Serializable>
    extends Repository<T, ID> {
    <S extends T> S save(S entity); 
    T findOne(ID primaryKey);       
    Iterable<T> findAll();          
    Long count();                   
    void delete(T entity);          
    boolean exists(ID primaryKey);  
}
```

### 페이징과 정렬(sorting)
CrudRepository를 extends하는 PagingAndSortingRepository 활용해 구현 가능합니다.
```java
public interface 
  PagingAndSortingRepository<T, ID extends Serializable>
  extends CrudRepository<T, ID> {
      Iterable<T> findAll(Sort sort);
      Page<T> findAll(Pageable pageable);
  }
}
```
```java
@Autowired
PagingAndSortingRepository<User, Long> repository;

Page<User> users = repository.findAll(new PageRequest(1, 20));
```

### 그외 Repository에서 제공하지 않는 다양한 쿼리 사용방법
| Keyword  | Sample                       | JPQL snippet                                 |
| -------- | ---------------------------- | -------------------------------------------- |
| And      | findByLastnameAndFirstname   | … where x.lastname = ?1 and x.firstname = ?2 |
| Between  | findByStartDateBetween       | … where x.startDate between ?1 and ?2        |
| LessThan | findByAgeLessThan            | … where x.age < ?1                           |
| OrderBy  | findByAgeOrderByLastnameDesc | … where x.age = ?1 order by x.lastname des   |       

## 참고자료
https://gmlwjd9405.github.io/2019/08/11/entity-mapping.html  
https://ict-nroo.tistory.com/113  
http://wonwoo.ml/index.php/post/717
