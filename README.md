# 🎓 타우랑가 유학원 웹사이트

뉴질랜드 타우랑가 지역 전문 유학원의 공식 웹사이트입니다. 20년 경력의 전문성을 바탕으로 한국 초·중학생의 뉴질랜드 유학을 전문적으로 지원합니다.

## 📋 프로젝트 개요

타우랑가 유학원은 뉴질랜드 타우랑가 지역의 안전하고 체계적인 유학 서비스를 제공하는 전문 교육 기관입니다. 본 웹사이트는 학부모님들께 유학원의 서비스, 실제 후기, 프로그램 정보를 제공하고, 온라인 상담 신청을 지원합니다.

### 주요 특징
- 📱 **반응형 디자인**: 모바일, 태블릿, 데스크톱 모든 기기 지원
- 🎨 **모던한 UI/UX**: 부드러운 애니메이션과 직관적인 네비게이션
- 🌐 **단일 페이지 구조**: 빠른 로딩과 원활한 사용자 경험
- 📊 **실시간 카운터 애니메이션**: 주요 통계 수치의 시각적 표현
- 🎬 **멀티미디어 콘텐츠**: YouTube 동영상 및 이미지 갤러리

## 🚀 빠른 시작

### 필수 요구사항
- 웹 브라우저 (Chrome, Firefox, Safari, Edge 최신 버전 권장)
- (옵션) 로컬 개발 서버 (Live Server, Python HTTP Server 등)

### 설치 및 실행

#### 1. 프로젝트 클론
```bash
git clone https://github.com/ondallio/tauranga-study-website.git
cd tauranga-study-website
```

#### 2. 로컬에서 실행

**방법 A: 브라우저에서 직접 열기**
```bash
# 프로젝트 폴더에서 index.html 파일을 더블 클릭하거나
open index.html  # macOS
start index.html # Windows
xdg-open index.html # Linux
```

**방법 B: VS Code의 Live Server 사용 (권장)**
1. VS Code에서 프로젝트 폴더 열기
2. "Live Server" 확장 프로그램 설치
3. `index.html` 파일에서 우클릭 → "Open with Live Server"

**방법 C: Python HTTP 서버 사용**
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# 브라우저에서 http://localhost:8000 접속
```

**방법 D: Node.js http-server 사용**
```bash
npx http-server -p 8000
# 브라우저에서 http://localhost:8000 접속
```

## 📁 프로젝트 구조

```
tauranga-study-website/
├── index.html          # 메인 웹페이지 (54.5 KB)
├── README.md           # 프로젝트 문서
├── .gitignore          # Git 제외 파일 목록
└── .git/               # Git 저장소 데이터
```

### 파일 설명
- **index.html**: 전체 웹사이트가 포함된 단일 HTML 파일
  - HTML 구조
  - CSS 스타일 (embedded)
  - JavaScript 로직 (embedded)
  - 모든 콘텐츠 섹션

## 🛠️ 기술 스택

### 프론트엔드 기술

#### HTML5
- 시맨틱 HTML 구조
- Open Graph 메타태그 (소셜 미디어 공유 최적화)
- SEO 최적화된 메타 정보

#### CSS3
- **CSS Variables**: 일관된 테마 관리
  - 색상 팔레트: Deep Navy, Royal Blue, Teal, Gold
- **Flexbox & CSS Grid**: 반응형 레이아웃
- **Custom Animations**: fadeInUp, bounce 등
- **반응형 디자인**: 3단계 브레이크포인트
  - Desktop: 1200px+
  - Tablet: 768px - 1199px
  - Mobile: < 768px

#### JavaScript (Vanilla)
- **순수 JavaScript**: 프레임워크 없이 구현
- **Intersection Observer API**: 스크롤 기반 애니메이션 트리거
- **DOM 조작**: 동적 UI 업데이트
- **이벤트 핸들링**: 스크롤, 클릭, 모바일 메뉴

### 외부 라이브러리 및 리소스

#### 폰트
- **Google Fonts**: Inter (400, 600, 700)
- **Pretendard**: 한글 최적화 폰트 (CDN)

#### 애니메이션
- **AOS (Animate On Scroll)** v2.3.1
  - 스크롤 기반 요소 애니메이션
  - 800ms 애니메이션 지속시간

#### 이미지 & 미디어
- Unsplash 이미지 (무료 고품질 이미지)
- YouTube 임베드 (학교 투어 영상)

## ✨ 주요 기능

### 사용자 인터페이스

#### 1. 네비게이션
- 고정 헤더 (스크롤 시 스타일 변경)
- 모바일 햄버거 메뉴
- 부드러운 스크롤 앵커 링크
- 스크롤 진행 표시줄

#### 2. 히어로 섹션
- 전체 화면 배경 이미지
- 애니메이션 헤드라인
- 2개의 CTA 버튼 (상담 신청, 더 알아보기)
- 스크롤 인디케이터

#### 3. 핵심 가치 (Core Values)
- 3개 주요 차별점 강조
  - 안전한 환경
  - 전문성
  - 지속적인 지원

#### 4. 생활 환경 섹션
- 4개 이미지 갤러리
- 검증된 홈스테이 정보
- 체크리스트 형식 특징 나열

#### 5. 교육 환경 섹션
- 다문화 교육 소개
- 소규모 학급 (20-25명)
- 통학 안전 시스템
- 주요 통계 (학교 수, 졸업생, 만족도)

#### 6. 학부모 후기
- 3개의 실제 후기 카드
- 학년 및 재학 기간 표시
- 익명 처리된 학부모 성함

#### 7. 연혁 타임라인
- 20년 회사 역사 (2005-2025)
- 주요 마일스톤 표시
- 누적 성과 통계

#### 8. 프로그램 & 서비스
- 4개 주요 서비스 카드
  1. 출국 전 준비
  2. 정착 지원
  3. 학업 관리
  4. 생활 케어

#### 9. 타우랑가 소개
- 5가지 장점 소개
- 자연환경, 교육 시스템, 안전성 등
- 이미지와 텍스트 2단 레이아웃

#### 10. 동영상 섹션
- YouTube 임베드 동영상
- 3개 동영상 썸네일 카드
  - 학생 일상
  - 다문화 친구 관계
  - 방과 후 활동

#### 11. 문의하기 섹션
- 3가지 문의 방법
  - KakaoTalk (실시간 상담)
  - Naver Cafe (학부모 커뮤니티)
  - 전화 상담 (070 번호)
- Google Maps 위치 링크
- 이메일 연락처

### JavaScript 인터랙션

1. **스크롤 진행 바**: 페이지 상단의 진행률 표시
2. **스티키 네비게이션**: 스크롤 시 네비게이션 스타일 변경
3. **모바일 메뉴 토글**: 햄버거 아이콘 클릭 시 메뉴 열기/닫기
4. **부드러운 스크롤**: 앵커 링크 클릭 시 부드러운 이동
5. **카운터 애니메이션**: 통계 수치의 숫자 증가 애니메이션
6. **스크롤 트리거 애니메이션**: AOS 라이브러리 활용

## 🎨 디자인 시스템

### 컬러 팔레트
```css
--color-primary: #1B3A6D    /* Deep Navy - 신뢰감 */
--color-secondary: #2E5090  /* Royal Blue - 전문성 */
--color-accent: #4FBDBA      /* Teal - 현대적 */
--color-gold: #D4AF37        /* Gold - 프리미엄 */
--color-light-gray: #F7F9FC  /* 배경 */
--color-white: #FFFFFF       /* 기본 배경 */
```

### 타이포그래피
- **본문**: Pretendard (한글 최적화)
- **대체 폰트**: Inter, system fonts
- **크기 범위**: 14px - 56px (반응형)

### 반응형 브레이크포인트
- **Desktop**: 1200px 이상 - 3단 그리드, 전체 레이아웃
- **Tablet**: 768px - 1199px - 조정된 간격 및 폰트
- **Mobile**: 768px 미만 - 단일 컬럼, 햨버거 메뉴

## 📦 배포

### GitHub Pages 배포 (자동)

프로젝트는 GitHub Pages를 통해 자동 배포됩니다.

#### 배포 단계
1. **변경사항 커밋 및 푸시**
   ```bash
   git add .
   git commit -m "Update: 변경 사항 설명"
   git push origin main
   ```

2. **GitHub Pages 설정 확인**
   - GitHub 저장소 → Settings → Pages
   - Source: Deploy from branch → `main` / `root`
   - 배포 URL: `https://ondallio.github.io/tauranga-study-website/`

3. **배포 완료 확인**
   - GitHub Actions 탭에서 배포 상태 확인
   - 일반적으로 2-5분 내 완료

### 다른 호스팅 플랫폼 배포

#### Netlify
1. Netlify 계정 로그인
2. "New site from Git" 클릭
3. GitHub 저장소 연결
4. Build settings:
   - Build command: (비워두기)
   - Publish directory: `/`
5. "Deploy site" 클릭

#### Vercel
1. Vercel 계정 로그인
2. "New Project" 클릭
3. GitHub 저장소 import
4. 자동 설정 사용 → "Deploy" 클릭

#### 기타 정적 호스팅
- **Firebase Hosting**
- **AWS S3 + CloudFront**
- **Azure Static Web Apps**
- **Cloudflare Pages**

## 🔧 개발 가이드

### 코드 수정하기

#### HTML 구조 변경
`index.html` 파일의 해당 섹션을 직접 수정:
```html
<!-- 예: 히어로 섹션 제목 변경 -->
<h1 class="hero-title" data-aos="fade-up">
  행복이 우선인 교육입니다
</h1>
```

#### 스타일 변경
`<style>` 태그 내부의 CSS 수정:
```css
/* 예: 프라이머리 컬러 변경 */
:root {
  --color-primary: #1B3A6D;
}
```

#### JavaScript 기능 수정
`<script>` 태그 내부의 코드 수정:
```javascript
// 예: 애니메이션 지속시간 변경
AOS.init({
  duration: 800,  // 이 값 변경
  offset: 100,
});
```

### 콘텐츠 업데이트

#### 텍스트 변경
- HTML 본문의 해당 텍스트 직접 수정
- 한글 인코딩 유지 (UTF-8)

#### 이미지 변경
- Unsplash URL을 다른 이미지 URL로 교체
- 또는 로컬 이미지 사용 시 `/assets/` 폴더 생성 후 경로 수정

#### 동영상 변경
YouTube iframe의 `src` 속성 변경:
```html
<iframe src="https://www.youtube.com/embed/새로운_비디오_ID"></iframe>
```

## 📈 성능 최적화

### 현재 상태
- 단일 HTML 파일: 54.5 KB
- 외부 이미지 로딩 (Unsplash)
- CDN 기반 폰트 및 라이브러리

### 개선 제안
1. **이미지 최적화**
   - Unsplash 이미지를 로컬로 다운로드
   - WebP 포맷 변환
   - 반응형 이미지 사용 (`srcset`)

2. **CSS/JS 분리**
   - 별도 파일로 분리하여 캐싱 활용
   - CSS: `styles.css`
   - JS: `script.js`

3. **레이지 로딩**
   - 이미지에 `loading="lazy"` 속성 추가
   - Intersection Observer로 동영상 레이지 로드

4. **압축 및 번들링**
   - HTML/CSS/JS 압축
   - 빌드 도구 도입 (Vite, Parcel 등)

## 🧪 테스트

### 브라우저 호환성 테스트
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

### 모바일 기기 테스트
- ✅ iOS Safari
- ✅ Android Chrome
- ✅ Samsung Internet

### 반응형 테스트
브라우저 개발자 도구에서 다양한 화면 크기 테스트:
```
- iPhone SE (375px)
- iPhone 12 Pro (390px)
- iPad (768px)
- iPad Pro (1024px)
- Desktop (1920px)
```

## 🤝 기여 가이드

프로젝트 개선에 기여하고 싶으시다면:

1. **Fork** 이 저장소
2. **Feature branch** 생성 (`git checkout -b feature/새기능`)
3. **변경사항 커밋** (`git commit -m 'Add: 새로운 기능 추가'`)
4. **Branch에 Push** (`git push origin feature/새기능`)
5. **Pull Request** 생성

### 커밋 메시지 규칙
```
Add: 새로운 기능 추가
Update: 기존 기능 수정
Fix: 버그 수정
Remove: 기능 제거
Docs: 문서 수정
Style: 코드 포맷팅 (기능 변경 없음)
Refactor: 코드 리팩토링
```

## 📝 라이선스

이 프로젝트는 타우랑가 유학원의 소유이며, 상업적 용도로 사용됩니다.

## 📞 문의

- **웹사이트**: [GitHub Pages URL]
- **이메일**: info@taurangastudy.com
- **카카오톡**: [ID 입력]
- **전화**: 070-XXXX-XXXX

## 🙏 감사의 말

- **이미지**: [Unsplash](https://unsplash.com) - 무료 고품질 이미지 제공
- **폰트**: [Google Fonts](https://fonts.google.com), [Pretendard](https://github.com/orioncactus/pretendard)
- **애니메이션**: [AOS Library](https://michalsnik.github.io/aos/)

---

**© 2025 타우랑가 유학원. All rights reserved.**
뉴질랜드 정식 등록 교육 기관
