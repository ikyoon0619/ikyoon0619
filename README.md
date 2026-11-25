## 윤인규 | Java/Spring 백엔드 개발자

사내 업무 시스템과 외부 API 연동 서비스를 Spring Boot로 만들고, AWS EC2에 Docker로 배포해 운영하고 있습니다.
동시성, JPA 성능, 트랜잭션 경계처럼 실제 서비스에서 문제가 되는 부분을 직접 재현하고 수치로 확인하며 개선합니다.

| | |
|---|---|
| 총 경력 | 5년 3개월 (제조 대기업 영업 CRM 개발, 인프라) |
| 주력 기술 | Java 17, Spring Boot 3, Spring Data JPA, QueryDSL, MySQL, Docker, AWS EC2 |
| 포트폴리오 | https://portfolio-site-ikyoon.netlify.app |
| 연락처 | ikyoon0619@gmail.com |

## 프로젝트

### 1. 구매요청·전자결재 시스템

[코드](https://github.com/ikyoon0619/purchase-approval) · [데모](http://54.180.77.43) (체험 계정 `dev1` / `devlead` / `admin`, 비밀번호 `pass1234`)

구매요청서를 올리면 팀장, 본부장, (500만 원 이상이면) 구매팀장 순서로 결재하고, 승인 후 발주·입고·재고까지 이어지는 사내 업무 시스템입니다.

- 같은 문서를 동시에 결재하면 한 건만 반영(낙관적 락), 동시 입고 시 재고 유실은 `SELECT … FOR UPDATE`로 해결
- N+1 문제를 fetch join으로 개선(쿼리 11회 → 1회), 컬렉션 페이징은 batch fetch size로 처리
- 외부 API(국세청 사업자 상태)는 트랜잭션 밖에서 호출, 감사 로그는 AOP와 `REQUIRES_NEW`로 기록
- Spring Batch 야간 집계, Flyway 마이그레이션, GitHub Actions CI, 테스트 118개, AWS EC2 Docker 배포

`Java 17` `Spring Boot 3` `JPA` `QueryDSL` `Spring Security` `Spring Batch` `Thymeleaf` `MySQL 8` `Docker` `AWS EC2`

### 2. AI 약국 찾기

[코드](https://github.com/ikyoon0619/pharmacy-backend) · [데모](https://pharmacy-ikyoon.onrender.com)

"강남역 근처 일요일 밤 10시에 여는 약국"처럼 문장으로 물으면 실제 약국 데이터로 답하는 Spring Boot 서비스입니다.

- 공공데이터 약국 25,432곳의 영업시간을 매일 수집하고, 자정을 넘는 영업까지 계산
- 카카오 로컬 API와 Claude API(Anthropic Java SDK)를 연동해 도구 호출 흐름을 직접 구현
- 진행 상황과 답변을 SSE로 실시간 전송, 테스트 74개(JUnit 5, Mockito), Docker로 배포

`Java 17` `Spring Boot 3` `JPA` `SSE` `Kakao API` `Claude API` `Docker`

### 3. AI 영화 추천·검색 앱

[코드](https://github.com/ikyoon0619/vue3-movie-app) · [데모](https://superb-croissant-161b98.netlify.app/#/recommend)

기분이나 상황을 적으면 영화를 추천하고, OMDb API로 실제 존재하는 영화인지 확인한 뒤 보여 주는 Vue 3 앱입니다.

- API 키는 Netlify Function 뒤에 두어 브라우저 코드에 노출되지 않도록 처리
- 하루 사용량 제한(전체·사용자별), 외부 API를 대체한 Vitest 테스트 22개

`Vue 3` `Vuex` `Netlify Functions` `Vitest`

### 4. AI 고객상담 에이전트

[코드](https://github.com/ikyoon0619/ai-cs-agent) · [데모](https://ai-cs-agent.onrender.com)

제품 카탈로그 문서를 근거로 고객 질문에 답하고, 재고 조회·시승 예약 같은 기능을 호출하는 상담 서비스입니다.

- 키워드 검색과 벡터 검색을 함께 쓰는 하이브리드 검색으로 검색 정확도(MRR) 0.928 → 0.957
- 예약처럼 실제 처리가 일어나는 기능은 상담원 승인 후 실행
- FastAPI, PostgreSQL(pgvector), Render 배포

`Python` `FastAPI` `PostgreSQL` `LangChain` `LangGraph` `Claude API`
