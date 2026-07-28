# 포트폴리오 사이트 개선 작업 지시서

대상 파일: `index.html` (단일 파일)

## 작업 원칙 (반드시 준수)

- **컬러는 기존 토큰만 사용.** 새 hex 값 추가 금지. `--color-brand`, `--color-accent`, `--color-surface-sunken` 등 `:root`에 이미 정의된 변수만 쓴다. 다크모드 대응이 자동으로 따라오게 하기 위함이다.
- 컴포넌트 CSS에 hex 직접 작성 금지 (기존 파일 상단 주석 규칙 유지).
- 기존 `--space-*`, `--radius-*`, `--text-*` 스케일을 벗어나는 임의 값 금지.
- 섹션 구조와 클래스명은 최대한 유지. 리팩터링이 아니라 수정 작업이다.
- 한 항목씩 적용하고, 적용 후 라이트/다크 양쪽에서 확인한다.

---

# P0 — 지금 당장 (버그 / 리스크)

## P0-1. 앵커 이동 시 제목이 고정 헤더에 가려짐

**증상:** 네비게이션에서 `#about`, `#stack` 등을 클릭하면 섹션 제목이 72px 헤더 뒤로 들어가 안 보인다.

**원인:** `header.nav`가 `position:fixed; height:var(--header-h)`인데 앵커 대상에 `scroll-margin-top`이 없다.

**수정:** BASE 영역에 추가.

```css
:where(section[id], main[id]){
  scroll-margin-top: calc(var(--header-h) + var(--space-4));
}
```

## P0-2. 전화번호 공개 노출

**문제:** `#contact`의 `<a href="tel:...">` 로 개인 휴대폰 번호가 정적 HTML에 그대로 박혀 있다. 크롤러/스팸 봇이 즉시 수집한다. 포트폴리오 사이트는 링크가 어디로 퍼질지 통제할 수 없다.

**수정:** Phone `contact-item` 블록 전체를 삭제하고, 그 자리에 GitHub를 넣어 2칸 그리드를 유지한다.

```html
<div class="contact-list">
  <div class="contact-item">
    <div class="ci-label">Email</div>
    <a class="ci-value" href="mailto:jsh340866@gmail.com">jsh340866@gmail.com</a>
  </div>
  <div class="contact-item">
    <div class="ci-label">GitHub</div>
    <a class="ci-value" href="https://github.com/jsh340866" target="_blank" rel="noopener">github.com/jsh340866</a>
  </div>
</div>
```

전화번호는 이력서 PDF(지원 시 직접 제출)에만 넣는다.

## P0-3. "GitHub Repo" 버튼이 레포가 아니라 프로필로 감

**문제:** ValuePick 섹션의 `GitHub Repo` 버튼이 `github.com/jsh340866`(프로필)로 연결된다. 라벨과 목적지가 불일치해 채용담당자가 레포를 찾아 헤맨다. 이건 **가장 중요한 링크**다.

**수정:** ValuePick 백엔드 레포 직링크로 교체한다.

```html
<a class="btn btn-secondary" href="https://github.com/project-valuepick/valuepick" target="_blank" rel="noopener">GitHub Repo</a>
```

Contact 섹션의 `GitHub` 버튼(`github.com/jsh340866`)은 프로필이 맞으므로 **그대로 둔다.** 프로젝트 레포와 개인 프로필은 각자 역할이 다르다.

## P0-4. 다크모드 첫 로드 시 흰 화면 번쩍임 (FOUC)

**증상:** 다크로 설정한 사용자가 재방문하면 라이트 화면이 한 프레임 보였다가 다크로 전환된다.

**원인:** 테마 복원 스크립트가 `</body>` 직전에 있어 CSS 페인트 이후에 실행된다.

**수정:** `<head>` 안 `<style>` **앞**에 인라인 스크립트를 추가하고, 하단 스크립트에서는 복원 로직을 제거한다.

```html
<!-- <head> 안, <style> 태그 바로 위 -->
<script>
(function(){
  var s = localStorage.getItem('theme');
  var d = window.matchMedia('(prefers-color-scheme: dark)').matches;
  if(s === 'dark' || (!s && d)) document.documentElement.setAttribute('data-theme','dark');
})();
</script>
```

하단 스크립트의 테마 IIFE는 토글 핸들러만 남긴다.

```javascript
(function(){
  var root = document.documentElement;
  var btn = document.getElementById('themeToggle');
  if(!btn) return;
  btn.addEventListener('click', function(){
    var isDark = root.getAttribute('data-theme') === 'dark';
    if(isDark){ root.removeAttribute('data-theme'); localStorage.setItem('theme','light'); }
    else { root.setAttribute('data-theme','dark'); localStorage.setItem('theme','dark'); }
  });
})();
```

부수 효과로 시스템 다크 설정 자동 대응까지 해결된다.

## P0-5. 한글 파일 경로

**문제:** 이미지 경로가 `프로젝트작업/docs/img/시스템%20아키텍쳐.png` 형태다. 서버/CDN/브라우저 조합에 따라 인코딩이 깨져 404가 난다. GitHub Pages는 대체로 동작하지만 보장되지 않고, 로컬 ↔ 배포 환경 불일치의 단골 원인이다. 공백까지 섞여 있어 위험이 배가된다.

**수정:** 디렉터리와 파일명을 전부 영문 소문자 kebab-case로 변경하고 HTML 참조를 일괄 치환한다.

```
프로젝트작업/docs/img/시스템 아키텍쳐.png  →  assets/img/system-architecture.png
프로젝트작업/docs/img/기술 아키텍처 .png   →  assets/img/tech-architecture.png
프로젝트작업/docs/img/Main_mobile.png      →  assets/img/mobile-main.png
프로젝트작업/docs/img/invest_mobile.png    →  assets/img/mobile-invest.png
프로젝트작업/docs/img/MyPage_mobile.png    →  assets/img/mobile-mypage.png
프로젝트작업/docs/GIF/mainpage-1.gif       →  assets/demo/home.gif
... (나머지 GIF 동일 규칙)
```

> 참고: "아키텍쳐"는 표준 표기 "아키텍처"의 오기. `alt` 텍스트와 캡션도 함께 수정할 것. 외부 링크 URL(`project-valuepick.github.io/valuepick/시스템%20아키텍쳐.html`)도 동일 문제를 갖고 있으나 별도 레포이므로 여기서는 건드리지 않는다.

## P0-6. 데모 이미지 초기 상태에 `src` 없음

**문제:** `<img id="featureImg" alt="기능 데모" loading="lazy">` — `src` 속성 없이 시작한다. JS 실행 전까지 깨진 이미지가 노출되고, JS가 실패하면 영구적으로 빈 칸이다. 또한 JS로 `src`를 주입하므로 `loading="lazy"`는 아무 효과가 없다.

**수정:** 첫 번째 탭의 이미지를 HTML에 직접 넣고 `loading="lazy"`를 제거한다.

```html
<div class="media-frame">
  <img id="featureImg" src="assets/demo/home.gif"
       alt="ValuePick 홈 화면 데모">
</div>
<p class="media-cap" id="featureCap">홈 · 코스피 지수/환율 위젯, TOP10, 4대 랭킹 — 10초 주기 실시간 갱신</p>
```

JS의 `activate()`에서 `img.alt`도 함께 갱신하도록 수정한다.

```javascript
img.src = btn.dataset.src;
img.alt = btn.textContent.trim() + ' 화면 데모';
cap.textContent = btn.dataset.cap;
```

---

# P1 — 채용담당자가 바로 걸리는 지점 (콘텐츠)

## P1-1. 자격증 섹션에서 운전면허 제거

**문제:** 섹션 설명이 "실무 지식을 자격으로도 증명해가고 있습니다"인데 카드 4개 중 하나가 **2종 보통 운전면허**다. 설명과 정면 충돌하고, "쓸 게 없어서 채웠구나"로 읽힌다. 백엔드 채용에서 감점 요인이다.

**수정:** 해당 `cert-card` 삭제 → 3칸 그리드로 조정.

```css
.cert-grid{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:var(--space-4);}
@media(max-width:900px){.cert-grid{grid-template-columns:repeat(2,minmax(0,1fr));}}
@media(max-width:520px){.cert-grid{grid-template-columns:minmax(0,1fr);}}
```

추가로, "취득 예정" 항목에는 **목표 응시 회차**를 명시해 구체성을 더한다. (예: "2026년 3회 응시 예정")

## P1-2. Hero lead 문장을 완료형으로 교체

**h1은 그대로 둔다.** "반갑습니다, 정승원입니다"라는 담백한 인사말은 의도된 선택이며 변경하지 않는다. 헤드라인에 카피라이팅을 얹으면 오히려 과장된 인상을 준다.

**문제는 바로 아래 `lead` 문장이다.**

> 데이터를 다루는 백엔드 개발자를 **목표로 하고 있습니다**. ... 만드는 일에 **관심이 많습니다**.

한 문장에 지망 표현이 두 번 들어간다. 실제로는 2,559개 기업 수집 파이프라인을 구현하고 배포까지 완료했으므로 "하고 싶다"가 아니라 "했다"로 말할 근거가 있다. 현재 문장은 스스로 지망생 프레임을 씌워 사이트 전체 톤을 한 단계 낮춘다.

**수정:** `h1`은 유지하고 `lead`만 완료형으로 교체한다.

```html
<span class="eyebrow">OPEN TO WORK · 국비 풀스택 과정 26.08 수료 예정</span>
<h1>반갑습니다,<br><span class="name">정승원</span>입니다</h1>
<p class="lead">
  DART·KRX·환율 등 4종 외부 API를 매일 자동 수집해 투자지표를 계산하는
  백엔드 파이프라인을 설계·구현했습니다. 데이터가 안정적으로 쌓이고
  정확한 시간에 도는 시스템을 만듭니다.
</p>
```

바뀐 것은 동사뿐이다. "목표로 하고 있습니다" → "설계·구현했습니다", "관심이 많습니다" → "만듭니다".

**연쇄 확인:** About 섹션 첫 문단에도 동일한 톤의 문장("관심이 많은 백엔드 개발자입니다")이 있다. hero와 중복되므로 About 쪽은 전향 계기 서술로 시작하도록 다듬는다.

## P1-3. Weakness 항목 삭제 또는 리프레이밍

**문제:** About 섹션에 "Weakness & 보완" 카드가 있다. 약점 자진 공개는 **자소서와 면접의 영역**이지, 공개 웹사이트의 영역이 아니다. 사이트는 통과시키는 용도고, 약점은 그 다음 단계에서 대화로 푸는 것이다. "조바심을 내는 편"이라는 문장은 필터링 근거로 쓰일 수 있다.

**수정:** `t-label`을 `Approach`로 바꾸고 내용을 문제 해결 방식으로 재작성한다.

```html
<div class="trait">
  <div class="t-label">Approach</div>
  <p>문제가 생기면 코드부터 고치지 않고 로그와 실제 데이터를 먼저 확인합니다.
     원인을 작은 단위로 나눠 검증한 뒤 수정 범위를 정합니다.</p>
</div>
```

같은 내용을 강점의 언어로 말한 것이다. 사실을 왜곡한 게 아니라 초점을 바꾼 것이다.

## P1-4. `10+` 지표가 검증 불가

**문제:** metric 카드에 "10+ · 실제 트러블슈팅 & 기술적 의사결정"이라고 써 있지만 사이트에 노출된 건 4건이다. 확인 가능한 숫자와 주장이 어긋나면 나머지 지표의 신뢰도까지 같이 떨어진다.

**수정 (택1):**
- (a) 사이트에 4건만 있으므로 `4`로 낮추고 라벨을 "문서화된 트러블슈팅"으로 변경
- (b) `10+` 유지하되, 나머지 6건을 정리한 문서/README 링크를 metric 카드에 건다 — **이쪽을 권장**

## P1-5. "4인" metric은 성과가 아님

**문제:** metric 4개 중 "4인 · 팀 프로젝트, 1차 배포 완료"는 성과 지표가 아니라 사실 진술이다. 게다가 섹션 헤드에 이미 "4인 팀 프로젝트, 1차 배포 완료"라고 적혀 있어 중복이다.

**수정:** 본인이 만든 수치로 교체. 예시:

```html
<div class="metric">
  <div class="num">2,559</div>
  <div class="label-txt">일 단위 자동 수집 대상 상장기업 수</div>
</div>
```

> 실제 값은 사용자가 확인 후 확정. 스코어링 소요 시간, 스케줄러 일일 처리 건수 등도 후보.

## P1-6. 트러블슈팅 Result에 숫자 부족

**문제:** ISSUE 01만 정량적(`2,700회 → 1회`)이고 나머지 3건은 정성적이다. 특히 ISSUE 03(N+1)은 성능 문제인데 결과가 "쿼리 1회로 처리"뿐이다. 면접에서 **"그래서 얼마나 빨라졌나요?"**는 100% 나온다.

### 대원칙 — 기억으로 숫자를 쓰지 않는다

**측정하지 않은 수치는 절대 사이트에 올리지 않는다.** 근거 없는 숫자는 면접에서 한 번만 파고들어도 무너지고, 그 순간 나머지 지표 전체의 신뢰가 같이 날아간다. 숫자가 없는 편이 틀린 숫자보다 안전하다.

측정 전까지는 아래 **중간 문구**를 쓰고, 측정이 끝나면 확정 수치로 교체한다.

### ISSUE 03 — 규모 표현 주의

기억으로는 "기업 하나 조회할 때마다 2천 개가량의 쿼리"로 남아 있으나, 사이트에 적힌 원인 설명(`StockIndicator` 조회 시 LAZY `Company`를 지표 건수만큼 추가 SELECT)과 맞춰보면 실제 구조는 다음에 가깝다.

```
지표 목록 조회         1회
+ 지표 건수만큼 Company 추가 SELECT   N회   ← N이 수천 단위
─────────────────────────────
합계  1 + N 회  →  JOIN FETCH 적용 후 1회
```

즉 **기업 1개당 2천 쿼리가 아니라, 전체 스코어링 1회에 총 2천여 쿼리**다. 수집 대상 기업이 2,559개이므로 N이 그 규모인 것과 일치한다. 이 차이를 헷갈린 채로 쓰면 면접에서 바로 지적당한다. **반드시 측정해서 확인할 것.**

### 측정 방법

`application.yml`에 임시로 추가한다.

```yaml
spring:
  jpa:
    properties:
      hibernate:
        generate_statistics: true
logging:
  level:
    org.hibernate.stat: DEBUG
```

1. `JOIN FETCH`를 **제거한 이전 버전**으로 스코어링을 1회 실행 → 로그의 `Statistics` 블록에서 `queries executed to database` 와 총 소요 시간 기록
2. `JOIN FETCH` 적용 버전으로 동일하게 1회 실행 → 같은 값 기록
3. 두 값을 비교해 표에 채운다
4. **측정이 끝나면 위 설정을 원복한다.** 운영에서 켜두면 오버헤드가 있다.

> 이전 버전 재현이 어려우면 `git log`에서 해당 커밋을 찾아 별도 브랜치로 체크아웃해 돌린다. 커밋 해시를 확보해두면 그 자체가 근거가 된다.

### 보완할 형태

| 이슈 | 현재 결과 | 측정 후 목표 형태 |
|---|---|---|
| 02 재무 누락 | 항상 정확히 매칭 | 값이 0으로 저장되던 기업 N개사 → 0개사 |
| 03 N+1 | 쿼리 1회로 처리 | 스코어링 1회당 쿼리 `1+N회` → `1회`, 소요 `Xs` → `Ys` |
| 04 리츠/스팩 | 화이트리스트 제거 | 하드코딩 목록 N개 제거, 오탐 N건 해소 |

### 중간 문구 (측정 전까지 사용)

숫자 없이도 "무엇이 달라졌는지"는 정확히 말할 수 있다.

```html
<!-- ISSUE 03 -->
<div class="ts-result">결과: 지표 건수만큼 발생하던 추가 SELECT를 제거해, 전체 종목 스코어링을 단일 쿼리로 처리</div>

<!-- ISSUE 02 -->
<div class="ts-result">결과: 계정명 표기가 다른 기업에서도 누락 없이 매칭, 이후 신규 표기에도 코드 수정 불필요</div>

<!-- ISSUE 04 -->
<div class="ts-result">결과: 하드코딩 화이트리스트 제거, 신규 상장 종목도 코드 수정 없이 자동 분류</div>
```

ISSUE 02·04의 "코드 수정 없이 동작한다"는 서술은 숫자보다 오히려 설계 감각을 더 잘 보여준다. 이 둘은 측정에 매달리지 말고 이 문구로 확정해도 좋다. **측정이 꼭 필요한 건 ISSUE 03 하나다.**

## P1-7. 아키텍처 이미지에 텍스트 설명 없음

**문제:** 다이어그램 이미지 2장에 캡션이 제목뿐이다. 다이어그램은 화면에서 축소되면 글자가 안 읽히고, `alt="시스템 아키텍처"`로는 스크린리더 사용자에게 아무 정보도 전달되지 않는다.

**수정:** 각 `arch-card` 캡션 아래에 한 줄 요약을 추가한다.

```html
<div class="cap">
  <span>시스템 아키텍처</span>
  <a href="..." target="_blank" rel="noopener">상세보기</a>
</div>
<p class="arch-desc">스케줄러가 4종 외부 API를 순차 수집 → MySQL 적재 → 지표 계산 → TOP100 스코어링까지의 일일 배치 흐름</p>
```

```css
.arch-desc{
  margin:0;padding:0 var(--space-5) var(--space-5);
  font-size:var(--text-sm);color:var(--color-ink-soft);word-break:keep-all;
}
```

`alt`도 동일한 내용으로 채운다.

---

# P2 — 완성도 (성능 / 접근성 / 공유)

## P2-1. GIF 8개 — 용량 폭탄

**문제:** GIF는 압축 효율이 매우 나쁘다. 1920×1080 UI 데모 GIF는 보통 5~20MB다. 8개면 모바일에서 데이터를 수십 MB 태울 수 있고, 첫 탭은 즉시 로드된다.

**수정 (효과 순):**

1. **GIF → MP4/WebM 변환.** 동일 화질에서 GIF 대비 10~20배 작다.
   ```bash
   ffmpeg -i home.gif -movflags faststart -pix_fmt yuv420p \
     -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" -crf 28 home.mp4
   ```
   `<img>` 대신 아래로 교체한다. (자동재생 조건: `muted` + `playsinline` 필수)
   ```html
   <video id="featureVid" class="media-el"
          src="assets/demo/home.mp4"
          autoplay muted loop playsinline
          preload="metadata"
          aria-label="ValuePick 홈 화면 데모"></video>
   ```
   JS에서 `img.src` 대신 `vid.src` 갱신 + `vid.load()` 호출.

2. MP4 전환이 부담스러우면 최소한 GIF 폭을 1280px 이하로 리사이즈하고 프레임레이트를 10~12fps로 낮춘다.

3. 탭 전환 시 이전 미디어를 정지시켜 백그라운드 디코딩을 막는다.

## P2-2. `object-fit:cover` — 주석과 동작이 반대

**문제:**
```css
/* 원본과 동일한 16:9 — 비율 불일치로 인한 크롭·확대 방지 */
.media-frame img{width:100%;aspect-ratio:16/9;object-fit:cover;}
```
주석은 "크롭 방지"인데 `cover`는 **넘치는 부분을 잘라낸다**. 원본이 정확히 16:9가 아닌 GIF가 하나라도 있으면 UI가 잘린다.

**수정:**
```css
.media-frame img,
.media-frame video{
  width:100%;aspect-ratio:16/9;object-fit:contain;
  background:var(--color-surface-sunken);display:block;
}
```

## P2-3. 탭 접근성 — 반쪽 구현

**문제:** `role="tablist"`만 선언하고 `role="tab"`, `aria-controls`, `role="tabpanel"`, 키보드 화살표 이동이 전부 없다. 스크린리더는 탭 위젯으로 인식했다가 기대한 동작이 없어 오히려 혼란을 준다. **role만 선언하고 계약을 안 지키는 게 role을 안 쓴 것보다 나쁘다.**

**수정 (둘 중 택1):**

**(a) 간단한 길 — role 전부 제거.** 그냥 버튼 그룹으로 둔다. 기능상 아무 손해 없다.
```html
<div class="tab-list" id="tabList">
  <button class="tab-btn active" type="button" aria-pressed="true" ...>홈 화면</button>
```
JS에서 `aria-selected` 대신 `aria-pressed`를 토글한다.

**(b) 제대로 구현.** 각 버튼에 `role="tab"` `id` `aria-controls`, 패널에 `role="tabpanel"` `aria-labelledby`, 비활성 탭에 `tabindex="-1"`, 좌우 화살표 키 핸들러 추가.

> 면접에서 "접근성 신경 쓰셨네요"를 듣고 싶다면 (b), 리스크만 없애려면 (a). **(a)를 권장** — 잘못 구현된 ARIA보다 없는 게 낫고, 접근성 어필은 다른 곳(포커스 링, reduced-motion)에서 이미 하고 있다.

## P2-4. 모바일 네비게이션 부재

**문제:** `@media(max-width:760px)`에서 `nav.links{display:none}`으로 메뉴가 통째로 사라진다. 대체 수단이 없어 모바일에서는 긴 페이지를 스크롤로만 탐색해야 한다. 채용담당자는 상당수가 모바일로 먼저 연다.

**수정 (가벼운 방식 권장):** 헤더를 건드리지 말고, 모바일에서만 나타나는 가로 스크롤 섹션 바를 헤더 아래에 붙인다.

```html
<!-- header 바로 다음 -->
<nav class="section-bar" aria-label="섹션 바로가기">
  <a href="#about">About</a>
  <a href="#stack">Stack</a>
  <a href="#certs">Certificates</a>
  <a href="#project">Project</a>
  <a href="#contact">Contact</a>
</nav>
```

```css
.section-bar{display:none;}
@media(max-width:760px){
  .section-bar{
    display:flex;gap:var(--space-2);overflow-x:auto;
    position:fixed;top:var(--header-h);left:0;right:0;z-index:99;
    padding:var(--space-2) var(--gutter);
    background:var(--color-surface);
    border-bottom:1px solid var(--color-border);
    scrollbar-width:none;
  }
  .section-bar::-webkit-scrollbar{display:none;}
  .section-bar a{
    flex:0 0 auto;text-decoration:none;white-space:nowrap;
    padding:var(--space-2) var(--space-3);border-radius:var(--radius-xs);
    font-size:var(--text-sm);font-weight:600;color:var(--color-ink-soft);
    background:var(--color-surface-sunken);
  }
  :where(section[id]){scroll-margin-top:calc(var(--header-h) + 56px);}
  .hero{padding-block-start:calc(var(--header-h) + 56px + var(--space-8));}
}
```

## P2-5. OG 메타 태그 없음 + 배포 URL 정리

**현재 배포 주소:** `https://jsh340866.github.io/jsh340866/`

### 5-a. 레포명 변경 권장 (OG보다 먼저)

현재는 사용자명 `jsh340866` 아래에 같은 이름의 레포 `jsh340866`을 둔 **프로젝트 페이지** 구조라 경로에 이름이 두 번 들어간다. GitHub Pages는 레포명을 `<사용자명>.github.io`로 지으면 **사용자 페이지**로 승격되어 루트 경로를 쓴다.

```
현재:  https://jsh340866.github.io/jsh340866/
변경:  https://jsh340866.github.io/
```

**작업:** GitHub > 해당 레포 > Settings > 최상단 Repository name을 `jsh340866.github.io`로 변경 → Rename. 반영에 몇 분 걸린다.

**지금 해야 하는 이유:** 아직 이 URL을 어디에도 배포·공유하지 않았으므로 링크가 깨질 곳이 없다. 이력서에 주소를 적은 뒤에 바꾸면 그 이력서들이 전부 죽는다. OG 태그도 URL이 확정된 뒤에 붙여야 한다.

> 부수 효과: 경로가 루트가 되므로 이후 상대경로(`assets/img/...`) 계산이 단순해지고, 이력서·메일에 적을 때도 짧아진다.

### 5-b. OG 메타 태그

**문제:** 카카오톡·슬랙·링크드인으로 사이트 링크를 보내면 제목도 썸네일도 없는 맨 URL로 뜬다. 지원 메일에 링크를 넣는 순간 손해를 본다.

**주의:** `og:url`과 `og:image`는 **반드시 `https://`로 시작하는 절대경로**여야 한다. 크롤러는 페이지 맥락 없이 HTML만 가져가므로 상대경로를 해석하지 못한다.

**수정:** `<head>`에 추가. (레포명 변경을 완료한 기준)

```html
<meta property="og:type" content="website">
<meta property="og:title" content="정승원 — Backend Developer Portfolio">
<meta property="og:description" content="DART·KRX·환율 데이터를 매일 자동 수집해 저평가 우량주를 스코어링하는 파이프라인을 설계·구현했습니다.">
<meta property="og:url" content="https://jsh340866.github.io/">
<meta property="og:image" content="https://jsh340866.github.io/assets/img/og-cover.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:locale" content="ko_KR">
<meta name="twitter:card" content="summary_large_image">
```

> 레포명을 바꾸지 않기로 했다면 두 URL을 `https://jsh340866.github.io/jsh340866/` 와 `https://jsh340866.github.io/jsh340866/assets/img/og-cover.png` 로 쓴다. **끝 슬래시를 빠뜨리지 말 것.**

### 5-c. OG 커버 이미지

`og-cover.png` — 1200×630. 사이트 토큰과 동일한 값으로 제작한다.

| 요소 | 값 |
|---|---|
| 배경 | `#FFFFFF` (`--color-surface`) |
| 본문 텍스트 | `#12141A` (`--color-ink`) |
| 포인트 | `#0B5F66` (`--color-brand`) |
| 폰트 | Pretendard Bold |

내용은 3줄이면 충분하다.

```
정승원
Backend Developer
DART·KRX 데이터 파이프라인 · ValuePick
```

### 작업 순서 (중요)

```
1) 레포명 변경 → URL 확정
2) P0-5 (한글 경로 → assets/) 완료
3) og-cover.png 제작 후 assets/img/에 배치
4) OG 태그 삽입 → 배포
5) 카카오톡으로 본인에게 링크 전송해 미리보기 확인
```

**OG는 캐시가 강하다.** 카카오톡·슬랙은 한 번 읽은 미리보기를 오래 보관하므로, 잘못된 상태로 먼저 공유하면 수정해도 며칠간 그대로 노출된다. 위 순서를 지켜 **완성된 상태에서 처음 공유**할 것.

## P2-6. 빈 favicon

**문제:** `<link rel="icon" href="data:,">`. 브라우저 탭에 기본 문서 아이콘이 뜬다. 채용담당자가 탭 여러 개 열어놓으면 구분이 안 된다.

**수정:** 외부 파일 없이 인라인 SVG로 처리한다.

```html
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'><rect width='32' height='32' rx='6' fill='%230B5F66'/><text x='16' y='22' font-size='17' font-family='sans-serif' font-weight='700' fill='%23fff' text-anchor='middle'>S</text></svg>">
```

> 여기서만 hex 하드코딩이 불가피하다 (`data:` URI에는 CSS 변수를 쓸 수 없음). `%230B5F66`은 `--color-brand`와 동일한 값이다. 주석으로 명시할 것.

## P2-7. Skip link 없음

**수정:** `<body>` 최상단에 추가.

```html
<a class="skip-link" href="#top">본문으로 건너뛰기</a>
```

```css
.skip-link{
  position:absolute;left:var(--space-4);top:-100px;z-index:200;
  padding:var(--space-3) var(--space-4);border-radius:var(--radius-sm);
  background:var(--color-brand);color:var(--color-inverse);
  font-size:var(--text-sm);font-weight:600;text-decoration:none;
  transition:top .15s ease;
}
.skip-link:focus{top:var(--space-3);}
```

## P2-8. 타이포그래피 전면 교체 — Syne 제거, Pretendard + 시스템 mono

> **우선순위 상향.** 분량상 P2에 두었으나 실제로는 P1 직후에 처리한다. 사이트 전체 인상을 좌우하고, 다른 CSS 수정과 충돌할 수 있어 먼저 정리하는 편이 낫다.

### 문제

`--font-display: 'Syne'`인데 **Syne에는 한글 글리프가 없다.** 따라서 `h1,h2,h3,h4`에 걸어둔 display 폰트가 대부분 적용되지 않는다.

| 요소 | 내용 | 실제 렌더링 |
|---|---|---|
| h1 | 반갑습니다, 정승원입니다 | Pretendard (폴백) |
| h2 | 사용 기술 / 자격증 / 트러블슈팅 | Pretendard (폴백) |
| Stack h3 | Backend / Frontend / Infra | **Syne** |
| Cert h3 | 정보처리기사 | Pretendard (폴백) |
| ts-card h4 | 재무 데이터가 0으로 누락되는 버그 | Pretendard (폴백) |
| 로고 | Seungwon.dev | **Syne** |
| metric .num | 2,700 → 1 | **Syne** (숫자만) |

파생 문제 3가지:

1. **위계 붕괴** — Stack 섹션 h3("Backend")는 Syne, Certificates 섹션 h3("정보처리기사")는 Pretendard로 보인다. 같은 계층인데 서체가 다르다. 의도한 것이 아니라 폴백의 우연한 결과다.
2. **자간 오적용** — 폴백된 한글이 `letter-spacing:-0.03em`(라틴 기준)을 그대로 받는다. 한글은 글자폭이 넓어 이 자간이면 붙어 보이고, `--text-hero`(최대 4.5rem)에서 특히 두드러진다.
3. **낭비된 로드** — 웨이트 3종(600/700/800)을 받아오지만 800은 h1에 걸려 한글이라 미사용, 600도 사용처가 없다. 실제 Syne 노출은 로고 1개 + Stack h3 3개 + 숫자 몇 개가 전부다.

추가로 Syne는 아트센터·페스티벌 브랜딩용 실험 서체다. 이 사이트가 내세우는 정밀함·재현성·스케줄 신뢰성과 톤이 맞지 않는다.

### 방향

**Pretendard 단일 서체 + 시스템 mono.**

- Pretendard가 한글·영문 본문과 모든 헤딩을 담당한다. 위계는 서체 대비가 아니라 **웨이트(800/700/600)와 자간**으로 만든다.
- 숫자·영문 라벨·로고에만 **시스템 mono**를 쓴다. `ui-monospace, SFMono-Regular, Menlo, Consolas` 스택이므로 **네트워크 요청 0건**이다 (기존 `code{}` 규칙에서 이미 쓰던 스택을 변수로 승격하는 것뿐).
- **mono는 한글이 들어가는 요소에 절대 적용하지 않는다.** 적용하면 Syne와 동일한 폴백 문제가 재발한다.

### 1) `<head>` — Syne 관련 3줄 삭제

```html
<!-- 삭제 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@600;700;800&display=swap" rel="stylesheet">

<!-- 유지 (이 한 줄만 남는다) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.min.css">
```

Google Fonts 요청과 preconnect 2건이 사라져 초기 로딩이 빨라진다.

> Pretendard의 `variable-dynamic-subset` 사용은 그대로 유지한다. 실제 사용된 글자만 내려받는 방식이라 한글 폰트 용량 문제를 해결해준다.

### 2) 토큰 교체

```css
:root{
  /* --font-display 삭제 */
  --font-sans:'Pretendard Variable',Pretendard,-apple-system,BlinkMacSystemFont,'Malgun Gothic',sans-serif;
  --font-mono:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;

  /* --tracking-display 삭제 → 한글 기준으로 완화한 3단계로 대체 */
  --tracking-tight:  -0.02em;   /* hero 등 대형 */
  --tracking-snug:   -0.012em;  /* h2 / h3 */
  --tracking-normal: -0.005em;  /* h4 */

  /* hero 크기 하향 — Syne 800 기준으로 잡힌 값이라 한글에서 과하다 */
  --text-hero: clamp(2.25rem, 4.2vw, 3.75rem);
}
```

기존 `code{}` 규칙의 하드코딩된 mono 스택도 `var(--font-mono)`로 교체한다.

### 3) 헤딩 위계 — 웨이트로 만들기

```css
h1,h2,h3,h4{
  font-family:var(--font-sans);
  line-height:var(--leading-tight);
  margin:0;
}
h1{font-weight:800;letter-spacing:var(--tracking-tight);}
h2{font-weight:700;letter-spacing:var(--tracking-snug);}
h3{font-weight:700;letter-spacing:var(--tracking-snug);}
h4{font-weight:600;letter-spacing:var(--tracking-normal);}
```

### 4) mono 적용 — 영문·숫자만 담는 요소에 한정

```css
/* 로고 — 도메인처럼 읽히게 */
.logo{
  font-family:var(--font-mono);font-weight:700;
  font-size:var(--text-lg);letter-spacing:-0.03em;line-height:1;
  text-decoration:none;color:var(--color-ink);
}

/* 수치 — 등폭 정렬이 성과를 강하게 보이게 함 */
.metric .num{
  font-family:var(--font-mono);font-weight:700;
  font-size:var(--text-xl);letter-spacing:-0.02em;
  font-variant-numeric:tabular-nums;
  color:var(--color-brand);
  overflow-wrap:anywhere;line-height:1.2;
}
.t-row .t-date{
  font-family:var(--font-mono);
  font-variant-numeric:tabular-nums;
  color:var(--color-ink-faint);min-width:72px;
}

/* 라벨류 — 로그/터미널 톤. 트러블슈팅 섹션 성격과 맞는다 */
.kicker,
.role-item .num,
.ts-block .lbl,
.trait .t-label,
.contact-item .ci-label{
  font-family:var(--font-mono);font-weight:600;
}
```

`ISSUE 01` / `PROBLEM` / `APPROACH` / `TECH STACK` 라벨과 `2,700 → 1`, `2,559`, `2026.03` 수치가 등폭으로 정렬된다.

### 5) 잔여 참조 제거

`.logo .logo-dot`, `.section-head h2`, `.project-panel h3`, `.ts-card h4` 등 개별 규칙에 남아 있는 `font-family:var(--font-display)`와 `letter-spacing:var(--tracking-display)`를 **전부** 찾아 제거하거나 위 값으로 교체한다.

```bash
grep -n "font-display\|tracking-display\|Syne" index.html   # 결과 0건이어야 함
```

`.logo-dot`은 `font-family:inherit`이므로 자동으로 mono를 상속한다 — 별도 수정 불필요.

### 검증

- [ ] `grep -c "font-display\|Syne" index.html` → `0`
- [ ] Stack h3 "Backend"와 Certificates h3 "정보처리기사"가 **같은 서체**로 보임
- [ ] hero h1이 360px 폭에서 3줄 이내, 자간이 붙어 보이지 않음
- [ ] metric `2,700 → 1`의 화살표(U+2192)가 정상 출력 — mono 스택에서 폴백되면 그 글자만 튄다
- [ ] 다크모드에서 h1 800 웨이트가 과하게 굵어 보이면 `[data-theme="dark"] h1{font-weight:700;}` 추가 (어두운 배경에서 글자가 굵어 보이는 착시 보정)

## P2-9. 모바일 스크린샷이 200px — 내용 판독 불가

**문제:** `.phone{width:200px}`에 전체 화면 스크린샷을 넣으면 아무것도 안 읽힌다. 자리만 차지하고 정보 전달은 0이다.

**수정 (택1):**
- (a) 클릭 시 원본을 새 탭으로 여는 링크로 감싼다 — 가장 간단
- (b) 섹션을 통째로 삭제하고, Showcase 탭 캡션에 "반응형 지원" 한 줄만 남긴다

```html
<a class="phone" href="assets/img/mobile-main.png" target="_blank" rel="noopener">
  <img src="assets/img/mobile-main.png" alt="홈 화면 모바일 레이아웃" loading="lazy">
</a>
```
```css
.phone{display:block;text-decoration:none;transition:transform .15s ease;}
.phone:hover{transform:translateY(-2px);}
```

## P2-10. 탭 리스트 가로 스크롤 힌트 없음

**문제:** 탭 8개가 모바일에서 가로 스크롤되는데, 오른쪽에 더 있다는 시각적 단서가 없어 앞의 2~3개만 보고 넘어간다.

**수정:** 우측 페이드 마스크.

```css
.tab-list{
  mask-image:linear-gradient(to right,#000 calc(100% - 32px),transparent 100%);
  -webkit-mask-image:linear-gradient(to right,#000 calc(100% - 32px),transparent 100%);
}
@media(min-width:1000px){
  .tab-list{mask-image:none;-webkit-mask-image:none;}
}
```

---

# P3 — 정리 (기능 영향 없음)

## P3-1. 미사용 토큰 제거

다음 토큰들이 정의만 되고 어디서도 참조되지 않는다. 삭제하거나, 향후 사용 계획이 있으면 주석으로 용도를 남긴다.

```
--color-success / --color-warning / --color-danger
--color-scrim
--shadow-lift
--radius-md 일부 · --radius-xl 일부
.label-accent  (--color-accent도 동반 미사용)
.btn-sm
.hide-mobile   (마크업에 사용처 없음)
```

`--color-accent`는 살려서 쓰는 쪽이 낫다. 현재 페이지는 브랜드 틸 단색이라 시선의 위계가 평평하다. **딱 한 곳** — Hero의 `.eyebrow` "OPEN TO WORK" 부분에만 accent를 쓰면 구직 상태가 즉시 눈에 들어온다.

```css
.hero .eyebrow{
  color:var(--color-accent);
  background:color-mix(in srgb, var(--color-accent) 12%, transparent);
}
```

> 포인트 컬러는 한 군데에서만 써야 포인트다. 다른 곳에 확산시키지 말 것.

## P3-2. 인쇄 스타일

채용담당자가 페이지를 PDF로 저장하는 경우가 있다. 현재는 고정 헤더가 매 페이지에 겹치고 다크모드에서 배경이 통째로 인쇄된다.

```css
@media print{
  header.nav,.section-bar,.theme-btn,.skip-link,.tab-list{display:none !important;}
  .reveal{opacity:1 !important;transform:none !important;}
  :root{--color-bg:#fff;--color-surface:#fff;--color-ink:#000;}
  a[href^="http"]::after{content:" (" attr(href) ")";font-size:10px;}
  section{padding-block:var(--space-6);break-inside:avoid;}
}
```

## P3-3. 문구 다듬기

| 위치 | 현재 | 수정 |
|---|---|---|
| Contact h2 | 같이 일해보고 싶으신가요? | 함께 일할 기회를 찾고 있습니다 |
| Contact p | 편하게 연락 주세요 | 이력서와 상세 이력이 필요하시면 메일 주세요. 24시간 내 회신합니다. |
| 아키텍처 캡션 | 아키텍쳐 | 아키텍처 (전체 치환) |

Contact 헤드라인이 질문형이면 방문자에게 판단을 미루는 느낌이 된다. 상태를 진술하는 편이 낫다.

---

# 적용 순서

```
1) P0 전체        — 버그·리스크. 한 번에 처리 후 라이트/다크 양쪽 확인
2) P2-8           — 타이포그래피 전면 교체. 다른 CSS 수정과 충돌하므로 먼저 정리
3) P1-1 ~ P1-3    — 콘텐츠 삭제·재작성. 코드 변경 최소
4) P1-4 ~ P1-6    — 수치 확보 필요 (hibernate.generate_statistics 측정 선행)
5) P2-5, P2-6     — OG·favicon. 링크 공유 전 필수
6) P2 나머지
7) P3
```

> P2-8을 2순위로 올린 이유: 폰트/자간 토큰이 헤딩·라벨 전반에 걸쳐 있어, 나중에 하면 P2-1·P2-4 등에서 새로 쓴 CSS를 다시 손봐야 한다.

# 검수 체크리스트

- [ ] 라이트/다크 양쪽에서 전체 섹션 확인
- [ ] `grep -c "font-display\|Syne" index.html` → 0건
- [ ] 모든 h3가 같은 서체로 보임 (Stack "Backend" vs Certificates "정보처리기사")
- [ ] hero lead 문장에 "목표로", "관심이 많습니다" 등 지망형 표현이 남아있지 않음
- [ ] 다크 설정 상태로 새로고침 시 흰 화면 번쩍임 없음
- [ ] 네비 링크 클릭 시 섹션 제목이 헤더에 가리지 않음
- [ ] 360px 폭에서 가로 스크롤 발생하지 않음
- [ ] 키보드 Tab만으로 모든 인터랙티브 요소 도달, 포커스 링 보임
- [ ] 이미지·GIF 전부 200 응답 (개발자도구 Network에서 404 0건)
- [ ] `GitHub Repo` 버튼이 실제 ValuePick 레포로 이동
- [ ] 전화번호가 HTML 소스 어디에도 남아있지 않음 (`grep`으로 확인)
- [ ] 카카오톡으로 링크 보냈을 때 미리보기 카드 정상 출력
- [ ] 배포 URL이 `https://jsh340866.github.io/` (레포명 변경 반영), 이력서에 적은 주소와 일치
- [ ] www.valuepick.cloud 접속 정상 (죽어있으면 링크 제거 또는 "데모 준비중" 표기)