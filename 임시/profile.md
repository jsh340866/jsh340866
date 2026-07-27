# 정승원 (Seungwon Jeong)

데이터가 안정적으로 쌓이고, 그 위에서 서비스가 매일 같은 시간에 정확히 돌아가는 것에 관심이 많은 백엔드 개발자입니다.
토목공학을 전공하고 공무원 시험을 준비하다가, 직접 작성한 코드가 의도대로 동작하는 경험에 몰입해 개발자로 진로를 바꿨습니다. 국비 풀스택 개발자 과정(2026.08 수료 예정)을 진행하며 Java/Spring 기반 백엔드를 중심으로 학습하고 있고, SQLD 자격증을 준비 중입니다.

- 정보처리기사 필기 합격 (실기 결과 대기 중)
- 생활신조: "필요한 사람이 되자" — 눈에 띄지 않아도 팀에 필요한 일을 먼저 찾아서 합니다.
- 강점: 낯선 기술도 문서를 직접 파고들고 실제로 호출/실행해 확인하며 빠르게 적응합니다.
- 보완 중인 점: 예상 못한 문제에 조바심을 내는 편이라, 손부터 대지 않고 로그·데이터를 먼저 확인한 뒤 작은 단위로 나눠 검증하는 습관을 들이고 있습니다.

---

## Tech Stack

**Backend**

![Java](https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)
![Hibernate](https://img.shields.io/badge/Hibernate-59666C?style=for-the-badge&logo=hibernate&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![JUnit5](https://img.shields.io/badge/JUnit5-25A162?style=for-the-badge&logo=junit5&logoColor=white)

**Frontend**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=white)

**Infra**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![NGINX](https://img.shields.io/badge/NGINX-009639?style=for-the-badge&logo=nginx&logoColor=white)
![Amazon EC2](https://img.shields.io/badge/Amazon%20EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white)
![Let's Encrypt](https://img.shields.io/badge/Let's%20Encrypt-003A70?style=for-the-badge&logo=letsencrypt&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)

---

## Projects

### [ValuePick](https://www.valuepick.cloud) — 가치투자 지표 기반 종목 스크리닝 서비스

DART 재무제표, 공공데이터포털 주가, KRX 지수, 한국수출입은행 환율을 매일 새벽 자동 수집해 PER·PBR·ROE·Piotroski F-Score 등 투자지표를 계산하고, 멀티팩터 가중 스코어링으로 저평가 우량주 TOP100을 추천하는 서비스입니다. 4인 팀 프로젝트로, 1차 배포 완료 상태입니다.

**담당 역할 — 외부 데이터 수집 파이프라인 & 스코어링 엔진**

- **외부 API 3종 연동**: KRX(상장종목) · DART(전자공시, ZIP/XML) · 한국수출입은행(환율)을 조인해 기업정보 → 재무제표 → 환율 순으로 수집하는 파이프라인 구축
- **API 호출 최적화 (2,700회 → 1회)**: 종목별로 개별 호출하던 주가 수집 로직을, 문서를 재확인해 필수 파라미터가 아니던 종목코드 필터를 제거하고 날짜 기준 전 종목 일괄 조회로 전환. 일일 호출 한도 초과 문제를 근본적으로 해결
- **표준 계정 코드 기반 재무 매칭**: "영업이익"/"영업이익(손실)"처럼 회사마다 다른 계정명(`account_nm`) 표기 때문에 재무 데이터가 0으로 누락되던 문제를, DART가 제공하는 표준 계정 코드(`account_id`)로 매칭 기준을 바꿔 해결
- **법령 기반 종목 필터링**: 리츠/스팩 종목을 걸러낼 때 `contains` 매칭으로 인한 오탐(예: "메리츠금융지주")을, 관련 법령(부동산투자회사법·자본시장법)의 상호 표기 규칙을 근거로 `endsWith`/`contains`를 구분 적용해 화이트리스트 없이 해결
- **Cascade 삭제 설계**: 상장폐지 종목 처리 시 6개 자식 테이블을 `CascadeType.ALL` + `orphanRemoval`로 자동 정리
- **비동기 처리**: 2,500개 이상 종목을 `@Async` + 전용 스레드풀(`dartExecutor`)로 병렬 수집, 스케줄러 간 순서 보장을 위한 cron 스태거링 적용

**기술 스택**: Spring Boot, Spring Data JPA, MySQL, RestTemplate, DOM XML Parser, ZipInputStream, `@Async`/`@Scheduled`

---

## Contact

- GitHub: [@jsh340866](https://github.com/jsh340866)
- Email: jsh340866@gmail.com
