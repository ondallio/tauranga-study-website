# 🧪 테스트 가이드

타우랑가 유학원 웹사이트의 테스트 가이드입니다.

## 목차
- [브라우저 호환성 테스트](#브라우저-호환성-테스트)
- [반응형 디자인 테스트](#반응형-디자인-테스트)
- [접근성 테스트](#접근성-테스트)
- [성능 테스트](#성능-테스트)
- [기능 테스트](#기능-테스트)
- [크로스 브라우저 테스트 자동화](#크로스-브라우저-테스트-자동화)
- [사용자 시나리오 테스트](#사용자-시나리오-테스트)
- [테스트 체크리스트](#테스트-체크리스트)

---

## 브라우저 호환성 테스트

### 지원 브라우저

#### Desktop

| 브라우저 | 최소 버전 | 테스트 상태 | 비고 |
|---------|----------|------------|------|
| Chrome | 90+ | ✅ 통과 | 주 타겟 브라우저 |
| Firefox | 88+ | ✅ 통과 | Grid/Flexbox 완벽 지원 |
| Safari | 14+ | ✅ 통과 | webkit prefix 필요 시 추가 |
| Edge | 90+ | ✅ 통과 | Chromium 기반 |
| Opera | 76+ | ⚠️ 미확인 | Chromium 기반으로 호환 예상 |

#### Mobile

| 브라우저 | 최소 버전 | 테스트 상태 | 비고 |
|---------|----------|------------|------|
| iOS Safari | 14+ | ✅ 통과 | iPhone 6s 이상 |
| Chrome (Android) | 90+ | ✅ 통과 | 안드로이드 7.0+ |
| Samsung Internet | 14+ | ✅ 통과 | 한국 사용자 多 |
| Firefox (Android) | 88+ | ⚠️ 미확인 | - |

### 테스트 방법

#### 1. 실제 기기 테스트

**Desktop**
```
1. Windows 10 + Chrome 최신
2. macOS + Safari 최신
3. Ubuntu + Firefox 최신
```

**Mobile**
```
1. iPhone 12/13/14 (iOS 15+)
2. Samsung Galaxy S21/S22 (Android 11+)
3. 중저가 안드로이드 기기 (성능 테스트)
```

#### 2. 브라우저 개발자 도구

**Chrome DevTools**
```
1. F12 → Device Toolbar (Ctrl+Shift+M)
2. 다양한 기기 프로필 선택
3. Network throttling으로 느린 네트워크 시뮬레이션
```

**Firefox Responsive Design Mode**
```
1. F12 → Responsive Design Mode (Ctrl+Shift+M)
2. Touch simulation 활성화
```

#### 3. 온라인 테스트 도구

**BrowserStack**
```
1. https://www.browserstack.com 접속
2. Live → 기기/브라우저 선택
3. URL 입력하여 테스트
```

**LambdaTest**
```
1. https://www.lambdatest.com 접속
2. Real Time Testing 선택
3. 브라우저/OS 조합 선택
```

### 브라우저별 주의사항

#### Safari
```css
/* Backdrop filter Safari 지원 */
.element {
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
}

/* Smooth scrolling Safari */
html {
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
}
```

#### Internet Explorer 11 (선택적 지원)
```html
<!-- IE 11 미지원 안내 -->
<!--[if IE]>
  <div class="ie-warning">
    이 웹사이트는 Internet Explorer를 지원하지 않습니다.
    Chrome, Firefox, Edge를 사용해주세요.
  </div>
<![endif]-->
```

---

## 반응형 디자인 테스트

### 테스트 브레이크포인트

| 기기 유형 | 너비 | 테스트 기기 예시 |
|----------|------|-----------------|
| Mobile (Small) | 320px - 375px | iPhone SE, Galaxy S8 |
| Mobile (Medium) | 376px - 414px | iPhone 12/13/14, Galaxy S21 |
| Mobile (Large) | 415px - 767px | iPhone Pro Max, 큰 안드로이드 |
| Tablet (Portrait) | 768px - 1024px | iPad, Galaxy Tab |
| Tablet (Landscape) | 1025px - 1199px | iPad Pro |
| Desktop (Small) | 1200px - 1439px | 13" 노트북 |
| Desktop (Medium) | 1440px - 1919px | 15" 노트북, 일반 모니터 |
| Desktop (Large) | 1920px+ | FHD 모니터, 큰 화면 |

### 테스트 시나리오

#### 1. 레이아웃 테스트

**Mobile (375px)**
```
✅ 체크사항:
□ 단일 컬럼 레이아웃
□ 햄버거 메뉴 표시
□ 텍스트 읽기 가능 (최소 15px)
□ 버튼 터치 가능 (최소 44x44px)
□ 이미지가 화면에 맞게 조정됨
□ 가로 스크롤 없음
```

**Tablet (768px)**
```
✅ 체크사항:
□ 2단 그리드 또는 단일 컬럼
□ 네비게이션 메뉴 표시 또는 햄버거
□ 적절한 간격 유지
□ 이미지 크기 조정
```

**Desktop (1920px)**
```
✅ 체크사항:
□ 3단 그리드
□ 전체 네비게이션 표시
□ 최대 너비 제한 (1200px)
□ 중앙 정렬
□ 여백 적절
```

#### 2. 특정 섹션 테스트

**히어로 섹션**
```
Mobile:
□ 배경 이미지 위치 조정 (background-position)
□ 제목 크기 조정 (36px)
□ 버튼 세로 배치

Desktop:
□ 전체 화면 배경
□ 큰 제목 (56px)
□ 버튼 가로 배치
```

**카드 그리드**
```
Mobile: 1열
Tablet: 2열
Desktop: 3열

□ 카드 간격 일정
□ 호버 효과 작동 (desktop)
□ 터치 효과 작동 (mobile)
```

### Chrome DevTools 반응형 테스트

```
1. F12 → Device Toolbar 활성화
2. "Responsive" 선택
3. 너비를 320px부터 1920px까지 천천히 조정
4. 브레이크포인트에서 레이아웃 변경 확인
5. "Show media queries" 클릭하여 브레이크포인트 시각화
```

### 회전 테스트 (Orientation)

```
□ 세로 모드 (Portrait) 테스트
□ 가로 모드 (Landscape) 테스트
□ 회전 시 레이아웃 적절히 조정
□ 가로 모드에서 높이 부족 문제 없음
```

---

## 접근성 테스트

### WCAG 2.1 준수

#### Level A (최소 기준)

**1.1 텍스트 대안**
```html
✅ 모든 이미지에 alt 속성
<img src="hero.jpg" alt="타우랑가 해변과 학생들">

✅ 장식용 이미지는 빈 alt
<img src="decoration.png" alt="">

✅ 아이콘 버튼에 aria-label
<button aria-label="메뉴 열기">☰</button>
```

**1.3 적응 가능**
```html
✅ 시맨틱 HTML 사용
<nav>, <main>, <article>, <section>, <footer>

✅ 적절한 헤딩 계층
<h1> → <h2> → <h3> (건너뛰지 않음)
```

**2.1 키보드 접근성**
```
✅ 체크사항:
□ Tab 키로 모든 인터랙티브 요소 접근 가능
□ Enter/Space로 버튼 활성화
□ Esc로 모달 닫기
□ 포커스 표시 (outline) 유지
```

#### Level AA (권장)

**1.4.3 대비 (최소)**
```
✅ 텍스트 대비율:
□ 일반 텍스트: 4.5:1 이상
□ 큰 텍스트 (18pt+): 3:1 이상

테스트 도구:
- Chrome DevTools → Lighthouse → Accessibility
- WebAIM Contrast Checker
```

**1.4.10 재배치**
```
✅ 체크사항:
□ 200% 확대 시 내용 읽기 가능
□ 가로 스크롤 불필요
□ 텍스트 겹침 없음
```

### 접근성 테스트 도구

#### 1. Lighthouse (Chrome DevTools)

```
1. F12 → Lighthouse 탭
2. "Accessibility" 체크
3. "Generate report" 클릭
4. 점수 및 개선사항 확인

목표: 90점 이상
```

#### 2. WAVE (Web Accessibility Evaluation Tool)

```
1. https://wave.webaim.org 접속
2. URL 입력
3. 에러 및 경고 확인

주요 체크:
□ Errors: 0개
□ Contrast Errors: 0개
□ Alerts: 검토 후 수정
```

#### 3. axe DevTools (브라우저 확장)

```
1. Chrome/Firefox에 axe DevTools 설치
2. F12 → axe DevTools 탭
3. "Scan ALL of my page" 클릭
4. 문제 확인 및 수정
```

#### 4. 스크린 리더 테스트

**NVDA (Windows - 무료)**
```
1. https://www.nvaccess.org 다운로드
2. 설치 후 실행
3. 웹사이트 탐색 테스트

체크사항:
□ 모든 콘텐츠 읽힘
□ 링크 텍스트 의미 있음
□ 이미지 alt 텍스트 적절
□ 폼 레이블 읽힘
```

**VoiceOver (macOS - 내장)**
```
1. Cmd + F5로 VoiceOver 활성화
2. Safari에서 웹사이트 열기
3. Ctrl + Option + 화살표로 탐색

체크사항:
□ 랜드마크 탐색 가능
□ 헤딩 탐색 가능
□ 링크 목록 확인 가능
```

### 키보드 탐색 테스트

```
✅ 테스트 시나리오:
1. Tab: 다음 인터랙티브 요소로 이동
2. Shift + Tab: 이전 요소로 이동
3. Enter: 링크/버튼 활성화
4. Space: 버튼 활성화, 체크박스 토글
5. Esc: 모달/메뉴 닫기
6. Arrow keys: 드롭다운 메뉴 탐색

체크사항:
□ 논리적 탐색 순서
□ 포커스 표시 명확
□ Skip to main content 링크
□ 키보드 트랩 없음
```

### 포커스 관리

```css
/* ❌ 나쁜 예 - 포커스 제거 */
*:focus {
  outline: none;
}

/* ✅ 좋은 예 - 커스텀 포커스 스타일 */
a:focus,
button:focus {
  outline: 2px solid var(--color-accent);
  outline-offset: 2px;
}

/* 마우스 클릭 시만 포커스 숨김 */
*:focus:not(:focus-visible) {
  outline: none;
}

*:focus-visible {
  outline: 2px solid var(--color-accent);
}
```

---

## 성능 테스트

### Google Lighthouse

```
1. Chrome DevTools (F12) → Lighthouse
2. 카테고리 선택:
   ✅ Performance
   ✅ Accessibility
   ✅ Best Practices
   ✅ SEO
3. Device: Mobile & Desktop 모두 테스트
4. "Generate report"

목표 점수:
□ Performance: 90+
□ Accessibility: 90+
□ Best Practices: 90+
□ SEO: 90+
```

### Core Web Vitals

| 지표 | 좋음 | 개선 필요 | 나쁨 |
|------|------|----------|------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | 2.5s - 4s | > 4s |
| FID (First Input Delay) | ≤ 100ms | 100ms - 300ms | > 300ms |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | 0.1 - 0.25 | > 0.25 |

**측정 도구:**
- [PageSpeed Insights](https://pagespeed.web.dev)
- [web.dev/measure](https://web.dev/measure)
- Chrome DevTools → Performance

### 네트워크 속도별 테스트

```
Chrome DevTools → Network 탭 → Throttling

테스트 프로필:
□ Fast 3G (1.6 Mbps down, 750 Kbps up)
□ Slow 3G (500 Kbps down, 500 Kbps up)
□ Offline (오프라인 경험)

체크사항:
□ 3G에서 5초 내 FCP
□ 로딩 스피너 표시
□ 이미지 점진적 로딩
□ 오프라인 메시지 표시
```

### 성능 프로파일링

```
1. Chrome DevTools → Performance 탭
2. 녹화 시작 (Ctrl+E)
3. 페이지 스크롤 및 인터랙션
4. 녹화 중지

분석:
□ Long Tasks (50ms 초과) 확인
□ Layout Shift 확인
□ JavaScript 실행 시간
□ 렌더링 병목 찾기
```

---

## 기능 테스트

### 네비게이션

```
✅ Desktop
□ 로고 클릭 → 홈으로 이동
□ 메뉴 링크 클릭 → 해당 섹션으로 스크롤
□ CTA 버튼 클릭 → 문의 섹션으로 이동
□ 스크롤 시 네비게이션 스타일 변경

✅ Mobile
□ 햄버거 아이콘 클릭 → 메뉴 열림
□ 메뉴 링크 클릭 → 섹션 이동 + 메뉴 닫힘
□ 메뉴 외부 클릭 → 메뉴 닫힘
□ Esc 키 → 메뉴 닫힘
```

### 스크롤 애니메이션

```
✅ AOS 애니메이션
□ 스크롤 시 요소 fade-in
□ 애니메이션은 한 번만 실행 (once: true)
□ 모바일에서도 부드럽게 작동
□ 애니메이션 전 콘텐츠 숨김 없음 (접근성)
```

### 카운터 애니메이션

```
✅ 통계 수치 카운터
□ 해당 섹션 스크롤 시 시작
□ 0부터 최종 값까지 증가
□ 한 번만 실행
□ 리사이즈 시 재실행 안 됨
```

### 폼 (향후 추가 시)

```
✅ 입력 검증
□ 필수 필드 비어있을 때 에러
□ 이메일 형식 검증
□ 전화번호 형식 검증
□ 에러 메시지 명확

✅ 제출
□ 제출 중 로딩 표시
□ 성공 메시지 표시
□ 실패 시 에러 메시지
```

### 외부 링크

```
✅ 체크사항
□ 카카오톡 링크 작동
□ 네이버 카페 링크 작동
□ 전화번호 클릭 → 전화 앱 열림 (모바일)
□ 이메일 클릭 → 이메일 앱 열림
□ Google Maps 링크 작동
□ YouTube 동영상 재생
□ 외부 링크에 rel="noopener" 추가
```

---

## 크로스 브라우저 테스트 자동화

### Playwright (권장)

```bash
# 설치
npm install -D @playwright/test

# 테스트 실행
npx playwright test
```

**tests/navigation.spec.js**
```javascript
const { test, expect } = require('@playwright/test');

test.describe('Navigation', () => {
  test('should navigate to sections on menu click', async ({ page }) => {
    await page.goto('http://localhost:8000');

    // 메뉴 클릭
    await page.click('a[href="#about"]');

    // 섹션으로 스크롤 확인
    const aboutSection = await page.locator('#about');
    await expect(aboutSection).toBeInViewport();
  });

  test('mobile menu should open and close', async ({ page }) => {
    await page.setViewportSize({ width: 375, height: 667 });
    await page.goto('http://localhost:8000');

    // 햄버거 메뉴 클릭
    await page.click('.mobile-menu-btn');

    // 메뉴 열림 확인
    const menu = await page.locator('.nav-menu');
    await expect(menu).toBeVisible();

    // 메뉴 닫기
    await page.click('.mobile-menu-btn');
    await expect(menu).not.toBeVisible();
  });
});
```

### Cypress

```bash
# 설치
npm install -D cypress

# 실행
npx cypress open
```

**cypress/e2e/homepage.cy.js**
```javascript
describe('Homepage', () => {
  beforeEach(() => {
    cy.visit('http://localhost:8000');
  });

  it('should load successfully', () => {
    cy.get('h1').should('be.visible');
  });

  it('should navigate smoothly', () => {
    cy.get('a[href="#programs"]').click();
    cy.get('#programs').should('be.visible');
  });

  it('should display all sections', () => {
    cy.get('section').should('have.length.greaterThan', 5);
  });
});
```

---

## 사용자 시나리오 테스트

### 시나리오 1: 학부모가 유학원 정보 확인

```
1. 사용자가 웹사이트 방문
   □ 히어로 섹션 로딩 (2초 이내)
   □ 제목 및 CTA 버튼 표시

2. 스크롤하여 핵심 가치 확인
   □ 3개 핵심 가치 카드 표시
   □ 아이콘 및 텍스트 읽기 가능

3. 학부모 후기 확인
   □ 3개 후기 카드 표시
   □ 실제 후기 배지 표시

4. 문의 방법 확인
   □ 카카오톡/네이버 카페/전화 링크 작동
   □ 클릭 시 해당 앱/페이지 열림
```

### 시나리오 2: 모바일에서 프로그램 정보 확인

```
1. 모바일 브라우저로 접속 (375px)
   □ 레이아웃 깨지지 않음
   □ 텍스트 읽기 가능

2. 햄버거 메뉴 열기
   □ 메뉴 오버레이 표시
   □ 애니메이션 부드러움

3. "프로그램" 메뉴 클릭
   □ 해당 섹션으로 스크롤
   □ 메뉴 자동 닫힘

4. 프로그램 카드 확인
   □ 단일 컬럼 레이아웃
   □ 모든 카드 표시
```

### 시나리오 3: 동영상 시청

```
1. 동영상 섹션으로 스크롤
   □ YouTube iframe 표시

2. 동영상 재생 버튼 클릭
   □ 동영상 재생
   □ 전체화면 가능
   □ 모바일에서도 작동
```

---

## 테스트 체크리스트

### 출시 전 필수 테스트

#### 기능 (Functionality)
- [ ] 모든 내부 링크 작동
- [ ] 모든 외부 링크 작동
- [ ] 모바일 메뉴 열기/닫기
- [ ] 스크롤 애니메이션 작동
- [ ] 카운터 애니메이션 작동
- [ ] YouTube 동영상 재생
- [ ] 스크롤 진행 바 작동

#### 반응형 (Responsive)
- [ ] Mobile 320px 테스트
- [ ] Mobile 375px 테스트
- [ ] Mobile 414px 테스트
- [ ] Tablet 768px 테스트
- [ ] Tablet 1024px 테스트
- [ ] Desktop 1920px 테스트
- [ ] 가로 스크롤 없음 (모든 화면)

#### 브라우저 (Cross-browser)
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)
- [ ] iOS Safari
- [ ] Chrome Android
- [ ] Samsung Internet

#### 성능 (Performance)
- [ ] Lighthouse Performance 90+
- [ ] LCP < 2.5s
- [ ] FID < 100ms
- [ ] CLS < 0.1
- [ ] 이미지 최적화 확인
- [ ] 3G에서 로딩 테스트

#### 접근성 (Accessibility)
- [ ] Lighthouse Accessibility 90+
- [ ] WAVE 에러 0개
- [ ] 키보드 탐색 가능
- [ ] 스크린 리더 테스트
- [ ] 색상 대비 확인
- [ ] Alt 텍스트 확인

#### SEO
- [ ] Lighthouse SEO 90+
- [ ] 메타 태그 확인
- [ ] Open Graph 태그 확인
- [ ] 시맨틱 HTML 확인
- [ ] robots.txt 확인
- [ ] sitemap.xml 확인

#### 보안 (Security)
- [ ] HTTPS 사용
- [ ] 외부 링크에 rel="noopener"
- [ ] CSP 헤더 설정 (선택)
- [ ] XSS 방지 확인

---

## 버그 리포트 템플릿

```markdown
### 버그 설명
[버그에 대한 간단한 설명]

### 재현 단계
1. [첫 번째 단계]
2. [두 번째 단계]
3. [세 번째 단계]

### 예상 결과
[예상했던 동작]

### 실제 결과
[실제로 발생한 동작]

### 환경
- 브라우저: [Chrome 120]
- OS: [Windows 11]
- 화면 크기: [1920x1080]
- 기기: [Desktop / iPhone 13]

### 스크린샷
[스크린샷 첨부]

### 우선순위
- [ ] Critical (사이트 작동 불가)
- [ ] High (주요 기능 문제)
- [ ] Medium (부분적 문제)
- [ ] Low (사소한 문제)
```

---

체계적인 테스트를 통해 모든 사용자에게 일관된 경험을 제공할 수 있습니다.
