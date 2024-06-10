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
	- 
- Queue

### Exchange Type
- Direct
- Topic
- Headers
- Fanout