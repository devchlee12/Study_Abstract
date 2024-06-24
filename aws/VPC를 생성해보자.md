### VPC 관련 몇가지 알아둘점
- 커스텀 VPC 생성 시 자동으로 만들어지는 리소스
	- 라우팅 테이블, 기본 NACL, 기본 보안그룹
	- 서브넷 생성 시 모두 기본 라우팅 테이블로 자동 연동
- 서브넷 생성 시 AWS는 총 5개의 IP를 미리 점유함
- VPC에는 단 하나의 IGW만 생성가능
	- IGW생성 후 직접 VPC에 연동 필요
- 보안 그룹은 VPC단위
- 서브넷은 가용영역 단위

### VPC 생성
- 직접 커스팀 VPC 생성
- 서브넷 생성
- 각 서브넷에 각각 Routing Table 연동
- Public 서브넷에 인터넷 경로 구성 : IGW
- Public 서브넷에 EC2 프로비전
- Private 서브넷에 EC2 프로비전
- Bastion Host로 Private 서브넷에 접속하고 싶다면 Public subnet에서 ssh로 접속
- Private 서브넷에서 인터넷에 접속하고 싶다면 NatGateway 생성