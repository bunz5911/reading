# Cloudflare Pages 마이그레이션 가이드

이 가이드는 현재 프로젝트를 Cloudflare Pages로 마이그레이션하는 방법을 설명합니다.

## 사전 준비

1. **Cloudflare 계정 생성**
   - https://dash.cloudflare.com/sign-up 접속
   - 무료 계정으로 시작 가능

2. **도메인 준비 (선택사항)**
   - 기존 도메인이 있다면 Cloudflare에 추가
   - 또는 Cloudflare Pages의 무료 서브도메인 사용 가능 (예: `your-project.pages.dev`)

## 마이그레이션 단계

### 1단계: GitHub 저장소 확인

현재 프로젝트가 GitHub에 연결되어 있는지 확인:
```bash
git remote -v
```

GitHub에 연결되어 있지 않다면:
```bash
git remote add origin https://github.com/your-username/reading.git
git push -u origin main
```

### 2단계: Cloudflare Pages 프로젝트 생성

1. **Cloudflare 대시보드 접속**
   - https://dash.cloudflare.com 접속
   - 좌측 메뉴에서 "Workers & Pages" 클릭
   - "Create application" → "Pages" → "Connect to Git" 선택

2. **GitHub 저장소 연결**
   - GitHub 계정 인증
   - 저장소 선택: `bunz5911/reading`
   - "Begin setup" 클릭

3. **빌드 설정**
   - **Project name**: `reading` (또는 원하는 이름)
   - **Production branch**: `main`
   - **Build command**: (비워두기 - 정적 사이트이므로 빌드 불필요)
   - **Build output directory**: `.` (루트 디렉토리)
   - **Root directory**: `/` (기본값)

4. **환경 변수 설정** (필요한 경우)
   - 현재는 정적 사이트이므로 환경 변수 불필요

5. **"Save and Deploy" 클릭**

### 3단계: 커스텀 도메인 설정 (선택사항)

1. **도메인 추가**
   - Pages 프로젝트 → "Custom domains" 탭
   - "Set up a custom domain" 클릭
   - 도메인 입력 (예: `reading.yourdomain.com`)

2. **DNS 설정**
   - Cloudflare에 도메인이 추가되어 있다면 자동으로 설정됨
   - 다른 DNS 제공자를 사용하는 경우 CNAME 레코드 추가 필요

### 4단계: 배포 확인

1. **자동 배포**
   - GitHub에 push하면 자동으로 배포됩니다
   - 배포 상태는 Cloudflare Pages 대시보드에서 확인 가능

2. **수동 배포**
   - "Deployments" 탭에서 특정 커밋을 선택하여 재배포 가능

## 파일 구조

프로젝트에 다음 파일들이 추가되었습니다:

- `_headers`: HTTP 헤더 설정 (캐싱, 보안 헤더)
- `_redirects`: 리다이렉트 규칙
- `cloudflare-pages.json`: Cloudflare Pages 설정 (참고용)

## 성능 최적화

### 이미지 최적화
- Cloudflare Images 사용 고려 (선택사항)
- 현재는 lazy loading이 적용되어 있음

### 캐싱 전략
- `_headers` 파일에 캐싱 규칙이 설정되어 있습니다:
  - HTML: 1시간
  - CSS/JS: 1년 (immutable)
  - 이미지/비디오: 1년 (immutable)

### CDN 활용
- Cloudflare Pages는 자동으로 글로벌 CDN을 제공합니다
- 전 세계 어디서나 빠른 로딩 속도

## 보안 설정

`_headers` 파일에 다음 보안 헤더가 포함되어 있습니다:
- `X-Frame-Options`: 클릭재킹 방지
- `X-Content-Type-Options`: MIME 타입 스니핑 방지
- `X-XSS-Protection`: XSS 공격 방지
- `Referrer-Policy`: 리퍼러 정보 제어

## 모니터링 및 분석

1. **Analytics**
   - Cloudflare Pages 대시보드에서 기본 분석 제공
   - "Analytics" 탭에서 방문자 통계 확인

2. **Web Vitals**
   - 성능 메트릭 자동 수집
   - Core Web Vitals 모니터링

## 트러블슈팅

### 배포 실패 시
1. 빌드 로그 확인
2. 파일 경로 확인 (대소문자 구분)
3. `_headers` 파일 문법 확인

### 이미지가 로드되지 않을 때
1. 파일 경로 확인 (`public/` 폴더 구조)
2. 대소문자 확인
3. 브라우저 캐시 클리어

### 리다이렉트가 작동하지 않을 때
1. `_redirects` 파일 문법 확인
2. Cloudflare Pages의 리다이렉트 규칙 확인

## 비용

- **Cloudflare Pages 무료 플랜**:
  - 무제한 요청
  - 무제한 대역폭
  - 500개 빌드/월
  - 커스텀 도메인 지원

## 추가 리소스

- [Cloudflare Pages 문서](https://developers.cloudflare.com/pages/)
- [Cloudflare Pages 시작 가이드](https://developers.cloudflare.com/pages/get-started/)
- [Cloudflare 커뮤니티 포럼](https://community.cloudflare.com/)

## 마이그레이션 체크리스트

- [ ] Cloudflare 계정 생성
- [ ] GitHub 저장소 확인
- [ ] Cloudflare Pages 프로젝트 생성
- [ ] 빌드 설정 완료
- [ ] 첫 배포 성공 확인
- [ ] 커스텀 도메인 설정 (선택사항)
- [ ] HTTPS 자동 설정 확인
- [ ] 성능 테스트
- [ ] 모니터링 설정 확인

## 다음 단계

마이그레이션 완료 후:
1. 기존 호스팅 서비스에서 DNS 변경 (도메인 사용 시)
2. 구글 폼 iframe URL 확인 (필요시 업데이트)
3. 모든 링크 및 리소스 경로 테스트
4. 모바일 반응형 확인
5. 성능 최적화 추가 고려

