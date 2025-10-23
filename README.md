# Tauranga – Figma Design Preview
정적(Static) HTML 기반의 디자인 확인용 파일입니다. JS는 포함하지 않았고, Figma 임포트 플러그인(HTML to Figma 등)에서 안정적으로 구조를 인식하도록 작성했습니다.

## 파일 구성
```
/tauranga-figma-design
├─ index.html        # 디자인 미리보기 페이지
├─ /css/tailwind.css # 커스텀 유틸리티 포함 스타일
└─ /assets/          # 이미지·아이콘 (현재 외부 URL 사용)
```

## GitHub Pages 배포
1) GitHub에 새 repo 생성 → 이 폴더 업로드  
2) Settings → Pages → Deploy from Branch → `main / root`  
3) 배포 URL 예: `https://<username>.github.io/tauranga-figma-design/`

## Figma 임포트 팁
- 스크립트가 없으므로 구조/색/타이포·간격 위주로 변환됩니다.
- 카드 이미지 박스는 오른쪽으로 살짝 돌출되도록 설계되어 있습니다.
