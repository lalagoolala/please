# Google OAuth origin_mismatch 문제 해결 가이드

## 문제 상황
Google 계정으로 로그인/회원가입 시 "400 오류: origin_mismatch" 메시지가 나타납니다.

## 원인
Google OAuth 2.0 설정에서 현재 사용 중인 도메인이 등록되지 않아 발생하는 문제입니다.

## 해결 방법

### 1단계: Google Cloud Console 접속
1. [Google Cloud Console](https://console.cloud.google.com)에 접속합니다
2. 프로젝트를 선택하거나 새로 생성합니다

### 2단계: OAuth 동의 화면 설정
1. 왼쪽 메뉴에서 **"OAuth 동의 화면"** 클릭
2. **사용자 유형** 선택:
   - 개발 환경: "외부" 선택
3. 필수 정보 입력:
   - 앱 이름: "5학년 보건교실"
   - 사용자 지원 이메일: 본인 이메일
   - 개발자 연락처: 본인 이메일
4. **저장 후 계속** 클릭

### 3단계: OAuth 2.0 클라이언트 ID 설정
1. 왼쪽 메뉴에서 **"사용자 인증 정보"** 클릭
2. **+ 사용자 인증 정보 만들기** → **OAuth 2.0 클라이언트 ID** 선택
3. **애플리케이션 유형**: "웹 애플리케이션" 선택
4. **이름**: "5학년 보건교실 Web"

### 4단계: 승인된 URI 추가 (중요!)
**승인된 JavaScript 원본(Authorized JavaScript Origins)** 섹션에 다음을 추가합니다:

```
http://localhost:8000
http://localhost:3000
http://localhost:5000
http://127.0.0.1:8000
http://127.0.0.1:3000
http://127.0.0.1:5000
https://yourdomain.com (실제 배포 도메인)
```

**승인된 리디렉션 URI(Authorized Redirect URIs)** 섹션에도 동일하게 추가합니다.

### 5단계: 클라이언트 ID 복사
생성된 클라이언트 ID를 복사합니다 (형식: `XXXXX.apps.googleusercontent.com`)

### 6단계: index.html 업데이트
[index.html](index.html)의 다음 부분을 수정합니다:

```javascript
// 약 1450줄 근처의 window.onload 함수 내
google.accounts.id.initialize({
    client_id: "YOUR_CLIENT_ID_HERE",  // ← 여기에 복사한 클라이언트 ID 입력
    callback: handleCredentialResponse
});
```

## 로컬 개발 환경에서 테스트하기

### 옵션 1: Python 웹 서버 사용
```bash
# 프로젝트 폴더에서
python -m http.server 8000
```

브라우저에서 `http://localhost:8000` 또는 `http://127.0.0.1:8000` 접속

### 옵션 2: Node.js http-server 사용
```bash
# 먼저 설치 (처음 한 번만)
npm install -g http-server

# 서버 시작
http-server -p 8000
```

## 프로덕션 배포

GitHub Pages에 배포하는 경우:
1. Google Cloud Console에서 새로운 클라이언트 ID 생성 (웹 애플리케이션)
2. **승인된 JavaScript 원본**에 GitHub Pages URL 추가:
   ```
   https://yourusername.github.io
   ```
3. 해당 클라이언트 ID를 index.html에 입력

## 테스트 체크리스트

- [ ] Google Cloud Console에 로컬 호스트 URI 등록됨
- [ ] Client ID가 index.html에 정확히 입력됨
- [ ] 로컬 서버가 정상 포트(8000, 3000, 5000)에서 실행 중
- [ ] 브라우저 콘솔에 오류 메시지 없음
- [ ] Google 로그인 버튼이 표시됨
- [ ] 클릭 시 Google 계정 선택 화면이 뜨는지 확인

## 추가 문제 해결

### "403 Forbidden" 오류
- Google Cloud 프로젝트에서 Google+ API가 활성화되었는지 확인
- **API 및 서비스** → **라이브러리** → "Google+ API" 검색 후 활성화

### "Invalid client" 오류
- Client ID가 올바르게 입력되었는지 확인
- 콘솔에서 생성한 Client ID와 index.html의 Client ID가 일치하는지 확인

### "Popup blocked" 오류
- 브라우저의 팝업 차단 설정 확인
- localhost URL을 팝업 차단 예외 목록에 추가

## 참고 링크
- [Google Sign-In 문서](https://developers.google.com/identity/gsi/web)
- [OAuth 2.0 설정 가이드](https://developers.google.com/identity/protocols/oauth2)
- [Google Cloud Console](https://console.cloud.google.com)
