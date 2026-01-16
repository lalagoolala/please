# 🚀 GitHub Pages에 정적 웹사이트 배포하기

## 📌 확인사항

이 프로젝트는 **순수 정적 HTML/CSS/JavaScript**입니다:
- ✅ 서버 없음 (Python/Flask 불필요)
- ✅ 데이터베이스 없음 (Firebase 불필요)
- ✅ GitHub Pages에서 직접 배포 가능
- ✅ 무료 호스팅

---

## 🎯 배포 3단계 (5분)

### Step 1️⃣: Git에 업로드

```bash
# 프로젝트 디렉토리로 이동
cd c:\Users\cyh99\Documents\프로젝트

# 모든 파일 추가
git add .

# 커밋
git commit -m "정적 HTML 홈페이지 배포"

# GitHub에 푸시
git push origin main
```

### Step 2️⃣: GitHub Pages 활성화

1. **GitHub 저장소** 접속
2. **Settings** (⚙️) 클릭
3. 왼쪽 메뉴에서 **Pages** 선택
4. **Source** → `main` 선택 (또는 `main branch`)
5. **Save** 클릭

![GitHub Pages 설정](https://docs.github.com/assets/cb-8330/images/help/pages/pages-settings-screenshot.png)

### Step 3️⃣: 접속

GitHub Pages 빌드 완료까지 **2-3분** 기다린 후 접속:

```
https://[username].github.io/[repository-name]
```

**예시:**
- GitHub 사용자명: `cyh99`
- 저장소 이름: `home`
- **배포 URL**: `https://cyh99.github.io/home`

---

## ✅ 확인 사항

### GitHub 저장소 확인
```bash
# 저장소가 public인지 확인
# Settings → Visibility → Public 선택
```

### 배포 상태 확인
1. Settings → Pages 에서 상태 확인
2. 초록색 체크표시 = 배포 완료 ✅
3. 주황색 점 = 배포 중 ⏳

### 첫 접속 시 안 보이면?
1. **브라우저 캐시 삭제**: `Ctrl + Shift + Delete`
2. **강제 새로고침**: `Ctrl + F5`
3. **2-3분 더 대기** (GitHub Pages 갱신 시간)

---

## 🎨 커스터마이징

### 학교명 변경
`index.html`의 5번 줄:
```html
<div class="navbar-brand">🏥 [학교명] 보건교실</div>
```

### 공지사항 미리 입력
`index.html`의 JavaScript 섹션 (약 400줄):
```javascript
localStorage.setItem('notice', JSON.stringify([
    { 
        id: 1, 
        title: '건강 습관 챌린지 시작', 
        author: '보건선생님', 
        content: '이번 달부터 건강 습관 챌린지를 시작합니다!', 
        date: '2024.01.10' 
    }
]));
```

### 색상 변경
CSS 섹션의 색상 코드 변경:
```css
#ff6b6b  /* 빨강 */
#667eea  /* 보라 */
#ffd93d  /* 노랑 */
```

---

## 📁 파일 구조

```
[저장소]/
├── index.html          ← 메인 파일 (이것 하나로 완성!)
├── README.md           ← 설명서
└── STATIC_DEPLOY.md    ← 이 파일
```

---

## 💾 데이터는 어디에 저장되나요?

### 저장 위치
- 각 사용자의 **브라우저 로컬 스토리지**
- 외부 서버/클라우드 없음

### 특징
- ✅ 개인정보 안전 (로컬 저장)
- ✅ 인터넷 없이도 사용 가능
- ⚠️ PC/태블릿/휴대폰마다 데이터 분리
- ⚠️ 브라우저 캐시 삭제 시 데이터 삭제됨

---

## 🔄 업데이트하기

홈페이지를 수정했을 때:

```bash
# 변경사항 커밋
git add .
git commit -m "홈페이지 수정 설명"
git push origin main
```

**배포 시간**: 1-2분 후 반영됨

---

## 🌐 브라우저 호환성

| 브라우저 | 지원 |
|---------|------|
| Chrome | ✅ |
| Safari | ✅ |
| Firefox | ✅ |
| Edge | ✅ |
| Opera | ✅ |
| 모바일 Chrome | ✅ |
| iOS Safari | ✅ |

---

## 🚀 고급 옵션 (선택사항)

### 1. 도메인 연결하기
Settings → Pages → Custom domain
```
example.com (또는 yourdomain.com)
```

### 2. HTTPS 자동 설정
Settings → Pages → "Enforce HTTPS" 체크

### 3. CI/CD 파이프라인
`.github/workflows/deploy.yml` 파일 추가로 자동 배포

---

## 📞 문제 해결

### Q: 배포가 안 되는데?
**A:** 
1. 저장소가 **Public** 설정인지 확인
2. `index.html` 파일이 프로젝트 **루트**에 있는지 확인
3. GitHub Pages **Settings**에서 `main` 브랜치 선택 확인

### Q: 홈페이지가 안 보이는데?
**A:**
1. 배포 완료까지 **2-3분** 기다리기
2. 브라우저 캐시 삭제: `Ctrl + Shift + Delete`
3. 강제 새로고침: `Ctrl + F5`

### Q: 로그인이 안 되는데?
**A:**
1. 같은 브라우저에서 회원가입했는지 확인
2. PC/태블릿/휴대폰은 데이터가 분리되어 있음
3. 브라우저 개발자 도구 → Application → Local Storage 확인

### Q: 데이터를 다른 기기에서도 보고 싶어요
**A:** 클라우드 저장소 추가 필요 (Firebase, MongoDB 등)

---

## 🎓 다음 단계

### 기초 학습
- [HTML 튜토리얼](https://www.w3schools.com/html/)
- [CSS 튜토리얼](https://www.w3schools.com/css/)
- [JavaScript 튜토리얼](https://www.w3schools.com/js/)

### 심화 학습
- 데이터베이스 연동 (Firebase, MongoDB)
- 백엔드 서버 (Node.js, Python)
- 인증 시스템 (OAuth, JWT)

---

## ✨ 완료!

축하합니다! 🎉 이제 GitHub Pages에서 정적 홈페이지가 배포되었습니다!

**배포된 URL**: `https://[username].github.io/[repository-name]`

더 강력한 기능이 필요하면, Firebase나 Node.js 백엔드를 추가할 수 있습니다.
