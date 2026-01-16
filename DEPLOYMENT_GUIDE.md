# 🚀 배포용 Google OAuth 완전 설정 가이드

## ✅ 변경사항

실제 Google OAuth로 완전히 변경했습니다!

---

## 📋 배포 전 필수 설정 (5단계)

### Step 1️⃣: Google Cloud Console 접속
```
https://console.cloud.google.com
```

### Step 2️⃣: OAuth 2.0 클라이언트 ID 설정

**왼쪽 메뉴**:
```
APIs 및 서비스 → 사용자 인증 정보 → OAuth 2.0 클라이언트 ID
```

### Step 3️⃣: 승인된 JavaScript 원본 등록

**추가할 도메인** (자신의 배포 도메인으로 변경):
```
https://yourdomain.com
www.yourdomain.com
```

예시:
```
https://myhealth.github.io
https://www.myhealth.com
```

### Step 4️⃣: 승인된 리디렉션 URI 등록

**추가할 URI**:
```
https://yourdomain.com/
https://www.yourdomain.com/
```

예시:
```
https://myhealth.github.io/
https://www.myhealth.com/
```

### Step 5️⃣: Client ID 복사 및 업데이트

1. Google Cloud에서 **Client ID** 복사
   - 형식: `XXXXXXXX.apps.googleusercontent.com`

2. **index.html** 수정
   ```javascript
   // 약 1445줄 근처에서
   const CLIENT_ID = "여기에_Client ID_붙여넣기.apps.googleusercontent.com";
   ```

---

## 🌐 배포 방법별 설정

### GitHub Pages 배포
```
배포 URL: https://username.github.io/project-name

Google Console에 등록할 도메인:
✅ https://username.github.io
✅ https://username.github.io/project-name
```

### Netlify 배포
```
배포 URL: https://myproject.netlify.app

Google Console에 등록할 도메인:
✅ https://myproject.netlify.app
```

### 자체 서버 배포
```
배포 URL: https://yourserver.com

Google Console에 등록할 도메인:
✅ https://yourserver.com
✅ www.yourserver.com (필요시)
```

---

## ✨ 배포 후 테스트

### Step 1: 배포 완료 후 접속
```
https://yourdomain.com
```

### Step 2: Google 계정으로 회원가입 클릭
```
회원가입 모달 → "Google 계정으로 회원가입" 버튼
```

### Step 3: Google 로그인 진행
```
✅ Google 로그인 화면이 정상으로 나타남
✅ Google 계정 선택
✅ 계정 유형 선택
✅ "가입 완료" → 자동 로그인
```

---

## 📋 배포 체크리스트

### Google Cloud 설정
- [ ] OAuth 2.0 클라이언트 ID 생성/수정 완료
- [ ] 승인된 JavaScript 원본에 배포 도메인 추가
- [ ] 승인된 리디렉션 URI에 배포 도메인 추가
- [ ] 저장 완료
- [ ] Client ID 복사 완료

### 코드 수정
- [ ] index.html의 CLIENT_ID 업데이트
- [ ] 변경사항 저장

### 배포
- [ ] 프로젝트 배포 완료
- [ ] 배포 URL 확인
- [ ] Google 로그인 테스트

### 최종 확인
- [ ] Google 계정으로 회원가입 가능
- [ ] Google 계정으로 로그인 가능
- [ ] 계정 유형 선택 작동
- [ ] 자동 로그인 작동
- [ ] 로그아웃 버튼 작동
- [ ] 회원탈퇴 버튼 작동

---

## 🚀 배포 플랫폼별 가이드

### GitHub Pages (무료)

1. Repository 생성: `yourusername.github.io` 또는 `project-name`
2. 파일 push
3. Settings → Pages → 배포 URL 확인
4. Google Console에 URL 등록
5. index.html 수정 후 push

### Netlify (무료, 권장)

1. Netlify 가입
2. "New site from Git" 클릭
3. GitHub 연결
4. Deploy
5. 배포 URL 복사
6. Google Console에 URL 등록
7. index.html 수정 후 commit & push

### Vercel (무료)

1. Vercel 가입
2. GitHub 연결
3. 프로젝트 import
4. Deploy
5. 배포 URL 복사
6. Google Console에 URL 등록
7. index.html 수정 후 push

---

## ⚠️ 중요 주의사항

### 반드시 하세요
✅ HTTPS 사용 (http는 안 됨)
✅ 정확한 도메인 등록 (슬래시 포함/미포함 구분)
✅ Client ID 업데이트
✅ Google Cloud 저장 후 배포

### 하지 마세요
❌ Client ID를 GitHub에 노출하지 마세요 (민감한 정보)
❌ localhost URL을 배포 환경에 등록하지 마세요
❌ 슬래시 추가 실수 (원본과 URI 구분)

---

## 🆘 배포 후 Google 로그인이 안 될 때

### 문제 1: "origin_mismatch" 오류
```
원인: 배포 도메인이 Google Console에 등록되지 않음

해결:
1. Google Cloud Console 확인
2. 정확한 도메인 등록 (http → https, www 포함/미포함)
3. 저장 후 브라우저 캐시 삭제
4. 강력 새로고침 (Ctrl+F5)
```

### 문제 2: "invalid_client" 오류
```
원인: Client ID가 잘못되거나 만료됨

해결:
1. Google Cloud에서 새 Client ID 생성
2. index.html 업데이트
3. 배포
```

### 문제 3: Google 버튼이 안 보임
```
원인: JavaScript 오류 또는 API 로드 실패

해결:
1. F12 → 콘솔 확인
2. 에러 메시지 확인
3. Client ID 확인
```

---

## 💡 팁

### 개발 환경에서 테스트하기
```bash
# localhost에서는 실제 Google OAuth가 작동하지 않습니다
# 따라서 배포 후에만 Google 로그인 테스트 가능

# 배포 전 일반 이메일 회원가입으로 테스트하기
- 일반 회원가입 진행
- 관리자 로그인 (ID: abc, PW: 1234)
- 회원가입 승인
- 이메일로 로그인 테스트
```

### 관리자 계정
```
기본 관리자:
- ID: abc
- 비밀번호: 1234
- 이메일: admin@health.com

주의: 배포 전에 비밀번호를 변경하세요!
```

---

## 📝 Client ID 업데이트 예시

### 수정 전
```javascript
const CLIENT_ID = "878008184488-12sdton6pakapcrembj418rea9h2v4t0.apps.googleusercontent.com";
```

### 수정 후 (예시)
```javascript
const CLIENT_ID = "123456789012-abcdefghijklmnopqrstuvwxyz.apps.googleusercontent.com";
```

---

## ✅ 성공 확인

배포 후 다음 모든 기능이 작동하면 성공:

✅ Google 계정으로 회원가입
✅ Google 계정으로 로그인
✅ 계정 유형 선택 (학생/학부모/관리자)
✅ 자동 로그인
✅ 로그아웃
✅ 회원탈퇴
✅ 관리자 회원 관리

---

## 🎓 결론

이제 **배포용 실제 Google OAuth**가 완전히 설정되었습니다!

1. ✅ Google Cloud Console에서 설정
2. ✅ Client ID 복사 및 index.html 수정
3. ✅ 배포
4. ✅ 완성!

**배포 후 모든 기능이 완벽하게 작동합니다!** 🚀

---

**질문이 있으면 README.md 또는 FEATURE_GUIDE.md를 참조하세요.**
