# 한국어 학습 랜딩페이지

순수 HTML, CSS, JavaScript로만 구성된 간단한 랜딩페이지입니다.

## 📁 파일 구조

```
reading/
├── index.html          # 메인 페이지
└── public/
    └── video/          # 비디오 파일들
        ├── chant.mp4
        ├── chat.mp4
        ├── key.mp4
        └── voice.mp4
```

## 🚀 실행 방법

### 방법 1: 브라우저로 직접 열기 (간단)
1. `index.html` 파일을 브라우저로 드래그 앤 드롭
2. 또는 파일 탐색기에서 `index.html`을 더블클릭

**주의**: 일부 브라우저에서는 로컬 파일 프로토콜(`file://`)로 비디오가 재생되지 않을 수 있습니다.

### 방법 2: 간단한 로컬 서버 실행 (권장)

#### Python 사용
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

#### Node.js 사용
```bash
# npx 사용 (Node.js 설치 필요)
npx serve

# 또는 http-server 사용
npx http-server -p 8000
```

#### PHP 사용
```bash
php -S localhost:8000
```

그 다음 브라우저에서 `http://localhost:8000` 접속

## 🎨 기능

- **4개 섹션**: 각각 다른 비디오 배경
- **스크롤 애니메이션**: 부드러운 페이드인 효과
- **네비게이션 도트**: 우측 사이드바로 섹션 이동
- **반응형 디자인**: 모바일/태블릿/데스크톱 지원
- **소셜 링크**: 유튜브, 인스타그램, 블로그, 이메일

## 📝 커스터마이징

### 텍스트 변경
`index.html` 파일을 텍스트 에디터로 열어서 `<h1>`, `<p>` 태그 내용을 수정하세요.

### 비디오 변경
`public/video/` 폴더의 mp4 파일을 교체하거나, HTML에서 `<source src="...">` 경로를 수정하세요.

### 링크 변경
마지막 섹션의 링크들을 찾아서 `href` 속성을 수정하세요.

## 🌐 배포 방법

### Cloudflare Pages (권장) ⭐
1. Cloudflare 계정 생성 (https://dash.cloudflare.com)
2. Workers & Pages → Create application → Pages → Connect to Git
3. GitHub 저장소 연결
4. 빌드 설정:
   - Build command: (비워두기)
   - Build output directory: `.`
5. 자동 배포 완료!
6. 자세한 가이드: `CLOUDFLARE_MIGRATION_GUIDE.md` 참고

### GitHub Pages
1. GitHub 저장소 생성
2. 파일 업로드
3. Settings > Pages에서 배포 설정

### Netlify / Vercel
1. 프로젝트 폴더를 드래그 앤 드롭
2. 자동 배포 완료

### 일반 웹 호스팅
FTP로 파일들을 업로드하면 됩니다.

## 💡 문제 해결

### 비디오가 재생되지 않을 때
- 로컬 서버를 사용해서 실행하세요 (`file://` 대신 `http://`)
- 브라우저 콘솔(F12)에서 에러 확인
- 비디오 파일 경로가 올바른지 확인

### 스타일이 깨질 때
- HTML 파일의 `<style>` 태그가 손상되지 않았는지 확인
- 브라우저 캐시를 지우고 새로고침 (Ctrl + F5)

---

**모든 Next.js 의존성이 제거되었습니다!** 이제 순수 HTML/CSS/JS만으로 작동합니다.

