### ELB란?
- 들어오는 애플리케이션 트래픽을 여러 대상(EC2,컨테이너 Ip주소 등)에 자동으로 분산
- 단일 가용영역 뿐만 아니라 여러 가용영역에서 부하 처리 가능
- Health Check 기능
	- 직접 트래픽 발생시켜서 Instance살아있는지 체크
- AutoScaling과 연동 가능
- 지속적으로 IP주소 바뀌고, IP고정이 불가능
	- 항상 도메인 기반으로 사용해야함

### ELB의 종류
- Application Load Balancer
	- 똑똑한 녀석
	- 트래픽을 모니터링해서 라우팅 가능
- Network Load Balancer
	- 빠른 녀석
	- TCP기반 빠른 트래픽 분산
	- Elastic IP할당 가능
- Classic Load Balancer
	- 옛날 녀석
	- 예전에나 사용되던 타입으로 현재는 잘 사용안함
- Gatway Load Balancer
	- 먼저 트래픽 체크하는 녀석
	- 트래픽이 EC2로 가기전에 뭔가 처리해줄 때 사용\
		- 방화벽,캐싱,트래픽분석,인증,로깅 등

### 대상그룹이란?
- ALB가 라우팅할 대상의 집합
- 구성
	- 3+1가지 종류
		- Instance
		- Ip - private
		- Lambda
		- ALB
	- 프로토콜
		- HTTP
		- HTTPS
			- ALB로 구현하면 HTTP 구현이 굉장히 편하다
		- gRPC
	- 기타설정
		- 트래픽 분산 알고리즘, 고정 세션 등

### ELB사용방법
- 대상그룹으로 인스턴스들을 추가
- 로드밸런서 생성
- AutoScaling서비스와 연동 가능
	- 대상그룹 등록
	- ELB모니터링 활성화
