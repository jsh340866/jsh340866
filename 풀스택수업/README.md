# 📚 풀스택 개발자 학습 기록 (2026-02 ~ 2026-07)

2026년 2월 말부터 7월까지 진행한 풀스택 개발자 과정의 학습 기록입니다. 요구사항 분석/화면설계 → 프론트엔드 기초(HTML/CSS/JS) → 데이터베이스(MySQL) → Java → 웹 백엔드(JSP/Servlet → Spring Boot) → 인증/외부 API 연동 → React → Docker/AWS 배포 → Python/데이터분석·머신러닝(회귀/분류/군집화/이상치탐지) → FastAPI 서버 개발 → PySpark 분산처리 순으로 학습 범위를 확장했습니다.

## 목차

| 월 | 기간 | 핵심 주제 |
|---|---|---|
| [🧭 2월](#-2월-학습-내용-오리엔테이션--요구사항분석) | 02-25 ~ 02-27 | 프로젝트 요구사항 분석, 화면설계, Git 기초 |
| [🌸 3월](#-3월-학습-내용-프론트엔드-기초) | 03-03 ~ 03-31 | Git/GitHub, HTML/CSS, JavaScript, 프론트 라이브러리(Swiper·GSAP·Leaflet 등) |
| [🌱 4월](#-4월-학습-내용-데이터베이스--java-입문) | 04-01 ~ 04-29 | MySQL(DDL/DML/정규화/JOIN), Java 기초 문법, OOP 입문 |
| [🚀 5월](#-5월-학습-내용-java-심화--jspservlet--spring-boot-입문) | 05-04 ~ 05-29 | Java 심화(컬렉션/스트림/네트워크), JSP/Servlet, Spring Boot 입문 |
| [⚙️ 6월](#️-6월-학습-내용-spring-boot-고급--외부-api--보안--react) | 06-01 ~ 06-30 | JPA/MyBatis, 외부 API(OAuth2/결제), Spring Security/JWT, React |
| [☁️ 7월](#️-7월-학습-내용-배포인프라--pythonml-입문) | 07-01 ~ 07-28 | React-Spring 연동, Docker/AWS/Jenkins 배포, Python 머신러닝(회귀/분류/군집화/이상치탐지), FastAPI, PySpark |

---

## 🧭 2월 학습 내용 (오리엔테이션 · 요구사항분석)

### 주요 학습 주제
- 개발 환경 세팅(VSCode, draw.io, Figma)
- 프로젝트(도서관리 시스템) 요구사항 분석 및 화면설계
- 유스케이스 다이어그램 / 플로우차트 작성
- Git 기초 명령어 및 SourceTree

### 날짜별 요약

| 날짜 | 핵심 학습 주제 |
|---|---|
| 2026-02-25 | 도서관리 시스템 요구사항 정의 — 회원/비회원/사서/관리자 액터별 CRUD 권한 설계 |
| 2026-02-26 | 유스케이스 다이어그램, 회원가입 유스케이스 명세서, 로그인·회원가입 플로우차트 |
| 2026-02-27 | 장바구니·결제(카드 인증) 플로우차트 확장, Figma 프로토타입·스타일가이드, Git 기초(init/add/commit/branch/merge), SourceTree |

### 핵심 역량
- 요구사항 분석 및 화면설계 도구(draw.io, Figma) 활용 능력
- Git 기초 버전관리 이해

---

## 🌸 3월 학습 내용 (프론트엔드 기초)

### 주요 학습 주제
- Git/GitHub 협업(Organization, Branch Rule, Issue/Milestone, rebase, conflict 해결)
- HTML 기본 구조 및 Form/Table/Bootstrap5
- CSS Box Model, Position, Flexbox, Grid, 애니메이션, 반응형 단위
- JavaScript 핵심 문법(변수/함수/배열/DOM/이벤트/비동기)
- 프론트엔드 라이브러리 실습(Swiper, Lodash, ScrollMagic, GSAP, Chart.js, Leaflet)

<details>
<summary>날짜별 요약 (20일)</summary>

| 날짜 | 핵심 학습 주제 |
|---|---|
| 2026-03-03 | Git 기본(add/commit --amend/reflog/reset 3종/branch/merge --no-ff), GitHub Organization·Repository·Issue/Milestone 협업 구조 |
| 2026-03-04 | GitHub Projects 이슈 관리, SourceTree 원격 연동(reset 3종, conflict 해결, rebase 후 merge --no-ff) |
| 2026-03-05 | 웹 개념(Client/Server/IP/Port/HTTP), VSCode 세팅, HTML 기본 구조(h1~h6, div/span, ul/ol/li) |
| 2026-03-06 | HTML 엔티티, Emmet 문법, table(rowspan/colspan), a/img/video 태그, form 회원가입 예제 |
| 2026-03-07 | form action/method(GET/POST), input 타입, Bootstrap5 grid; data-* 속성, CSS 선택자 우선순위, 반응형 단위(px/%/vw) |
| 2026-03-10 | CSS 단위(px/em/rem/%/vw/clamp), margin·padding 단축값, box-sizing, overflow, 자식·자손 선택자, ::before/::after |
| 2026-03-11 | position(relative/absolute/fixed/sticky), GNB 드롭다운, z-index, Flexbox(justify-content/align-items/wrap) |
| 2026-03-12 | CSS Grid(template-columns/areas), transition/transform, @keyframes 애니메이션; 미디어쿼리, JS 입문(console/typeof) |
| 2026-03-16 | 템플릿 리터럴, let/const, Object/this, querySelector, 배열 함수(push/forEach/sort/filter/reduce/map) |
| 2026-03-17 | 이벤트 기반 목록 필터링, createElement 렌더링, Prototype, 비교/논리 연산자 |
| 2026-03-18 | 흐름제어(if/else if/else), while·for 반복문, 함수 선언식 vs 화살표 함수 |
| 2026-03-20 | Hoisting, Scope(전역/함수/블록), Closure, Callback, 마우스 이벤트(drag&drop) |
| 2026-03-23 | 키보드 이벤트(한글조합 composition), 체크박스, scroll/resize 이벤트, DOMContentLoaded vs load |
| 2026-03-24 | DOM 노드 CRUD, querySelectorAll, document.forms, 동적 노드 생성/삭제 |
| 2026-03-25 | 동기/비동기(setTimeout), Promise then/catch, async/await, Swiper 슬라이더 |
| 2026-03-27 | Swiper 세로형·멀티슬라이드, Lodash(throttle/debounce/cloneDeep), ScrollMagic |
| 2026-03-30 | ScrollMagic 심화, GSAP 애니메이션, Chart.js, QRCode.js, Leaflet 지도 기본 |
| 2026-03-31 | Leaflet 지오코더(reverse geocoding)·마커 클러스터링, Bootstrap5 컴포넌트(Nav/OffCanvas/Modal/Carousel/Card) |

</details>

### 핵심 역량
- 개발도구 적응 능력 및 웹 퍼블리싱 기초 이해
- GitHub 협업 워크플로우 활용 능력
- UI 구성 감각 및 JavaScript 기반 인터랙션 구현 능력

---

## 🌱 4월 학습 내용 (데이터베이스 / Java 입문)

### 주요 학습 주제
- MySQL DDL/DML/DCL/TCL, ERD 설계, 정규화(1NF~BCNF), JOIN/VIEW/PROCEDURE/TRIGGER
- 개발환경(Eclipse+Git), JIRA 협업툴
- Java 기초 문법(변수/형변환/연산자/제어문), 배열, 객체지향(캡슐화/상속/다형성/추상클래스/인터페이스)

<details>
<summary>날짜별 요약 (23일)</summary>

| 날짜 | 핵심 학습 주제 |
|---|---|
| 2026-04-01 | MySQL 설치, DATABASE/TABLE 생성, PK 지정, ALTER TABLE, INSERT/SELECT/UPDATE |
| 2026-04-03 | DDL/DML/DCL/TCL 구분, GRANT/REVOKE 권한부여, TRANSACTION(SAVEPOINT, autocommit) |
| 2026-04-06 | 외부 JSON/CSV 데이터 Import, ERD 개념(PK 실선/FK 점선 표기) |
| 2026-04-07 | ERD 심화 — 엔티티/관계/속성/키, 카디널리티(1:1, 1:N, N:M), 중간테이블 변환 |
| 2026-04-08 | 정규화 1NF~4NF(원자값/부분종속/이행종속/BCNF), SELECT 기초 |
| 2026-04-09 | INSERT 다중삽입/IGNORE, AUTO_INCREMENT, ON DUPLICATE KEY UPDATE, PK/FK 제약조건 |
| 2026-04-10 | JOIN(INNER/OUTER/UNION), PROCEDURE, TRANSACTION/SAVEPOINT, VIEW, TRIGGER |
| 2026-04-13 | Java Eclipse 설치·Git 연동, 정렬 알고리즘 자습(버블/선택/삽입/합병) |
| 2026-04-14 | 네트워크 서브넷마스크 계산, 리눅스 기본 명령어 자습 |
| 2026-04-15 | JIRA 설치, 프로젝트/이슈/에픽 생성, Confluence 연동 |
| 2026-04-16 | Java main 구조, print/println/printf, 이스케이프 문자, 진법 표현 |
| 2026-04-17 | 변수와 메모리 구조(Stack/Heap), Primitive vs Reference, 형변환·오버플로우 |
| 2026-04-20 | 자동/강제 형변환, Scanner 입력(nextInt/nextLine) 버퍼 처리 |
| 2026-04-21 | 증감연산자, 단락회로(&&/\|\|), 비트연산, switch fall-through |
| 2026-04-22 | while 누적합산, 중첩루프(구구단·별찍기), 조건부 매개변수 제어 |
| 2026-04-23 | 객체지향 입문(클래스=설계도, 객체=인스턴스), 별찍기 패턴 공식화 |
| 2026-04-24 | 메서드 오버로딩, 가변인자, 생성자/this(), 캡슐화, ==와 equals() |
| 2026-04-27 | String 메서드(charAt/indexOf/substring/split), StringBuilder, toString() |
| 2026-04-28 | 배열(얕은/깊은 복사, 2차원), static/싱글톤 패턴, 상속·오버라이딩·캐스팅 |
| 2026-04-29 | 업/다운캐스팅, 다형성, instanceof, 추상클래스, 인터페이스, final |

</details>

### 핵심 역량
- 데이터베이스 설계 및 SQL 활용 능력
- Java 언어 입문 → 객체지향 설계 이해
- 협업 툴(JIRA/Git) 활용 능력

---

## 🚀 5월 학습 내용 (Java 심화 / JSP·Servlet / Spring Boot 입문)

### 주요 학습 주제
- Object/Exception/Generic, Collection Framework, Swing GUI
- 파일 입출력(IO), JDBC, Socket/Thread 네트워크 프로그래밍, Reflection
- 람다식/Stream API, 객체지향 설계(추상클래스/인터페이스)
- JSP/Servlet, DTO/DAO/MVC(Model2), Cookie/Session, Filter/Listener
- Spring Boot 입문(IoC/DI/Bean), Spring MVC, Validation, Thymeleaf

<details>
<summary>날짜별 요약 (18일)</summary>

| 날짜 | 핵심 학습 주제 |
|---|---|
| 2026-05-04 | Object/Exception/Generic — toString/equals/hashCode, 업·다운캐스팅, 와일드카드 |
| 2026-05-06 | 컬렉션 프레임워크(List/Set/Map), Stream 정렬; Swing GUI(JFrame/JButton) 이벤트 |
| 2026-05-07 | 파일 입출력 — FileReader/Writer, FileInputStream/OutputStream, 버퍼 파일복사 |
| 2026-05-08 | 보조/데이터/객체 스트림 — BufferedReader, DataInputStream, 직렬화(Serializable) |
| 2026-05-11 | JDBC PreparedStatement CRUD, ResultSet, DTO, Transaction, 공공데이터 연동 |
| 2026-05-12 | Socket/Thread 멀티채팅(synchronized/wait-notifyAll); Reflection 기반 GUI 채팅 |
| 2026-05-13 | 람다식/메서드참조(`::`)/클로저, Stream filter·map·sorted·collect |
| 2026-05-14 | 함수형 인터페이스(andThen), Annotation+Reflection 자동주입, REST API(HttpClient/JSON) |
| 2026-05-15 | 추상클래스 기반 설계 — 상속(Marine/Medic), Has-A 관계, Thread 동시처리 |
| 2026-05-18 | 추상클래스/인터페이스 심화, Reflection 동적 객체생성, 제네릭 컬렉션 |
| 2026-05-19 | JSP 기초 — 선언문/스크립틀릿/표현식, GET/POST, JavaBean DTO, EL |
| 2026-05-20 | JSP Forward/Redirect, DTO/DAO 구조, JDBC 연결, 회원가입·로그인 흐름 |
| 2026-05-21 | 로그인/회원가입/세션 유지(session.setAttribute/invalidate); Cookie 생성·조회·삭제 |
| 2026-05-22 | Servlet MVC 전체 흐름(Controller→DAO→DB→JSP); Filter/Listener/Resource(Connection Pool) |
| 2026-05-26 | JDBC 인터페이스 프로젝트 — Outbox/Inbox 패턴(SEND/RECV/MONITOR), Batch, 재시도 처리 |
| 2026-05-27 | Spring Boot 입문 — IoC/DI(생성자 주입), Bean/DispatcherServlet, Lombok |
| 2026-05-28 | Spring MVC 파라미터 처리 — @RequestParam, DTO 바인딩, forward:/redirect: |
| 2026-05-29 | Validation(@NotBlank 등)+BindingResult, @ControllerAdvice 전역예외, Thymeleaf |

</details>

### 핵심 역량
- Java 객체지향 프로그래밍 및 계층형 구조 설계 능력
- JDBC 기반 DB 연동 및 트랜잭션 처리 이해
- JSP/Servlet 기반 MVC 요청 처리 및 세션 인증 구현 경험
- Spring Boot 기초(IoC/DI/Validation/예외처리) 이해

---

## ⚙️ 6월 학습 내용 (Spring Boot 고급 / 외부 API / 보안 / React)

### 주요 학습 주제
- MyBatis/JPA 데이터 접근, 페이징, 연관관계 매핑, 트랜잭션 관리
- RestController 기반 REST API, 카카오/네이버/구글 OAuth2 로그인, 카카오페이·PortOne 결제
- 공공데이터 Open API, FCM 푸시, 파일업로드, AOP, Scheduled/Batch
- Spring Security 인증/인가, JWT + Redis 기반 인증 구조
- Node.js/SCSS 환경, React 기초(JSX/Props/Hook) 및 Spring Boot 연동

<details>
<summary>날짜별 요약 (24일)</summary>

| 날짜 | 핵심 학습 주제 |
|---|---|
| 2026-06-01 | Thymeleaf(표현식/반복문/Fragment), 전역예외처리, DataSource/DAO 기반 JDBC |
| 2026-06-02 | MyBatis Annotation/XML Mapper, 동적 SQL(`<if>`,`<where>`), Bean Validation |
| 2026-06-04 | JPA Pageable/Page 페이징; 연관관계 매핑(@ManyToOne), JPQL Join Fetch, Lazy/Eager |
| 2026-06-05 | Spring Transaction — JpaTransactionManager vs DataSourceTransactionManager |
| 2026-06-08 | RestController, XHR 비동기통신, @RequestBody, ResponseEntity, Pageable REST API |
| 2026-06-09 | Book REST API, XHR/jQuery/Fetch/Axios 비교; 공공데이터 Open API(기상청/대구버스) |
| 2026-06-10 | 동기/비동기 요청 처리, OpenWeatherMap API, 카카오 OAuth2 로그인, 카카오맵 |
| 2026-06-11 | 카카오/네이버 로그인 OAuth2, 카카오페이, 외부 API 공통 패턴(HttpHeaders/HttpEntity) |
| 2026-06-12 | 카카오/네이버/구글 로그인, KakaoPay, Google Calendar/Mail API, Bearer 인증 |
| 2026-06-15 | PortOne 결제 API(토큰발급, 본인인증조회, 결제조회/취소) |
| 2026-06-16 | Firebase FCM 푸시알림, MultipartFile 파일업로드, AOP, Filter/Interceptor, Spring Batch |
| 2026-06-17 | Spring Event Listener, HandlerMapping, DispatcherServlet 흐름 |
| 2026-06-18 | Spring Security 기본설정(CSRF, UserDetails, BCrypt); 인증/인가 상세; OAuth2 Client(카카오) |
| 2026-06-22 | JWT 인증(AccessToken/RefreshToken), JWTAuthorizationFilter |
| 2026-06-23 | JWT + Redis 기반 RefreshToken 관리, AccessToken 재발급 |
| 2026-06-24 | Node.js/npm 개발환경 구축, SCSS(Nesting, 부모선택자, 변수) |
| 2026-06-25 | React 기초 문법(JSX, Component, Props, useState, useEffect) |
| 2026-06-26 | React 이벤트·조건부렌더링, React Router(Route/Layout/Outlet) |
| 2026-06-29 | React Props/Context API, React Router/Layout 심화 |
| 2026-06-30 | React+Spring Boot Axios 연동, JPA CRUD, FormData 파일업로드(Todo 프로젝트) |

</details>

### 핵심 역량
- JPA/MyBatis 기반 데이터 접근 및 연관관계 설계 능력
- OAuth2 소셜 로그인·결제 등 외부 API 연동 경험
- Spring Security/JWT 기반 인증·인가 구조 구현 능력
- React 기초 문법 이해 및 Spring Boot REST API 연동 경험

---

## ☁️ 7월 학습 내용 (배포/인프라 · Python/ML 입문)

### 주요 학습 주제
- React-Spring Boot 통합(파라미터/Validation/JPA/파일업로드/외부API/Security)
- Swagger API 문서화, Docker(Image/Container/Compose/Hub)
- AWS EC2, Jenkins CI/CD, Route 53 도메인 + SSL 인증서, HTTPS 자동배포
- Docker 기반 Jenkins 전환, GitHub-EC2 연동 자동배포
- Python 기초 문법 및 NumPy — 머신러닝 입문
- pandas 데이터 전처리(결측치/인코딩)와 지도학습(LinearRegression/LogisticRegression/RandomForest/LightGBM) 회귀·분류 파이프라인, 평가지표(MAE/RMSE/R², accuracy/ROC-AUC/precision/recall)
- 비지도학습(KMeans 군집화, PCA 차원축소, Apriori 연관규칙)과 IsolationForest 이상치 탐지
- Matplotlib/Seaborn 데이터 시각화(히스토그램/산점도/히트맵)
- FastAPI REST API 서버 구축 및 Docker 컨테이너화
- PySpark 분산처리(로컬/스탠드얼론 클러스터, Window 함수, Parquet 저장)

<details>
<summary>날짜별 요약 (17일)</summary>

| 날짜 | 핵심 학습 주제 |
|---|---|
| 2026-07-01 | React+Spring Boot 종합 — 파라미터 3방식, Validation/예외처리, JPA, 파일업로드, 외부 API(카카오/네이버/구글/FCM/토스페이먼츠), Security+JWT+OAuth2 |
| 2026-07-02 | React↔Spring Boot 로그인/로그아웃 — Axios+JWT, 토큰 검증, STATELESS 세션 설정 |
| 2026-07-03 | Swagger(SpringDoc/OpenAPI) 문서 자동화, Profile 분리, @ConfigurationProperties |
| 2026-07-06 | Docker 기초 — Image/Container 개념, Dockerfile 작성, 포트 매핑, Volume 영속성 |
| 2026-07-07 | Docker Compose로 React+Spring Boot+MySQL+Redis 다중 컨테이너 구성, Docker Hub Push/Pull |
| 2026-07-08 | AWS EC2 보안그룹/PuTTY SSH 접속, Jenkins 설치, GitHub Webhook 자동 빌드 |
| 2026-07-09 | Route 53 도메인 연결, Let's Encrypt SSL 발급, Jenkins HTTPS(443) 자동배포; Jenkins Docker 컨테이너 전환(DooD 구조) |
| 2026-07-10 | Docker 리소스 전체 정리 후 재기동, Jenkins-GitHub-EC2 SSH 자동배포, Nginx(FN)가 SSL 종단하도록 전환 |
| 2026-07-13 | 파이썬 기초 문법(변수/자료구조/제어문/함수) 및 중급 패턴, NumPy 배열(ndarray) 생성/인덱싱/벡터연산/axis 집계 — 머신러닝 입문 |
| 2026-07-14 | pandas Series/DataFrame 조작(loc/iloc/조건필터/인코딩), 결측치 처리(중앙값/최빈값), Adult Income 데이터 이진분류(RandomForest, accuracy/ROC-AUC) |
| 2026-07-15 | 이진분류 노트북 코드 리뷰 — EDA→전처리→인코딩→분할→학습→평가→제출 전체 파이프라인 원리 정리(데이터 누수 방지, stratify, predict vs predict_proba) |
| 2026-07-20 | 선형회귀(단순/다중) — 상관분석/히트맵, 원핫인코딩, MAE/RMSE/R², LightGBM 비교, statsmodels OLS로 계수 유의성(p-value) 검증 |
| 2026-07-21 | 로지스틱회귀 — 시그모이드, StandardScaler(fit은 train에만), 임계값 조정과 recall/precision 트레이드오프, joblib 모델+스케일러 저장 |
| 2026-07-22 | 비지도학습 — KMeans 군집화(실루엣 점수/Elbow Method), PCA 차원축소(explained_variance_ratio_), Apriori 연관규칙(지지도/신뢰도/향상도), 이상치 탐지 알고리즘 개관 |
| 2026-07-23 | IsolationForest 이상치 탐지(contamination, decision_function) 및 제거 전후 분류 성능 비교; Matplotlib 시각화(히스토그램/산점도/추세선)로 EDA·다중분류·회귀 관계 확인 |
| 2026-07-24 | FastAPI 서버 구축 및 Docker 컨테이너화, CORSMiddleware/Pydantic 요청 검증, feature_spec.json 기반 폼 자동생성, SQLite 연동 CRUD API |
| 2026-07-28 | PySpark 로컬(`local[*]`) 실행 — stack()으로 Wide→Long 변환, Window 함수(row_number/avg over), Parquet partitionBy 저장; 스탠드얼론 클러스터(spark://) 전환과 분산 처리 원리(executor/파티션 지역성) 검증 |

</details>


### 핵심 역량
- Docker/Docker Compose 기반 다중 컨테이너 설계·배포 능력
- AWS EC2 + Jenkins + Route 53/SSL을 이용한 CI/CD 파이프라인 구축 경험
- React-Spring Boot 풀스택 서비스 통합 및 배포 경험
- Python 기초 및 NumPy를 활용한 데이터 처리 입문
- pandas 기반 데이터 전처리와 scikit-learn 지도학습(회귀/분류)·비지도학습(군집화/차원축소/이상치탐지) 파이프라인 구현 및 평가지표 해석 능력
- FastAPI로 REST API 서버를 구축하고 Docker로 컨테이너화하는 능력
- PySpark를 활용한 대용량 데이터 분산 처리 개념 이해

---

## 🧗 전체 학습 흐름

- **2월**에는 **프로젝트 요구사항 분석과 화면설계**로 시작해, 개발 도구(draw.io, Figma, Git)에 적응하며 첫 발을 뗐습니다.
- **3월**에는 **프론트엔드 기초**에 집중하며 HTML/CSS 퍼블리싱부터 JavaScript 핵심 문법, 다양한 프론트 라이브러리(Swiper, GSAP, Leaflet 등) 실습까지 웹 개발의 기본기를 다졌습니다.
- **4월**에는 **데이터베이스와 Java 백엔드 기초**로 범위를 넓혀, MySQL 설계·정규화·SQL부터 Java 문법과 객체지향(상속·다형성·인터페이스)까지 풀스택 개발자로 성장하기 위한 기반을 체계적으로 학습했습니다.
- **5월**에는 **Java 심화(컬렉션·스트림·네트워크)**부터 **JSP/Servlet**을 거쳐 **Spring Boot**까지 학습 범위를 확장하며, 로그인 인증과 MVC 요청 처리 흐름을 직접 구현했습니다.
- **6월**에는 **JPA/MyBatis 데이터 계층, OAuth2 소셜 로그인·결제 등 외부 API 연동, Spring Security/JWT 인증**을 심화 학습하고, 후반부에는 **React**로 넘어가 프론트엔드와 Spring Boot를 Axios로 연동하는 풀스택 흐름을 완성했습니다.
- **7월**에는 React-Spring Boot 통합을 마무리한 뒤 **Docker, AWS EC2, Jenkins, Route 53/SSL**을 이용한 **CI/CD 자동배포 파이프라인**을 직접 구축했고, 이후 **Python·NumPy 기반 머신러닝**으로 학습 방향을 새롭게 확장했습니다. pandas 전처리부터 **지도학습(회귀·분류)과 비지도학습(군집화·차원축소·연관규칙·이상치탐지)** 전체 파이프라인을 실습했고, 이를 **FastAPI REST API 서버**로 서빙하는 흐름과 **PySpark 분산처리**(로컬→스탠드얼론 클러스터)까지 경험을 넓혔습니다.

요구사항 분석 → 프론트엔드 → 데이터베이스/Java → 웹 백엔드(Spring) → 인증/외부연동/React → 배포 인프라(Docker/AWS/Jenkins) → 데이터분석/머신러닝 → API 서버/분산처리까지, 5개월간 풀스택 개발 전 영역을 단계적으로 확장하며 학습했습니다.
