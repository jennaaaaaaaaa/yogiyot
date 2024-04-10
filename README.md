# yogiyot
- 항해 99에서 진행한 첫번째 프로젝트
- 백엔드 : 2명
- 프로젝트 기간: 2024.01 ~ 2024.01 / 2주
- 팀노션: [팀노션](https://www.notion.so/yogiyot-9defd1d7b68048d7aa26fbdd912e66bb)
<br>

### 프로젝트 개요
- 음식 주문 서비스 api 개발
- 회원이 사장님과 손님으로 나눠짐
  - 사장님으로 회원가입 할 경우 음식점 등록, 음식점 정보 수정, 삭제, 음식점에 메뉴 등록, 수정, 삭제 가능
  - 손님으로 회원가입 할 경우 음식점 조회, 검색, 주문, 주문내역조회 가능

### 역할
- 음식점 등록 수정 삭제
- 회원가입 시 이메일인증(nodemailer)
- 브랜드 검색 (elasticsearch)
- 브랜드 목록 조회 (redis)

<br>

### 기술 스택
- Node.js, Prisma, Redis, AWS EC2, nodemailer, AWS SES

<br>

### 프로젝트 진행 단계
1. 회원가입, 로그인 및 음식점 등록, 수정, 삭제, 메뉴 등록, 수정, 삭제, 음식 주문, 조회 api 구축
2. api에 접근 권한 설정
4. 회원가입 시 이메일 인증 기능 구현
5. redis로 음식점 목록 조회 기능 구현


### 구현 내용
1. 음식점 정보 등록 , 수정, 삭제, 상세조회, 목록조회 기능
   - userType에 따라 사장님으로 회원가입한 계정만 접근 가능하도록 구현
   - 삭제는 softDelete로 구현
   - 사업장 등록 시 등록하려는 주소로 등록된 사업장 여부 확인 후 없다면 등록하도록 구현
  

2. 이메일 인증 기능
   - nodemailer와 aws ses 적용으로 회원가입 시 이메일 인증을 하도록 구현
     -  ssl인증서와 aws ses 중 aws ses를 적용한 이유
       -  aws ses는 대량의 이메일을 서버 부담없이 처리
       -  사용한 만큼만 나가는 비용으로 비용 부담이 적음
       -  확장성을 제공하기에 서비스가 커진다는 가정에서 aws ses를 적용
         
3. 음식점 목록 조회에 redis 적용
   - 서비스의 확장성을 고려하여 redis를 적용
     - redis 적용 전
       ![redis 적용 전](https://github.com/jennaaaaaaaaa/yogiyot/assets/111362623/cce2d15c-b78a-47ae-87ca-a0e06ae68ebe)
       
     - reids 적용 후
       
       ![redis 적용 후](https://github.com/jennaaaaaaaaa/yogiyot/assets/111362623/e403df4b-138a-4b2d-9d76-494f41f547ed)

     - jmeter로 부하테스트 해본 결과
       - 1000명이 동시에 50초 동안 2번씩 반복 요청 했을 때
         
          <img width="145" alt="부하테스트 시나리오" src="https://github.com/jennaaaaaaaaa/yogiyot/assets/111362623/9d8fe78e-73b8-4a3d-b52f-9b8c1679b787">

         - redis 적용 상태( 평균 걸린 시간 : 2ms)
           <img width="875" alt="redis 적용 후 jmeter" src="https://github.com/jennaaaaaaaaa/yogiyot/assets/111362623/0f22c8ee-dd4d-472c-9c9f-6a0a706ebe85">
         - redis 적용 전 상태( 평균 걸린 시간: 5022ms)
            <img width="880" alt="redis 적용 전 jmeter" src="https://github.com/jennaaaaaaaaa/yogiyot/assets/111362623/3f6c7d69-d4c3-4bc4-bb8d-2648057ee0ff">

<br>

### 트러블슈팅
- 문제: 사업장 새로 추가 시 redis가 업데이트 되지 않음
- 시도: ttl 설정으로 유효한 시간 마다 데이터를 사동으로 삭제 해주는 기능을 적용하려 했지만 잘되지 않음
- 해결 방법: 시간 부족으로 사업장이 추가될 때 캐쉬가 한번 지워지도록 구현
