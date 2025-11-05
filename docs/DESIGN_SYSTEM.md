# 🎨 디자인 시스템

타우랑가 유학원 웹사이트의 디자인 시스템 가이드입니다.

## 목차
- [컬러 팔레트](#컬러-팔레트)
- [타이포그래피](#타이포그래피)
- [반응형 브레이크포인트](#반응형-브레이크포인트)
- [간격 시스템](#간격-시스템)
- [애니메이션](#애니메이션)
- [컴포넌트 스타일](#컴포넌트-스타일)

## 컬러 팔레트

### 주요 색상 (Primary Colors)

#### Deep Navy - 신뢰감과 전문성
```css
--color-primary: #1B3A6D;
```
- **용도**: 헤더, 푸터, 주요 섹션 배경
- **의미**: 신뢰할 수 있는 교육 기관의 이미지
- **사용 예시**: 네비게이션 바, 타임라인 배경, 버튼

#### Royal Blue - 전문성
```css
--color-secondary: #2E5090;
```
- **용도**: 보조 배경, 호버 상태
- **의미**: 전문적이고 체계적인 서비스
- **사용 예시**: 카드 배경, 링크 호버

### 강조 색상 (Accent Colors)

#### Teal - 현대적이고 친근한
```css
--color-accent: #4FBDBA;
```
- **용도**: CTA 버튼, 아이콘, 강조 요소
- **의미**: 친근하고 접근하기 쉬운 유학원
- **사용 예시**: Primary 버튼, 체크마크, 링크

#### Soft Gold - 프리미엄 품질
```css
--color-gold: #D4AF37;
```
- **용도**: 특별한 배지, 하이라이트
- **의미**: 20년 경력의 프리미엄 서비스
- **사용 예시**: "실제 후기" 배지, 스크롤 인디케이터

### 중성 색상 (Neutral Colors)

#### 배경 및 텍스트 색상
```css
--color-white: #FFFFFF;           /* 주 배경 */
--color-light-gray: #F7F9FC;      /* 보조 배경 */
--color-medium-gray: #6B7280;     /* 보조 텍스트 */
--color-dark-gray: #1F2937;       /* 주 텍스트 */
```

### 색상 사용 가이드

#### 텍스트 색상
- **헤딩 (H1-H6)**: `--color-dark-gray` 또는 `--color-primary`
- **본문 텍스트**: `--color-dark-gray`
- **보조 텍스트**: `--color-medium-gray`
- **반전 텍스트** (어두운 배경): `--color-white`

#### 버튼 색상
- **Primary CTA**: `--color-accent` 배경 + `--color-white` 텍스트
- **Secondary CTA**: `transparent` 배경 + `--color-accent` 테두리
- **호버 상태**: 밝기 조정 (brightness, opacity)

#### 배경 색상
- **섹션 교차**: `--color-white`와 `--color-light-gray` 번갈아 사용
- **강조 섹션**: `--color-primary` (예: 교육 환경, 연혁)
- **카드**: `--color-white` + box-shadow

### 색상 접근성

#### 대비율 (WCAG 2.1 기준)

✅ **AA 등급 이상 조합**
- `#1B3A6D` (Deep Navy) + `#FFFFFF` (White) - 대비율: 10.5:1
- `#1F2937` (Dark Gray) + `#FFFFFF` (White) - 대비율: 14.8:1
- `#4FBDBA` (Teal) + `#FFFFFF` (White) - 대비율: 3.2:1

⚠️ **주의 필요**
- `#D4AF37` (Gold) + `#FFFFFF` (White) - 작은 텍스트에는 사용 자제

---

## 타이포그래피

### 폰트 패밀리

#### 본문 폰트
```css
font-family: 'Pretendard', -apple-system, BlinkMacSystemFont,
             'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
```

**Pretendard 특징:**
- 한글 최적화 폰트
- 다양한 굵기 지원 (100-900)
- 뛰어난 가독성
- 무료 라이선스 (SIL OFL)

#### 영문 강조 폰트
```css
font-family: 'Inter', sans-serif;
```

**Inter 특징:**
- 모던한 산세리프
- 숫자 가독성 우수
- 웹 최적화
- Weights: 400 (Regular), 600 (Semi-bold), 700 (Bold)

### 폰트 크기 (Font Sizes)

#### Desktop (1200px+)
```css
/* Headings */
--font-size-h1: 56px;      /* Hero 타이틀 */
--font-size-h2: 48px;      /* 섹션 타이틀 */
--font-size-h3: 36px;      /* 서브섹션 타이틀 */
--font-size-h4: 24px;      /* 카드 타이틀 */
--font-size-h5: 20px;      /* 소제목 */

/* Body */
--font-size-body-large: 20px;   /* 리드 문단 */
--font-size-body: 16px;         /* 기본 본문 */
--font-size-small: 14px;        /* 캡션, 보조 텍스트 */
```

#### Tablet (768px - 1199px)
```css
--font-size-h1: 48px;
--font-size-h2: 40px;
--font-size-h3: 32px;
--font-size-h4: 22px;
--font-size-body-large: 18px;
--font-size-body: 15px;
```

#### Mobile (< 768px)
```css
--font-size-h1: 36px;
--font-size-h2: 32px;
--font-size-h3: 24px;
--font-size-h4: 20px;
--font-size-body-large: 17px;
--font-size-body: 15px;
```

### 폰트 굵기 (Font Weights)

```css
--font-weight-regular: 400;    /* 본문 */
--font-weight-semibold: 600;   /* 소제목, 강조 */
--font-weight-bold: 700;       /* 헤딩 */
```

### 행간 (Line Height)

```css
--line-height-tight: 1.2;      /* 헤딩 */
--line-height-normal: 1.5;     /* 기본 */
--line-height-relaxed: 1.7;    /* 본문, 가독성 중시 */
```

### 자간 (Letter Spacing)

```css
--letter-spacing-tight: -0.02em;   /* 큰 헤딩 */
--letter-spacing-normal: 0;        /* 기본 */
--letter-spacing-wide: 0.05em;     /* 버튼, 레이블 */
```

### 타이포그래피 사용 예시

#### Hero 타이틀
```css
.hero-title {
  font-size: 56px;
  font-weight: 700;
  line-height: 1.2;
  letter-spacing: -0.02em;
  color: var(--color-white);
}
```

#### 섹션 타이틀
```css
.section-title {
  font-size: 48px;
  font-weight: 700;
  line-height: 1.2;
  color: var(--color-primary);
  margin-bottom: 24px;
}
```

#### 본문
```css
.body-text {
  font-size: 16px;
  font-weight: 400;
  line-height: 1.7;
  color: var(--color-dark-gray);
}
```

---

## 반응형 브레이크포인트

### 브레이크포인트 정의

```css
/* Desktop First 접근 방식 */
@media (max-width: 1199px) { /* Tablet */ }
@media (max-width: 767px)  { /* Mobile */ }
```

### Desktop (1200px 이상)

**레이아웃:**
- 최대 너비: 1200px (컨테이너)
- 3단 그리드 (카드, 특징)
- 2단 레이아웃 (이미지 + 텍스트)
- 전체 네비게이션 표시

**간격:**
- 섹션 패딩: 80px - 120px
- 카드 간격: 40px
- 요소 간격: 24px

### Tablet (768px - 1199px)

**레이아웃:**
- 최대 너비: 100% (좌우 패딩 40px)
- 2단 그리드 또는 단일 컬럼
- 축소된 간격

**조정사항:**
```css
@media (max-width: 1199px) {
  /* 폰트 크기 축소 */
  .section-title { font-size: 40px; }

  /* 간격 축소 */
  section { padding: 60px 40px; }

  /* 그리드 조정 */
  .grid-3 { grid-template-columns: repeat(2, 1fr); }
}
```

### Mobile (768px 미만)

**레이아웃:**
- 전체 너비 (좌우 패딩 24px)
- 단일 컬럼 레이아웃
- 햄버거 메뉴
- 스택형 구조

**조정사항:**
```css
@media (max-width: 767px) {
  /* 폰트 크기 축소 */
  .hero-title { font-size: 36px; }
  .section-title { font-size: 32px; }

  /* 간격 축소 */
  section { padding: 40px 24px; }

  /* 그리드 단일 컬럼 */
  .grid-3, .grid-2 { grid-template-columns: 1fr; }

  /* 모바일 메뉴 */
  .nav-menu { display: none; }
  .mobile-menu-btn { display: block; }
}
```

### 반응형 이미지

```css
/* 기본 반응형 */
img {
  max-width: 100%;
  height: auto;
}

/* 컨테이너에 맞춤 */
.gallery-image {
  width: 100%;
  height: 300px;
  object-fit: cover;
}

/* 모바일에서 높이 조정 */
@media (max-width: 767px) {
  .gallery-image {
    height: 200px;
  }
}
```

---

## 간격 시스템

### Spacing Scale

```css
--spacing-xs: 8px;
--spacing-sm: 16px;
--spacing-md: 24px;
--spacing-lg: 40px;
--spacing-xl: 60px;
--spacing-xxl: 80px;
--spacing-xxxl: 120px;
```

### 사용 가이드

#### 섹션 패딩
- Desktop: `80px - 120px` (상하)
- Tablet: `60px` (상하)
- Mobile: `40px` (상하)

#### 카드 간격
- Desktop: `40px` (gap)
- Tablet: `32px` (gap)
- Mobile: `24px` (gap)

#### 요소 간격
- 제목 ↔ 본문: `24px`
- 본문 문단: `16px`
- 버튼 ↔ 텍스트: `24px`

---

## 애니메이션

### AOS (Animate On Scroll) 설정

```javascript
AOS.init({
  duration: 800,      // 애니메이션 지속시간
  offset: 100,        // 트리거 오프셋
  easing: 'ease',     // Easing 함수
  once: true,         // 한 번만 실행
});
```

### 사용 가능한 애니메이션

#### Fade 애니메이션
```html
<div data-aos="fade-up">위로 페이드인</div>
<div data-aos="fade-down">아래로 페이드인</div>
<div data-aos="fade-left">왼쪽으로 페이드인</div>
<div data-aos="fade-right">오른쪽으로 페이드인</div>
```

#### Zoom 애니메이션
```html
<div data-aos="zoom-in">줌인</div>
<div data-aos="zoom-out">줌아웃</div>
```

#### Flip 애니메이션
```html
<div data-aos="flip-left">왼쪽 플립</div>
<div data-aos="flip-right">오른쪽 플립</div>
```

### 커스텀 애니메이션

#### Fade In Up
```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in-up {
  animation: fadeInUp 0.6s ease-out;
}
```

#### Bounce
```css
@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.bounce {
  animation: bounce 2s infinite;
}
```

### 호버 애니메이션

#### 카드 호버
```css
.card {
  transition: all 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}
```

#### 버튼 호버
```css
.btn {
  transition: all 0.3s ease;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(79, 189, 186, 0.3);
}
```

---

## 컴포넌트 스타일

### 버튼 (Buttons)

#### Primary Button
```css
.btn-primary {
  background: var(--color-accent);
  color: var(--color-white);
  padding: 16px 32px;
  border-radius: 8px;
  font-weight: 600;
  font-size: 16px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(79, 189, 186, 0.3);
}
```

#### Secondary Button
```css
.btn-secondary {
  background: transparent;
  color: var(--color-accent);
  padding: 16px 32px;
  border: 2px solid var(--color-accent);
  border-radius: 8px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-secondary:hover {
  background: var(--color-accent);
  color: var(--color-white);
}
```

### 카드 (Cards)

```css
.card {
  background: var(--color-white);
  padding: 32px;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}
```

### 네비게이션

```css
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background: var(--color-white);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  padding: 20px 0;
  transition: all 0.3s ease;
  z-index: 1000;
}

.navbar.scrolled {
  padding: 12px 0;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}
```

### 섹션 스타일

```css
section {
  padding: 80px 0;
}

section:nth-child(even) {
  background: var(--color-light-gray);
}

section:nth-child(odd) {
  background: var(--color-white);
}
```

---

## 아이콘 시스템

### 아이콘 크기
- **Small**: 16px
- **Medium**: 24px
- **Large**: 32px
- **XLarge**: 48px

### 아이콘 색상
- **Primary**: `var(--color-accent)`
- **Secondary**: `var(--color-medium-gray)`
- **Success**: `#10B981` (체크마크)
- **Warning**: `#F59E0B`

---

## 그림자 (Shadows)

```css
/* 카드 기본 */
--shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.05);

/* 카드 호버 */
--shadow-md: 0 4px 20px rgba(0, 0, 0, 0.08);

/* 강조 요소 */
--shadow-lg: 0 10px 30px rgba(0, 0, 0, 0.12);

/* 모달, 팝업 */
--shadow-xl: 0 20px 50px rgba(0, 0, 0, 0.2);
```

---

## 테두리 반경 (Border Radius)

```css
--radius-sm: 4px;      /* 작은 요소 */
--radius-md: 8px;      /* 버튼, 입력 필드 */
--radius-lg: 16px;     /* 카드 */
--radius-xl: 24px;     /* 큰 카드, 섹션 */
--radius-full: 9999px; /* 원형 버튼, 배지 */
```

---

이 디자인 시스템을 일관되게 적용하여 사용자에게 통일된 경험을 제공합니다.
