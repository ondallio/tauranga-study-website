# ⚡ 성능 최적화 가이드

타우랑가 유학원 웹사이트의 성능 최적화 가이드입니다.

## 목차
- [현재 성능 현황](#현재-성능-현황)
- [이미지 최적화](#이미지-최적화)
- [코드 최적화](#코드-최적화)
- [로딩 성능 개선](#로딩-성능-개선)
- [캐싱 전략](#캐싱-전략)
- [번들 크기 최적화](#번들-크기-최적화)
- [렌더링 성능](#렌더링-성능)
- [모니터링 및 측정](#모니터링-및-측정)

---

## 현재 성능 현황

### 파일 크기 분석

```
📦 프로젝트 총 크기: 227 KB
├── 📄 index.html: 54.5 KB
│   ├── HTML 구조: ~8 KB
│   ├── CSS (embedded): ~15 KB
│   ├── JavaScript (embedded): ~5 KB
│   └── 콘텐츠 (텍스트): ~26.5 KB
├── 🌐 외부 리소스:
│   ├── Pretendard 폰트 (CDN): ~150 KB
│   ├── Inter 폰트 (Google Fonts): ~20 KB
│   ├── AOS 라이브러리 (CDN): ~10 KB
│   └── Unsplash 이미지: ~2-3 MB (총합)
```

### 현재 로딩 시간 (예상)

**빠른 3G 네트워크 기준:**
- HTML 파일: ~1초
- 폰트 파일: ~2-3초
- 이미지 (병렬 로딩): ~5-8초
- **총 First Contentful Paint (FCP)**: ~2-3초
- **총 완전 로딩**: ~8-10초

### 개선 목표

| 지표 | 현재 | 목표 | 우선순위 |
|------|------|------|----------|
| HTML 크기 | 54.5 KB | 40 KB | 중간 |
| 이미지 총 크기 | ~3 MB | 500 KB | 높음 |
| FCP | 2-3s | <1.5s | 높음 |
| LCP | 5-8s | <2.5s | 높음 |
| TTI | 8-10s | <3.5s | 중간 |

---

## 이미지 최적화

### 1. 이미지 로컬화 및 압축

#### 문제점
- 현재 Unsplash에서 직접 로딩 (외부 의존성)
- 원본 크기 이미지 사용 (불필요하게 큰 파일)
- 캐싱 불가능

#### 해결 방법

**Step 1: 이미지 다운로드 및 저장**
```bash
# assets 폴더 생성
mkdir -p assets/images/{hero,gallery,education,testimonials,tauranga}

# 이미지 다운로드 (예시)
wget -O assets/images/hero/main.jpg "https://unsplash.com/..."
```

**Step 2: 이미지 압축**

옵션 A - ImageOptim / TinyPNG 사용 (GUI)
```
1. https://tinypng.com 접속
2. 이미지 업로드
3. 압축된 파일 다운로드
```

옵션 B - CLI 도구 사용
```bash
# npm 설치
npm install -g imagemin-cli imagemin-mozjpeg imagemin-pngquant

# JPEG 압축 (품질 80%)
imagemin assets/images/*.jpg --plugin=mozjpeg --plugin.quality=80 > compressed/

# PNG 압축
imagemin assets/images/*.png --plugin=pngquant > compressed/
```

**Step 3: WebP 포맷 변환**
```bash
# cwebp 설치 (Ubuntu/Debian)
sudo apt-get install webp

# 변환
cwebp -q 80 input.jpg -o output.webp

# 배치 변환
for img in assets/images/**/*.jpg; do
  cwebp -q 80 "$img" -o "${img%.jpg}.webp"
done
```

**Step 4: HTML에서 사용**
```html
<picture>
  <source srcset="assets/images/hero/main.webp" type="image/webp">
  <source srcset="assets/images/hero/main.jpg" type="image/jpeg">
  <img src="assets/images/hero/main.jpg" alt="타우랑가 해변" loading="lazy">
</picture>
```

### 2. 반응형 이미지

#### srcset 사용
```html
<img
  src="assets/images/hero/main-800.jpg"
  srcset="
    assets/images/hero/main-400.jpg 400w,
    assets/images/hero/main-800.jpg 800w,
    assets/images/hero/main-1200.jpg 1200w,
    assets/images/hero/main-1600.jpg 1600w
  "
  sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 1200px"
  alt="타우랑가 해변"
  loading="lazy"
>
```

#### 이미지 크기별 생성 스크립트
```bash
#!/bin/bash
# generate-responsive-images.sh

INPUT_DIR="assets/images/original"
OUTPUT_DIR="assets/images"
SIZES=(400 800 1200 1600)

for img in $INPUT_DIR/*.jpg; do
  filename=$(basename "$img" .jpg)

  for size in "${SIZES[@]}"; do
    convert "$img" -resize ${size}x -quality 80 \
      "$OUTPUT_DIR/${filename}-${size}.jpg"

    cwebp -q 80 "$OUTPUT_DIR/${filename}-${size}.jpg" \
      -o "$OUTPUT_DIR/${filename}-${size}.webp"
  done
done
```

### 3. Lazy Loading

#### Native Lazy Loading
```html
<img src="image.jpg" loading="lazy" alt="설명">
```

#### Intersection Observer (더 많은 제어)
```javascript
const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;
      img.classList.add('loaded');
      observer.unobserve(img);
    }
  });
});

document.querySelectorAll('img[data-src]').forEach(img => {
  imageObserver.observe(img);
});
```

```html
<img data-src="actual-image.jpg" src="placeholder.jpg" alt="설명">
```

### 4. Placeholder 전략

#### Blur Placeholder
```css
.img-wrapper {
  position: relative;
  overflow: hidden;
}

.img-placeholder {
  position: absolute;
  filter: blur(20px);
  transform: scale(1.1);
}

.img-actual {
  opacity: 0;
  transition: opacity 0.3s;
}

.img-actual.loaded {
  opacity: 1;
}
```

#### LQIP (Low Quality Image Placeholder)
```html
<div class="img-wrapper">
  <img src="tiny-10kb-blur.jpg" class="img-placeholder">
  <img data-src="full-image.jpg" class="img-actual" loading="lazy">
</div>
```

---

## 코드 최적화

### 1. CSS/JS 분리

#### 현재 구조 (단일 파일)
```html
<!-- index.html -->
<style>/* 15 KB CSS */</style>
<script>/* 5 KB JavaScript */</script>
```

#### 개선 구조 (파일 분리)
```
project/
├── index.html (8 KB)
├── css/
│   ├── styles.min.css (12 KB - 압축됨)
│   └── critical.css (2 KB - 인라인용)
└── js/
    └── main.min.js (4 KB - 압축됨)
```

**index.html**
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <!-- Critical CSS 인라인 -->
  <style>
    /* 첫 화면에 필요한 최소 CSS (2 KB) */
  </style>

  <!-- 나머지 CSS는 비동기 로드 -->
  <link rel="preload" href="css/styles.min.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="css/styles.min.css"></noscript>
</head>
<body>
  <!-- 콘텐츠 -->

  <!-- JavaScript는 defer로 로드 -->
  <script src="js/main.min.js" defer></script>
</body>
</html>
```

### 2. CSS 최적화

#### CSS 압축
```bash
# npm 설치
npm install -g cssnano postcss-cli

# 압축
postcss styles.css --use cssnano -o styles.min.css
```

#### 사용하지 않는 CSS 제거
```bash
# PurgeCSS 사용
npm install -g purgecss

purgecss --css styles.css --content index.html --output purged.css
```

#### Critical CSS 추출
```bash
# Critical 도구 사용
npm install -g critical

critical index.html --base ./ --inline --minify > index-critical.html
```

### 3. JavaScript 최적화

#### 압축 (Minification)
```bash
# Terser 사용
npm install -g terser

terser main.js -c -m -o main.min.js
```

#### 불필요한 코드 제거
- `console.log()` 제거
- 사용하지 않는 함수 제거
- 주석 제거

### 4. 폰트 최적화

#### 필요한 글리프만 로드
```html
<!-- Google Fonts - 필요한 weight만 -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
```

#### 폰트 로컬 호스팅
```css
@font-face {
  font-family: 'Pretendard';
  src: url('/fonts/Pretendard-Regular.woff2') format('woff2'),
       url('/fonts/Pretendard-Regular.woff') format('woff');
  font-weight: 400;
  font-display: swap; /* FOIT 방지 */
}
```

#### font-display 전략
```css
/* 권장: swap - FOUT 허용하지만 빠른 렌더링 */
font-display: swap;

/* 대안: fallback - 100ms 블록, 3초 스왑 */
font-display: fallback;
```

---

## 로딩 성능 개선

### 1. Resource Hints

```html
<head>
  <!-- DNS Prefetch - 외부 도메인 미리 해석 -->
  <link rel="dns-prefetch" href="//fonts.googleapis.com">
  <link rel="dns-prefetch" href="//unpkg.com">

  <!-- Preconnect - 중요한 외부 리소스 -->
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

  <!-- Preload - 곧 필요한 리소스 -->
  <link rel="preload" href="/fonts/Pretendard.woff2" as="font" type="font/woff2" crossorigin>
  <link rel="preload" href="/images/hero-bg.webp" as="image">

  <!-- Prefetch - 다음 페이지에서 필요할 리소스 -->
  <link rel="prefetch" href="/images/gallery-1.jpg">
</head>
```

### 2. 스크립트 로딩 전략

```html
<!-- 파싱 블로킹 (사용 지양) -->
<script src="script.js"></script>

<!-- Async - 다운로드 후 즉시 실행 (순서 보장 X) -->
<script src="analytics.js" async></script>

<!-- Defer - HTML 파싱 완료 후 실행 (순서 보장) ✅ 권장 -->
<script src="main.js" defer></script>

<!-- Module - 자동 defer -->
<script type="module" src="app.js"></script>
```

### 3. 외부 라이브러리 최적화

#### AOS 라이브러리 - 조건부 로드
```javascript
// 모바일에서는 애니메이션 비활성화
if (window.innerWidth > 768) {
  // AOS 라이브러리 로드
  const script = document.createElement('script');
  script.src = 'https://unpkg.com/aos@2.3.1/dist/aos.js';
  script.onload = () => {
    AOS.init({ duration: 800, offset: 100, once: true });
  };
  document.body.appendChild(script);
}
```

---

## 캐싱 전략

### 1. HTTP 캐싱 헤더

**`.htaccess` (Apache)**
```apache
<IfModule mod_expires.c>
  ExpiresActive On

  # HTML - 짧은 캐싱
  ExpiresByType text/html "access plus 1 hour"

  # CSS/JS - 1년 캐싱 (파일명에 해시 사용 시)
  ExpiresByType text/css "access plus 1 year"
  ExpiresByType application/javascript "access plus 1 year"

  # 이미지 - 1개월 캐싱
  ExpiresByType image/jpeg "access plus 1 month"
  ExpiresByType image/png "access plus 1 month"
  ExpiresByType image/webp "access plus 1 month"

  # 폰트 - 1년 캐싱
  ExpiresByType font/woff2 "access plus 1 year"
</IfModule>

# Gzip 압축
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/css application/javascript
</IfModule>
```

**Nginx**
```nginx
location ~* \.(css|js)$ {
  expires 1y;
  add_header Cache-Control "public, immutable";
}

location ~* \.(jpg|jpeg|png|webp|svg)$ {
  expires 1M;
  add_header Cache-Control "public";
}

location ~* \.(woff2|woff|ttf)$ {
  expires 1y;
  add_header Cache-Control "public, immutable";
}

# Gzip 압축
gzip on;
gzip_types text/css application/javascript image/svg+xml;
gzip_min_length 1000;
```

### 2. Service Worker 캐싱

```javascript
// sw.js
const CACHE_NAME = 'tauranga-v1';
const urlsToCache = [
  '/',
  '/css/styles.min.css',
  '/js/main.min.js',
  '/fonts/Pretendard.woff2',
  '/images/logo.svg'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(urlsToCache))
  );
});

self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => response || fetch(event.request))
  );
});
```

---

## 번들 크기 최적화

### 1. 빌드 도구 도입

#### Vite 설정 (권장)
```bash
npm init vite@latest
npm install
```

**vite.config.js**
```javascript
import { defineConfig } from 'vite';

export default defineConfig({
  build: {
    minify: 'terser',
    terserOptions: {
      compress: {
        drop_console: true, // console.log 제거
      }
    },
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['aos'], // 벤더 청크 분리
        }
      }
    }
  }
});
```

### 2. Tree Shaking

```javascript
// ❌ 나쁜 예 - 전체 라이브러리 import
import _ from 'lodash';

// ✅ 좋은 예 - 필요한 것만 import
import debounce from 'lodash/debounce';
```

---

## 렌더링 성능

### 1. JavaScript 실행 최적화

#### Debounce 스크롤 이벤트
```javascript
// 기존 (성능 낮음)
window.addEventListener('scroll', () => {
  updateProgressBar();
});

// 개선 (debounce)
const debounce = (func, wait) => {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), wait);
  };
};

window.addEventListener('scroll', debounce(() => {
  updateProgressBar();
}, 10));
```

#### RequestAnimationFrame 사용
```javascript
let ticking = false;

window.addEventListener('scroll', () => {
  if (!ticking) {
    window.requestAnimationFrame(() => {
      updateProgressBar();
      ticking = false;
    });
    ticking = true;
  }
});
```

### 2. DOM 조작 최적화

```javascript
// ❌ 나쁜 예 - 여러 번 DOM 접근
for (let i = 0; i < 100; i++) {
  document.getElementById('list').innerHTML += '<li>Item</li>';
}

// ✅ 좋은 예 - 한 번에 DOM 업데이트
const fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
  const li = document.createElement('li');
  li.textContent = 'Item';
  fragment.appendChild(li);
}
document.getElementById('list').appendChild(fragment);
```

### 3. CSS 성능

```css
/* ❌ 나쁜 예 - 복잡한 선택자 */
div > ul > li > a:hover {
  color: red;
}

/* ✅ 좋은 예 - 클래스 사용 */
.nav-link:hover {
  color: red;
}

/* will-change로 레이어 분리 (애니메이션 요소만) */
.animated-element {
  will-change: transform;
}
```

---

## 모니터링 및 측정

### 1. Lighthouse 측정

```bash
# Chrome DevTools
1. F12 → Lighthouse 탭
2. "Generate report" 클릭

# CLI
npm install -g lighthouse
lighthouse https://your-site.com --view
```

### 2. Web Vitals 측정

```javascript
// web-vitals 라이브러리 사용
import {getCLS, getFID, getFCP, getLCP, getTTFB} from 'web-vitals';

getCLS(console.log);
getFID(console.log);
getFCP(console.log);
getLCP(console.log);
getTTFB(console.log);
```

### 3. Performance API

```javascript
// 페이지 로딩 시간
window.addEventListener('load', () => {
  const perfData = window.performance.timing;
  const pageLoadTime = perfData.loadEventEnd - perfData.navigationStart;
  console.log(`Page load time: ${pageLoadTime}ms`);
});

// 리소스 타이밍
const resources = performance.getEntriesByType('resource');
resources.forEach(resource => {
  console.log(`${resource.name}: ${resource.duration}ms`);
});
```

---

## 성능 체크리스트

### 이미지
- [ ] WebP 포맷 사용
- [ ] 반응형 이미지 (srcset)
- [ ] Lazy loading 적용
- [ ] 압축 최적화 (80% 품질)
- [ ] 적절한 크기 사용

### 코드
- [ ] CSS/JS 파일 분리
- [ ] 압축 (minification)
- [ ] Critical CSS 인라인
- [ ] 불필요한 코드 제거
- [ ] Tree shaking 적용

### 폰트
- [ ] 필요한 weight만 로드
- [ ] font-display: swap 사용
- [ ] WOFF2 포맷 사용
- [ ] 폰트 서브셋팅

### 로딩
- [ ] DNS Prefetch 설정
- [ ] Preload 중요 리소스
- [ ] Defer 스크립트
- [ ] 조건부 로딩

### 캐싱
- [ ] HTTP 캐시 헤더 설정
- [ ] Gzip/Brotli 압축
- [ ] Service Worker (선택)
- [ ] CDN 사용 고려

### 렌더링
- [ ] Debounce 스크롤 이벤트
- [ ] RequestAnimationFrame 사용
- [ ] DOM 조작 최적화
- [ ] CSS 선택자 단순화

---

이 가이드를 단계적으로 적용하여 웹사이트 성능을 크게 향상시킬 수 있습니다.
