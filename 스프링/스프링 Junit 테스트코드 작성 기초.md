### 테스트 코드, 왜 작성하는가?

- 코드 안정성
- 기능 추가/변경 과정에서 side effect 줄임
- 코드 작성 목적이 명확히 표현 → 테스트 통과에 필요한 코드만 넣게되니까

### Junit이란?

- 자바 진영 단위테스트 도구
- 단위테스트란?
    - 모든 함수와 메소드에 대한 각각의 테스트케이스 작서아
- 스프링 2.2부터는 JUnit5사용한다
    - Jupiter,Platform,Vintage모듈로 구성
        - Jupiter
            - TestEngineAPI 구현체
            - Jupiter-API로 작성한 테스트 코드 발견하고 실행
        - Platform
            - Test실행 위한 뼈대
            - TestEngine인터페이스 가지고 있음
            - TestEngine Api + Console Launcher + JUnit4 Based Runnder 등
        - Vintage
            - TestEngineAPI 구현체인데, JUnit3,4구현

### JUnit라이프사이클 어노테이션

- Test
- BeforeEach
- AfterEach
- BeforeAll
- AfterAll

### JUnit 메인 어노테이션

- SpringBootTest
    - 통합테스트 용도로 사용
    - @SpringBootApplication으로 찾아가서 하위 모든 Bean스캔해서 로드
    - 그 후 Test용 ApplicationContext만들어 Bean추가하고 MockBean찾아 교체
- ExtendWith
    - 메인으로 실행될 클래스 지정 가능
    - SpringBootTest는 기본적으로 포함
- WebMvcTest(class명.class)
    - 지정한 클래스만 로드해서 테스트 진행
    - 매개변수 없으면 컨트롤러와 연관된 Bean모두 로드
- @Autowired about Mockbean
    - MockMvc라고 Controller API테스트 하는 객체 있는데 그거 주입받음
    - perform()으로 컨트롤러 동작 확인
- MockBean
    - 테스트할 클래스에서 주입받는 객체에 대해 가짜 객체 생성
    - 해당 객체는 실제 행위 하지 않음
    - given()으로 가짜객체 동작에 대해 정의 가능
- AutoConfigureMockMvc
    - MockMvc의존성 자동 주입
- Import
    - 필요한 클래스를 Configuration으로 사용 가능
- 통합 테스트
    - 전체 비즈니스 로직 동작하는지 확인
    - 모든 빈 스캔하고 로드해서 너무 무거움
- 단위 테스트
    - 모든 기능에 대한 테스트 각각 진행
    - FIRST원칙
        - Fast : 빨라야함
        - Independent : 독립적인 테스트 가능
        - Repeatable : 테스트는 매번 같은 결과 만들어야함
        - Self-Validating : 테스트는 그 자체로 실행해서 결과 확인 가능해야함
        - Timely : 비즈니스 코드가 완성되기 전에 구성하고 테스트가 가능해야함
            - TDD에서만 지킴