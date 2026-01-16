# 🔴 Google OAuth redirect_uri_mismatch 오류 - 긴급 해결

## 현재 상황
```
❌ 오류: 400 오류: redirect_uri_mismatch
이 앱에서 잘못된 요청이 잘못되었습니다.
```

## 빠른 해결 (3단계)

### Step 1: Google Cloud Console 접속
👉 https://console.cloud.google.com

### Step 2: 사용자 인증 정보 수정
1. 왼쪽 메뉴 → **사용자 인증 정보** 클릭
2. **OAuth 2.0 클라이언트 ID** 찾기
3. 클릭하여 편집 모드 열기

### Step 3: 승인된 JavaScript 원본 추가
다음을 **모두** 추가하세요:

```
http://localhost:8000
http://127.0.0.1:8000
http://localhost:3000
http://127.0.0.1:3000
http://localhost:5000
http://127.0.0.1:5000
```

**승인된 리디렉션 URI** 에도 동일하게 추가:
```
http://localhost:8000/
http://127.0.0.1:8000/
http://localhost:3000/
http://127.0.0.1:3000/
http://localhost:5000/
http://127.0.0.1:5000/
```

### Step 4: 저장 및 재시도
1. **저장** 버튼 클릭
2. 브라우저 캐시 삭제 (Ctrl+Shift+Delete)
3. 페이지 새로고침 (Ctrl+F5)
4. 다시 Google 로그인 시도

---

## 추가 팁

### 포트 확인
현재 사용 중인 포트가 정확히 무엇인지 확인하세요:

```bash
# 콘솔에서
python -m http.server 8000
```

메시지: `Serving HTTP on 0.0.0.0 port 8000` 이면 **8000** 포트 사용

### 정확한 URL 확인
브라우저 주소창에서:
```
http://localhost:8000
또는
http://127.0.0.1:8000
```

어느 것을 사용 중인지 확인하고, **둘 다** Google Console에 등록하세요.

### Client ID 확인
Google Console에서 생성된 Client ID를 복사하고, 아래 명령어로 index.html 업데이트:

검색할 부분을 찾아서 Client ID 위치 확인:
```javascript
// index.html 약 1450줄 근처
client_id: "YOUR_CLIENT_ID_HERE"
```

---

## 만약 여전히 안 되면

### 문제 1: 캐시 삭제
```
Ctrl + Shift + Delete (캐시/쿠키 삭제)
또는
개발자 도구 → 네트워크 → "캐시 비우기 및 강력 새로고침" 체크박스 선택
```

### 문제 2: 포트 번호 변경
현재 8000이 아닌 다른 포트 사용:

```bash
python -m http.server 3000
```

그 후 Google Console에서 3000 포트도 등록

### 문제 3: 완전히 새로운 Client ID 생성
1. Google Cloud Console
2. "OAuth 2.0 클라이언트 ID" 항목 삭제
3. 새로운 클라이언트 ID 생성
4. localhost URI 등록 후 생성
5. 새 Client ID로 index.html 업데이트

---

## 성공 확인

Google 로그인 버튼을 클릭했을 때:
✅ Google 로그인 화면이 나타남
✅ 계정 선택 후 계정 유형 선택 모달이 나타남
✅ "가입 완료" 후 자동 로그인됨

---

## 더 자세한 가이드
📄 **GOOGLE_OAUTH_FIX.md** 파일 참조
