```text
첨부된 코드는 일부 수정되고, 어노테이션이 생략되기도 하였습니다.
```

뽐뿌라는건 갑자기 온다는 걸 본 적이 있다.

<https://woowabros.github.io/experience/2019/02/28/pilot-project-settle.html>

여느때처럼 재미있는 글을 찾다가 예전에 비슷하게 했던 실수를 비슷한 방법으로 고치는 글을 보는데..  
Querydsl 이 그냥 갑자기 눈에 띄었고, 그냥 갑자기 하고 싶어졌다.

그렇게 야밤의 삽질을 적어봅니다.

## 자아성찰

### 현재의 구성

- SpringBoot 2.x 모놀리스 서비스
- Postgresql 로 구성된 2개의 DB
- mybatis 80%, JpaRepository 20%

### 내 실력

- 튜토리얼 해봄
- mybatis 와 JpaRepository 의 기계적인 사용은 할 수 있다. (= 깊은 이해가 없다.)

### 목표

- 기존의 것에 영향이 없게 & 유지보수 좀 쉽게 해보자.
  - 코드 어시스트 좀.. xml 싫어요..
  
## 1. 정보 수집

무난하게 김영한 님의 JPA 서적으로 시작. 튜토리얼 기억을 더듬어 EntityManager, EntityManagerFactory 를 넘어 JPAQuery 을 보는데 생각했던 것 만큼 이쁘지 않아서 갸우뚱하는 중에

<https://jojoldu.tistory.com/372>

역시 모든 것이 다 있는 jojoldu 님.. JPAQueryFactory 가 내가 딱 생각하는 형태였고, 해보기로 했다.

(Querydsl, Q type class 설정은 생략!)

## 2. 기존 소스 분석

```java
@Configuration
@EnableTransactionManagement
public class DataSourceConfig {

  private final DataSource dataSource;

  public DataSourceConfig(@Qualifier("dataSource") DataSource dataSource) {
    this.dataSource = dataSource;
  }

  @Primary
  @Bean(name = "entityManagerFactory")
  public LocalContainerEntityManagerFactoryBean entityMangerFactory(EntityManagerFactoryBuilder builder) {
    return builder
        .dataSource(dataSource)
        .packages("com.AAA.repository")
        .persistenceUnit("AAA")
        .build();
  }

  @Bean("transactionManager")
  @Qualifier("transactionManager")
  public PlatformTransactionManager transactionManager(EntityManagerFactoryBuilder builder) {
    return new JpaTransactionManager(Objects.requireNonNull(entityMangerFactory(builder).getObject()));
  }
}
```

튜토리얼은 그냥 복붙으로 따라하면 됬는데, 여기는 회사.  
당연히 레거시 코드를 이해하고 영향이 없도록 고쳐야 했다.

하지만 흔히 보던 EntityManager 나 Factory 는 없고, 못보던 객체들만 있어서 살짝 당황했는데 잘 읽어보니 힌트가 있었다. 객체 이름에 Factory 가 있고, Bean 으로 반환되는 것을 볼 때 저것을 잘 활용하면 되지 않을까 라는 생각으로 검색을 해봤다.

<https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa>

## 3. 구현 (1차)

```java
@RequiredArgsConstructor
@Repository
public class NoticeRepositorySupport {

  private final LocalContainerEntityManagerFactoryBean entityManagerFactory;

  public List<NoticeEntity> findAllByQd() {
    EntityManager em = entityManagerFactory.getObject().createEntityManager();
    JPAQuery query = new JPAQuery(em);
    QNoticeEntity qNotice = new QNoticeEntity("qn");

    return query.from(qNotice).fetch();
  }
}

@Test
public void qd() throws Exception {
    // when
    List<NoticeEntity> noticeEntityList = noticeRepositorySupport.findAllByQd();

    // then
    assertThat(noticeEntityList.size()).isGreaterThanOrEqualTo(0);
}
```

일단은 책에 있는 형태로 구현하는 게 더 쉬울 것 같아서 `LocalContainerEntityManagerFactoryBean` 를 가져오고 JPAQuery 의 기본형을 만들어봤다.  

아직 맘에 드는 형태는 아니지만 일단 성공했다는 것에 의의를 두고 테스트까지 만들어봤다.

## 4. 구현 (2차)

```java
@RequiredArgsConstructor
@Repository
public class NoticeRepositorySupport {

  private final LocalContainerEntityManagerFactoryBean entityManagerFactory;

  public List<NoticeEntity> findAllByQd() {
    EntityManager em = entityManagerFactory.getObject().createEntityManager();
    JPAQueryFactory queryFactory = new JPAQueryFactory(em);

    return queryFactory
        .selectFrom(NoticeEntity)
        .where(NoticeEntity.noticeId.goe(5))
        .fetch();
  }
}
```

약간의 수정으로 코드 어시스트, join , where 절을 통한 동적 쿼리도 되는 JPAQueryFactory 를 만들 수 있었다! 무엇보다도 기존의 로직에 영향을 주지 않으면서 만들었다는게 좋았다!

하지만.....

## 5. (급) 걱정

여기까지 만들고나니 걱정되는 것이 있었다.

- DB 가 2개인데 서로 연결될까?
- 되는건 둘째치고 transaction 이 보장될까?  
- DataSourceConfig 에 있는 `PlatformTransactionManager` 로 뭔가를 해야될 거 같은데,  
테스트는 어떻게 해봐야되지.....
- 뜬금포로 이걸 써도 될까?

그래서 시니어님에게 질문을 했고 결론은 기각 됬다 ㅠㅠ

- 이미 2종류의 DB 접근법이 있는데, 러닝 커브가 필요한 DB 접근법을 갑자기 도입하는건 힘들다.
- 2개 DB 에 대한 이해, 트랜잭션 고려 등이 부족하다.  
- 내년 초에 예정된 MSA 분리 때 적용을 하는 것이 어떤가?

특히 2번째 의견이 치명타였다.  
고작 몇 시간한 정도로 조회가 돌아가는 수준은 만들었지만 그 이상은 검증할 방법조차 생각나지 않으니..

## 회고

사실 더 진행해도 된다면 생각해 둔 것은 더 많았다. 하지만 시니어님의 피드백을 반박할 근거가 없었기에..  
오랜만에 동기부여가 되는 작업을 해서 좋았지만, 동시에 아직도 1인분은 멀었구나 하는 걸 느끼게 되었다.

라는 슬픔으로 뜬금없이 글을 작성했습니다.  
내년에는 `Querydsl 전환 완료` 로 글을 쓰고 싶다!!!!!
