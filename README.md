# yogiyot
- 항해 99에서 진행한 첫번째 프로젝트
- 백엔드 : 2명
- 프로젝트 기간: 2024.01.12(금) ~ 2024.01.25(목) / 2주

<br>

### 프로젝트 개요
- 음식 주문 서비스 api 개발
- 회원이 사장님과 손님으로 나눠짐
  - 사장님으로 회원가입 할 경우 음식점 등록, 음식점 정보 수정, 삭제, 음식점에 메뉴 등록, 수정, 삭제 가능
  - 손님으로 회원가입 할 경우 음식점 조회, 검색, 주문, 주문내역조회 가능

### 역할
---
- 음식점 등록 수정 삭제
- 회원가입 시 이메일인증(nodemailer)
- 브랜드 검색 (elasticsearch)
- 브랜드 목록 조회 (redis)

<br>

### 기술 스택
- Node.js, Prisma, Redis, AWS EC2, nodemailer, AWS SES

<br>

###프로젝트 진행 단계
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
       [![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8842ffa4-f952-449b-ba05-29bb5cb3e6d7/7344e4b5-ba38-4890-8ee7-42ab9bfe7825/Untitled.png)]()
     - reids 적용 후
       ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8842ffa4-f952-449b-ba05-29bb5cb3e6d7/791b271d-a087-4136-9d3a-097a2650c765/Untitled.png)
     - jmeter로 부하테스트 해본 결과
       - 1000명이 동시에 50초 동안 2번씩 반복 요청 했을 때
         ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8842ffa4-f952-449b-ba05-29bb5cb3e6d7/44df0613-e22d-40c5-bc0c-850bb5bbbfa4/Untitled.png)
         - 캐쉬가 있는 상태
           ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8842ffa4-f952-449b-ba05-29bb5cb3e6d7/6a544b82-8db1-400c-a758-800bca4a89b8/Untitled.png)

<br>

### 📌 주요 기능
---
[- ](https://pacific-hedge-455.notion.site/8e1680955e834bb2939e91ff92d686b5?v=cb919b063ea24a62a048d5f9c467ee2f)https://pacific-hedge-455.notion.site/8e1680955e834bb2939e91ff92d686b5?v=cb919b063ea24a62a048d5f9c467ee2f
