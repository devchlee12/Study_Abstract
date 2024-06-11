### RabbitMQ란 무엇인가
- AMQP를 구현하여 메시지 생성자와 소비자 사이에서 메시지 중계해주는 메시지 브로커
-  비동기 메시지를 사용하는 응용 프로그램들 사이에서 데이터 송수신을 도와줌

### MessageQueue는 왜 사용하는걸까?
- 비동기
	- 메시지 저장, 전송에 대해 동기화 안하고 Queue에 넣었다가 나중에 처리가능해서 병목현상 방지
- 낮은 결합도
	- Producer와 Consumer가 독립적으로 행동하므로 결합도 낮아짐
- 확장성
	- 다수의 프로세스가 메시지큐를 통해 메시지 보낼 수 있으므로 확장성 및 분산처리에 장점을 가짐
- 탄력성
	- 메시지 받아서 처리하는 서비스가 다운되도 메시지큐는 동작하고 있으므로 Queue에있는 메시지 다시 처리 가능
- 보장성
	- 결국 Customer 서비스에 전달되는 것을 보장

### RabbitMQ의 구조
- Producer
	- 메시지 생성하고 발송하는 주체
	- Queue에 메시지를 직접 보내는게 아니라 Exchange에 Publish하는것
- Consumer
	- 메시지를 받아서 처리하는 주체
- Exchange
	- Producer로부터 전달받은 메시지를 어떤 Queue에 발송할지 결정하는 객체
	- 4가지 타입과 Binding규칙에 따라 적절한 Queue로 메시지 전달
- Binding
	- Exchange와 Queue를 연결하는 관계
- Queue
	- RabbitMQ안에서 메시지를 일시적으로 저장하는 장소

### Exchange Type
- Direct Exchange
	- 메시지에 포함된 routing key를 기반으로 Queue에 메시지 전달
	- 여러개의 큐에 하나의 라우팅키를 지정하거나, 하나의 큐에 여러개의 라우팅 키를 지정하는 것도 가능
- Topic Exchange
	- 메시지에 포함된 routing key의 패턴을 이용해서 메시지를 라우팅
	- 키 전체가 일치하거나 일부패턴과 일치하는 모든 Queue로 메시지 전달
	- binding key
		- . 으로 구분되는 단어 조합
		- * : 정확히 1단어 대체
		- #: 0~N개의 단어 대체
- Headers Exchange
	- 메시지 라우팅을 위해 header를 사용하는 방식
	- routing key 속성은 무시되고 header속성의 값이 바인딩 시 지정된 값과 같은 경우에 일치하는것으로 간주
	- x-match
		- any : 헤더 테이블 값 중 하나가 연결된 값 중 하나와 일치하면 메시지 전달
		- all : 헤더 테이블의 값과 모든 값이 일치해야 메시지 전달
- Fanout Exchange
	- Exchange에 등록된 모든 Queue에 동일한 메시지 전달하는 브로드 캐스팅 라우팅 방식
### 하나의 Queue에 여러개의 Consumer가 붙어있다면 어떻게 될까?
- Round Robin으로 처리한다
	- Consumer들한테 번갈아가면서 메시지 전달
	- 그런데 이렇게하면 특정 Consumer에게 메시지가 누적되는 경우가 발생 가능
	- 그러면 어떻게 해결할까?
		- Prefetch
			- Consumer의 메모리에 쌓아둘 수 있는 최대 메시지의 양
			- 1로 설정하면 Consumer가 메시지를 처리하기 전에는 새로운 메시지를 받지 않기 때문에 작업 분산 가능 