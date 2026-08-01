<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=180&text=Jungseungwon&fontColor=ffffff&fontSize=45&fontAlignY=35&desc=Backend%20Developer&descAlignY=55&descSize=20" />
</div>

<div align="center">
  <h3>안녕하세요, 백엔드 개발자 정승원입니다 👋</h3>
  <p>데이터를 안정적으로 수집하고 다루는 백엔드에 관심이 많습니다. Spring Boot 기반 외부 API 연동과 데이터 배치 처리를 주로 다룹니다.</p>
  <a href="https://jsh340866.github.io/jsh340866/">
    <img src="https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=googlechrome&logoColor=white">
  </a>
</div>

<br>

<div align="center">
  <img alt="commit snake animation" src="https://raw.githubusercontent.com/jsh340866/jsh340866/output/github-contribution-grid-snake.svg">
</div>

<br>

## 🛠️ Tech Stack

**Backend**
<div align="center">
  <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=Java&logoColor=white">
  <img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=Spring%20Boot&logoColor=white">
  <img src="https://img.shields.io/badge/Spring%20Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white">
  <img src="https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white">
  <img src="https://img.shields.io/badge/JPA%2FHibernate-59666C?style=for-the-badge&logo=Hibernate&logoColor=white">
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white">
  <img src="https://img.shields.io/badge/JUnit5-25A162?style=for-the-badge&logo=junit5&logoColor=white">
</div>

**Frontend**
<div align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white">
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white">
  <img src="https://img.shields.io/badge/Javascript-F7DF1E?style=for-the-badge&logo=Javascript&logoColor=white">
</div>

**Infra & Etc**
<div align="center">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">
  <img src="https://img.shields.io/badge/NGINX-009639?style=for-the-badge&logo=nginx&logoColor=white">
  <img src="https://img.shields.io/badge/Amazon%20EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white">
  <img src="https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white">
  <img src="https://img.shields.io/badge/Let%27s%20Encrypt-003A70?style=for-the-badge&logo=letsencrypt&logoColor=white">
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=Git&logoColor=white">
</div>

**Data Engineering**
<div align="center">
  <img src="https://img.shields.io/badge/Apache%20Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white">
  <img src="https://img.shields.io/badge/PySpark-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/Apache%20Parquet-50ABF1?style=for-the-badge&logo=apacheparquet&logoColor=white">
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white">
  <img src="https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white">
</div>

<br>

## 📌 Projects

### valuepick — 주식/재무 데이터 분석 백엔드

Spring Boot 기반으로 국내 주식·재무 데이터를 수집하고 분석하는 백엔드 프로젝트입니다.

<a href="https://github.com/project-valuepick/valuepick">
  <img src="https://img.shields.io/badge/GitHub%20Repo-181717?style=flat-square&logo=github&logoColor=white">
</a>

- **DB 설계**: MySQL(investdb) 기반 스키마 설계 — 기업·주가·재무·지표·배당·환율·지수 도메인 간 관계 정의, 일별 시세/지표 대량 적재를 고려한 테이블 구성
- **외부 API 연동**: DART(재무제표·공시), 공공데이터포털(주가, XML 파싱), 한국수출입은행(환율), KRX(상장사 정보)를 RestTemplate으로 연동
- **스케줄링**: `@Scheduled` cron으로 평일 새벽 배치 파이프라인 자동화 — 환율 01:00 → 주가 01:20 → 지표 계산 01:50 → TOP100 스코어링 02:00, KRX 지수는 데이터 확정 시각에 맞춰 08:30 분리 실행, 오래된 데이터 정리 02:30
- **비동기 처리**: `@Async`를 활용한 대량 데이터 수집 비동기 처리
- **아키텍처**: JPA Repository + Service 계층 구조
- **핵심 도메인**: Company, StockPrice, StockIndicator, FinancialStatement, DividendInfo, Exchange, Top100, MarketIndex

### Apache-Spark — ValuePick 추천 로직 검증 (개인 프로젝트)

valuepick 서비스가 운영 중인 종목 추천 로직이 실제로 수익을 냈는지, Apache Spark로 2021~2023년 실제 데이터 기준 21,870개 전략을 동시에 백테스트해 검증했습니다.

<a href="https://github.com/jsh340866/Apache-Spark">
  <img src="https://img.shields.io/badge/GitHub%20Repo-181717?style=flat-square&logo=github&logoColor=white">
</a>

- **분산 처리**: PySpark 기반 5단계 파이프라인(원천 수집 → 시세 정제 → 지표 계산 → 백테스트 → MySQL 서빙), 잡 간 데이터 전달은 Parquet
- **그리드 탐색**: 가중치 프리셋 2,187개 × 리밸런싱 주기 2개 × 보유종목수 5개 = 21,870개 전략을 crossJoin+Window로 벡터화해 동시 처리
- **트러블슈팅**: `F.first()`/`F.last()` 순서 비결정성, 실행계획 트리 폭발로 인한 드라이버 OOM, 셔플 파티션 고정값으로 인한 스필 277GB 등 분산 처리 환경에서만 드러나는 문제를 실측으로 규명하고 해결
- **분석 결과**: KOSPI 단독 실행 시 87% 전략에서 성과 개선을 확인했으나, 최고 성과 전략을 추적한 결과 로직의 우수성이 아니라 일회성 회계 이벤트와 실제 주가 급등이 우연히 겹친 사례임을 검증

<br>

## 📜 Certificates

- ✅ 정보처리기사
- 📖 빅데이터분석기사 (취득 예정)
- 📖 SQLD (취득 예정)

<br>

## 📫 Contact

<div align="center">
  <a href="mailto:jsh340866@gmail.com">
    <img src="https://img.shields.io/badge/Gmail-EA4335?style=for-the-badge&logo=Gmail&logoColor=white">
  </a>
  <p>jsh340866@gmail.com</p>
</div>
