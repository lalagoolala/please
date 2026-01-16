# 🎓 5학년 보건교실 - 최신 기능 가이드

## 📌 주요 업데이트 사항

### 1️⃣ Google 계정으로 회원가입/로그인
✅ **완료된 기능**:
- 회원가입 모달에 "Google 계정으로 회원가입" 버튼 추가
- Google 계정으로 첫 가입 시 계정 유형(학생/학부모/관리자) 선택 가능
- 이미 가입한 Google 계정으로는 자동 로그인

**사용 방법**:
1. 회원가입 모달 열기 → "Google 계정으로 회원가입" 클릭
2. Google 계정으로 로그인
3. 계정 유형 선택 모달에서 원하는 타입 선택
4. "가입 완료" 버튼으로 가입 완료
5. 자동으로 로그인되어 홈 페이지에서 사용자명 표시

---

### 2️⃣ 로그아웃 기능
✅ **위치**: 상단 네비게이션 바 우측
✅ **표시 조건**: 로그인 후에만 표시

```
[사용자명] | 🗑️ 회원탈퇴 | 🚪 로그아웃
```

**기능**:
- 클릭 시 현재 세션 삭제
- 홈 페이지로 이동하며 로그인 화면 복구
- 로그인/회원가입 버튼 재표시

---

### 3️⃣ 회원탈퇴 기능 (★ NEW)
✅ **위치**: 상단 네비게이션 바 우측 (로그인 후)
✅ **UI**: "🗑️ 회원탈퇴" 버튼

**사용 방법**:
1. 로그인 상태에서 "🗑️ 회원탈퇴" 버튼 클릭
2. 확인 모달에서 경고 메시지 확인
3. "확인 - 회원탈퇴" 버튼으로 최종 확인
4. 계정이 완전 삭제되고 자동으로 로그아웃됨

⚠️ **주의**:
- 회원탈퇴 후 계정을 복구할 수 없습니다
- 작성한 게시물과 댓글은 삭제되지 않습니다
- 취소 버튼으로 언제든 취소 가능

---

### 4️⃣ 관리자 회원 관리 패널 (★ NEW)
✅ **접근 방법**: 
- 관리자 계정으로 로그인
- 상단의 "⚙️ 관리" 메뉴 → 클릭

✅ **탭 구성**:

#### 📋 탭 1: 회원가입 승인
- 가입 신청 중인 회원 목록
- ✓ 승인 / ✕ 거부 버튼

#### 👥 탭 2: 회원 관리 (NEW!)
- 가입이 완료된 모든 회원 목록 조회
- 각 회원의 정보:
  - 👤 이름
  - 📧 이메일
  - 📚 학년/반 번호 (학생만)
  - 계정 유형 (👤 학생 / 👨‍👩‍👧 학부모 / 👑 관리자)
  - 🗑️ 삭제 버튼 (회원 계정 삭제 가능)

#### ⚙️ 탭 3: 콘텐츠 편집
- 공지사항, 건강 정보 등 수정 가능

---

## 🔐 Google OAuth 설정 (중요!)

### ⚠️ Error: origin_mismatch
Google 계정 로그인 시 다음 오류가 나타나면:
```
400 오류: origin_mismatch
또는
Access denied: origin_mismatch
```

### ✅ 해결 방법

**상세 가이드는 `GOOGLE_OAUTH_FIX.md` 파일 참조**

**빠른 해결 단계**:

#### Step 1: Google Cloud Console 접속
https://console.cloud.google.com

#### Step 2: 프로젝트 선택/생성
현재 프로젝트 사용

#### Step 3: 사용자 인증 정보 설정
1. 좌측 메뉴 → "사용자 인증 정보" 클릭
2. OAuth 2.0 클라이언트 ID 생성 (또는 기존 것 수정)

#### Step 4: 승인된 출처 추가 (★ CRITICAL)
**승인된 JavaScript 원본(Authorized JavaScript Origins)**:
```
http://localhost:8000
http://127.0.0.1:8000
https://yourdomain.com  (배포 후)
```

**승인된 리디렉션 URI**:
```
http://localhost:8000
http://127.0.0.1:8000
https://yourdomain.com  (배포 후)
```

#### Step 5: Client ID 복사 및 업데이트
- 클라이언트 ID 복사 (형식: `XXXXX.apps.googleusercontent.com`)
- index.html 의 약 1450줄 근처 수정:
```javascript
google.accounts.id.initialize({
    client_id: "YOUR_CLIENT_ID_HERE",  // ← 여기에 붙여넣기
    callback: handleCredentialResponse
});
```

---

## 🧪 테스트 및 실행

### 로컬 환경 실행

#### 방법 1: Python (권장)
```bash
# 프로젝트 폴더에서
python -m http.server 8000

# 또는 Python 3
python3 -m http.server 8000
```

브라우저에서 접속: **http://localhost:8000**

#### 방법 2: Node.js
```bash
npm install -g http-server
http-server -p 8000
```

#### 방법 3: VS Code Live Server
- VS Code에서 index.html 우클릭
- "Open with Live Server" 선택

---

## 📊 사용자 계정 체계

### 계정 유형별 기능

| 기능 | 학생👤 | 학부모👨‍👩‍👧 | 관리자👑 |
|------|--------|----------|---------|
| 로그인/회원가입 | ✅ | ✅ | ✅ |
| 질의응답 작성 | ✅ | ✅ | ✅ |
| 댓글 작성 | ✅ | ✅ | ✅ |
| 공지사항 수정 | ❌ | ❌ | ✅ |
| 건강정보 수정 | ❌ | ❌ | ✅ |
| 회원가입 승인 | ❌ | ❌ | ✅ |
| 회원 관리 | ❌ | ❌ | ✅ |
| 회원탈퇴 | ✅ | ✅ | ✅ |

### 기본 관리자 계정
- **ID**: abc
- **비밀번호**: 1234
- **이메일**: admin@health.com

> ⚠️ 프로덕션 환경에서는 반드시 변경하세요!

---

## 🎨 UI/UX 개선 사항

### 네비게이션 바 상태 표시

**로그인 전**:
```
🏥 5학년 보건교실 | 🏠 홈 | ❓ 질의응답 | 🔐 로그인 | 📝 회원가입
```

**로그인 후 (일반 사용자)**:
```
🏥 5학년 보건교실 | 🏠 홈 | ❓ 질의응답 | 👤 사용자명 | 🗑️ 회원탈퇴 | 🚪 로그아웃
```

**로그인 후 (관리자)**:
```
🏥 5학년 보건교실 | 🏠 홈 | ⚙️ 관리 | ❓ 질의응답 | 👑 (관리자) 사용자명 | 🗑️ 회원탈퇴 | 🚪 로그아웃
```

---

## 📝 데이터 구조

### localStorage 구조

```javascript
// 1. 사용자 데이터
{
    id: 1234567890,           // Unix timestamp
    name: "홍길동",           // 사용자 이름
    email: "user@gmail.com",  // 이메일
    userId: "user",           // 아이디 (이메일 앞부분)
    password: "hash_or_plain",// 비밀번호
    type: "student",          // 계정 타입: student, parent, admin
    status: "approved",       // 상태: approved, pending
    studentId: "5-1-10"       // 학년반번호 (학생만)
}

// 2. 현재 로그인 사용자
localStorage.getItem('currentUser')

// 3. 대기 중인 회원
localStorage.getItem('pendingUsers')

// 4. 게시물/댓글
localStorage.getItem('qnaList')

// 5. 공지사항
localStorage.getItem('notice')

// 6. 건강 정보
localStorage.getItem('healthInfo')
```

---

## 🔒 보안 참고사항

### 현재 상태 (개발 환경)
- ✅ 로컬 스토리지에 안전하게 저장
- ✅ 클라이언트 사이드 인증
- ⚠️ 프로덕션 환경에는 미흡

### 프로덕션 배포 시 권장사항
1. **백엔드 API 구현**
   - Node.js/Express 또는 Python/Flask 서버
   - JWT 또는 세션 기반 인증
   
2. **데이터베이스**
   - MongoDB, PostgreSQL 등으로 사용자 정보 저장
   
3. **보안**
   - HTTPS 사용
   - 비밀번호 해싱 (bcrypt)
   - CSRF 토큰
   - Rate limiting

4. **Google OAuth**
   - OAuth 2.0 Authorization Code Flow 사용
   - 서버에서 클라이언트 시크릿으로 토큰 검증

---

## 📞 문제 해결

### Q: Google 로그인이 안 됩니다
**A**: 
- localhost URI가 Google Cloud Console에 등록되었는지 확인
- Client ID가 맞는지 확인
- 브라우저 개발자 도구 콘솔에서 오류 메시지 확인
- 자세한 가이드는 GOOGLE_OAUTH_FIX.md 참조

### Q: 회원탈퇴 후 계정을 복구하고 싶습니다
**A**: 
- 현재 버전에서는 삭제된 계정을 복구할 수 없습니다
- 같은 이메일로 다시 회원가입 가능

### Q: 로그인 정보를 잊어버렸습니다
**A**: 
- 현재 버전에서는 비밀번호 재설정 기능이 없습니다
- 관리자에게 문의하여 계정 재설정 요청

### Q: 관리자 계정을 어떻게 생성하나요?
**A**: 
- 회원가입 시 계정 유형에서 "관리자" 선택
- 관리자가 승인해야 활성화됨

---

## 📚 관련 파일

| 파일명 | 설명 |
|--------|------|
| `index.html` | 메인 애플리케이션 (모든 기능 포함) |
| `GOOGLE_OAUTH_FIX.md` | Google OAuth 설정 가이드 |
| `CHANGES.md` | 변경 사항 상세 기록 |
| `README.md` | 프로젝트 개요 |
| `START_HERE.md` | 빠른 시작 가이드 |

---

## 🚀 다음 단계

- [ ] Google OAuth 설정 완료
- [ ] 모든 기능 로컬 테스트
- [ ] GitHub Pages 배포 (선택)
- [ ] 프로덕션 환경으로 마이그레이션 (선택)

---

**마지막 업데이트**: 2026년 1월 16일  
**상태**: ✅ 모든 요청 기능 완료  
**테스트**: 대기 중
