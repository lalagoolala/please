# 🔴 Google OAuth redirect_uri_mismatch 오류 - 즉시 해결

## 📸 현재 문제
```
❌ 400 오류: redirect_uri_mismatch
오류 메시지: "이 앱에서 잘못된 요청이 들어왔습니다"
```

---

## ⚡ 3분 빠른 해결

### 👉 핵심: localhost URI를 Google Cloud Console에 등록하지 않았기 때문!

---

## 🚀 지금 바로 하기 (5단계)

### Step 1: 이 링크 열기
```
https://console.cloud.google.com
```

### Step 2: 왼쪽 메뉴
```
APIs 및 서비스 → 사용자 인증 정보
```

### Step 3: OAuth 클라이언트 ID 수정
```
"웹 애플리케이션" OAuth 2.0 클라이언트 ID 찾아 클릭
```

### Step 4: 다음 URL들 추가 ⭐ (MOST IMPORTANT)
```
승인된 JavaScript 원본:
- http://localhost:8000
- http://127.0.0.1:8000

승인된 리디렉션 URI:
- http://localhost:8000/
- http://127.0.0.1:8000/
```

### Step 5: 저장 및 재시도
```
[저장] 클릭
    ↓
브라우저: Ctrl+Shift+Delete (캐시 삭제)
    ↓
페이지: Ctrl+F5 (강력 새로고침)
    ↓
Google 로그인 버튼 다시 클릭
```

---

## ✅ 성공하면 이렇게 됩니다

```
Google 로그인 버튼 클릭
    ↓
✅ Google 계정 선택 화면 표시 (오류 없음!)
    ↓
계정 선택
    ↓
✅ 계정 유형 선택 모달 나타남
    ↓
계정 유형 선택 (학생/학부모/관리자)
    ↓
✅ "가입 완료" 클릭
    ↓
✅ 자동 로그인 + 홈 페이지 표시
```

---

## 📋 더 자세한 가이드

시간이 있으면 다음 파일을 읽어주세요:

| 파일 | 내용 | 시간 |
|------|------|------|
| **GOOGLE_OAUTH_QUICK_FIX.md** | 상세한 해결 방법 | 5분 |
| **GOOGLE_OAUTH_STEP_BY_STEP.md** | 스크린샷 단계별 가이드 | 10분 |
| **google-oauth-setup.html** | 웹 브라우저에서 보는 가이드 | 10분 |

---

## 🎯 추가 팁

### 포트 확인
내가 사용 중인 포트가 정확히 무엇인지 확인:

```bash
# 터미널을 보면:
python -m http.server 8000
# 또는
python -m http.server 3000
# 또는 다른 포트
```

**포트 번호**: `_______` (확인 후 기록)

### 여러 포트 모두 추가하기 (안전)
혹시 모르니 자주 사용하는 포트 모두 추가:

```
http://localhost:3000
http://127.0.0.1:3000
http://localhost:5000
http://127.0.0.1:5000
http://localhost:8000
http://127.0.0.1:8000
```

---

## 🆘 그래도 안 되면?

### 1. 콘솔 에러 확인
```
F12 → 콘솔 탭 → 빨간 메시지 확인 및 공유
```

### 2. 캐시 완전 삭제
```
Ctrl + Shift + Delete 누르기
"모든 시간" 선택 → 캐시 삭제 진행
```

### 3. 다른 브라우저 시도
```
Chrome / Firefox / Safari 중 하나 더 시도
```

### 4. 새 Client ID 생성
```
기존 클라이언트 ID 삭제
새로 만들기 (이번엔 localhost 미리 등록 후)
```

---

## 💡 핵심 포인트

✅ **필수**: Google Cloud Console에서 localhost URI 등록
✅ **필수**: 브라우저 캐시 완전 삭제
✅ **필수**: 강력 새로고침 (Ctrl+F5)

❌ **금지**: Client ID를 URL에 직접 노출

---

## 📞 다음 단계

1. ✅ Google Console 설정 완료
2. ✅ 브라우저 캐시 삭제
3. ✅ Google 로그인 테스트
4. ✅ 계정 유형 선택 후 가입

**모두 되면 완성!** 🎉

---

**마지막 팁**: 이 절차를 따르면 99% 해결됩니다!

혹시 문제가 있으면:
- GOOGLE_OAUTH_QUICK_FIX.md 읽기
- 또는 GOOGLE_OAUTH_STEP_BY_STEP.md 읽기
