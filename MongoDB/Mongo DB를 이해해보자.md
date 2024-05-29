### 몽고DB는 왜 쓰는거지?
- 수평 확장 가능한 분산시스템
	- 물론 RDBMS도 수평확장은 가능하지만, 좀 번거롭다.
- Schema가 존재하지 않음
	- 데이터를 자유로운 형식으로 담을 수 있다
- 완화된 ACID
	- ACID가 불가능하지는 않음 - 분산트랜잭션 지원
### 몽고DB의 데이터 구조
- 몽고DB는 Document기반 데이터베이스
- RDBMS와 구조를 비교해보자면?
	- Table : Collection
	- Row : Document
	- Column : Field
-  Document기반 데이터 베이스는 자유롭게 데이터구조를 만들 수 있다
	- MongoDB의 경우 BSON으로 데이터를 저장해서 배열이나 객체도 넣을 수 있음
- 몽고DB의 _ id필드
	- RDBMS에서 PK와 비슷한 존재
	- 분산된 DB에서 고유 식별자를 생성해야 하기에, ObjectId가 기본 타입인것
	- 만약 직접 지정하지 않으면 ObejctId가 생성되어 들어간다
	- 이 값을 통해 mongos가 해당 ObjectId가 존재하는 Shard에서 데이터 요청 가능
### ACID가 아니라 BASE? BASE란 무엇인가?

몽고DB는 ACID가 아니라 BASE를 기반으로 트랜잭션을 한다.
- Basically Available
	- 언제든지 사용 할 수 있다 (가용성)
- Soft state
	- 외부 개입 없이 정보 변경 될 수 있다
	- 일관 성을 위해 데이터 자동 수정
- Eventually consistant
	- 일시적으로 일관되지 않은 상태가 되더라도 일정 시간후에는 일관적인 상태가 되어야함
### CAP이론

CAP이론이란?
- Consistency, Availability, Partition tolerance는 모두 만족할 수 없다는 것
- Consistency
	- ACID의 Consistency와는 다르다
	- 모든 요청은 최신 데이터 또는 에러를 응답받는다는 것
- Availability
	- 모든 요청은 정상응답을 받는다는 것
	- 최신데이터 아닐 수 있는데 어쨋든 오류 없음
- Partition tolerance
	- 노드간 통신 실패해도 시스템 정상동작하는 것
- CAP이론에 따르면, CP,AP만 존재할 수 있다

이에 따르면 MongoDB는 CP이다.

### PACELC이론

네트워크 파티션이 발생하지 않는 정상적인 상황에서의 트레이드 오프를 설명함

네트워크 파티션이 발생할 때 (P)
- 가용성(A), 일관성(C) 중 하나를 선택해야함

네트워크 파티션이 발생하지 않을 때(E)
- 지연시간(L)과 일관성(C) 중 하나를 선택해야함

이에 따르면 MongoDB는 PC/EC이다
### MongoDB 의 데이터구조 설계는 어떻게 해야할까?
- 임베딩 vs 레퍼런싱
	- 임베딩이란?
		- 관련 데이터를 하나의 Document내에 포함
		- 자주 함께 조회될 때 유리
		- 예를 들어, 블로그 포스트와 그에 대한 댓글
	- 레퍼런싱
		- 관련 데이터를 별도의 컬렉션에 저장하고 문서간의 참조를 통해 연결
- 인덱싱
	- 단일필드 인덱스 : 하나의 필드에 대해
	- 복합 인덱스 : 여러 필드에 대해
	- 고유 인덱스 : 중복X