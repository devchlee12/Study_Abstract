비즈니스 로직을 처리할 때, 굳이 동기적으로 처리할 필요가 없는 연산들이 존재한다.

이런 연산의 실행시간이 오래걸린다면 불필요하게 응답시간이 늘어나게된다.

따라서 이럴 때는 비동기로 처리할 필요가 있는데, 스프링으로 어떻게 처리할까?
### @Async
- SpringBootApplication에 @EnableAsync 어노테이션 추가
- 메소드에 @Async 명시
- 기본적으로 Thread Excutor로 SimpleAsyncTaskExcutor사용
	- 각 작업마다 새로운 스레드 생성하여 비동기 방식으로 동작
	- 프로퍼티
		- concurrencyLimit : 지정한 수보다 요청 넘어서면 제한
	- 스레드 재사용하지 않는다
- 스레드 풀을 생성해서 동작하게 할 수 있다.
	- AsyncConfigurer를 구현한 설정 클래스에 ThreadPoolTaskExcuter빈을 등록하면 된다
		- 프로퍼티 설정
			- setCorePoolSize(n) : 기본 스레드 수
			- setMaxPoolSize(n) : 최대 스레드 수
			- setQueueCapacity(n) : Queue사이즈
			- 기본 스레드 수 꽉 차면 큐에 넣고, 큐도 꽉 차면 최대 스레드 수까지 생성해서 처리한다
				- 만약에 그거까지 꽉차면? RejectedExecutionException 발생
				- setRejectedExcutionHandler 등록해서 처리 가능
- 유의사항
	- 메소드 접근 지정자 private이면 안됨
	- 클래스 내부에서 Async메소드 호출하면 안됨
	- 생성자로 객체 생성하고 Async메소드 호출하면 안됨
- 작동방식
	- Spring AOP에 의해 프록시 방식으로 작동
		- Async Bean이 등록될 때, Spring이 프록시 객체로 Wrapping해서 등록
		- 따라서 해당 Bean사용할 때 Async Bean을 참조하게 되는 것
		- 그래서 private안되고, 내부에서 호출하면 안되는거임
- CompleteFuture를 통해 비동기 작업의 결과를 처리할 수 있음
### 다른 비동기처리 방식은 없을까?
- DeferredResult, Callable
- WebFlux

