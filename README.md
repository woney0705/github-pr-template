# 🚀 PR Template Practice

GitHub Actions를 활용한 자동 PR 템플릿 적용 연습 프로젝트

## 📌 프로젝트 목적

브랜치 전략에 따라 **자동으로 적절한 PR 템플릿이 적용**되도록 GitHub Actions를 구성하는 방법을 학습합니다.

### 학습 목표
- ✅ 브랜치별 PR 템플릿 자동 적용
- ✅ GitHub Actions 워크플로우 작성
- ✅ 다양한 PR 템플릿 관리 전략

## 🌳 브랜치 구조

```
main (production)
  ↑
stage (staging)
  ↑
backend          frontend
  ↑                ↑
feature/BE-*     feature/FE-*
fix/BE-*         fix/FE-*
```

## 📁 프로젝트 구조

```
.
├── .github/
│   ├── workflows/
│   │   └── auto-pr-template.yml           # PR 템플릿 자동 적용 워크플로우
│   └── PULL_REQUEST_TEMPLATE/
│       ├── dev_be_pr_template.md          # Backend 개발용 템플릿
│       ├── dev_fe_pr_template.md          # Frontend 개발용 템플릿
│       ├── stage_pr_template.md           # Stage 배포용 템플릿
│       └── prod_pr_template.md            # Production 배포용 템플릿
└── README.md
```

**중요**: `backend/` 및 `frontend/` 브랜치에는 `.github/PULL_REQUEST_TEMPLATE.md` 기본 파일을 생성하지 않습니다. GitHub Actions가 자동으로 처리합니다.

## 🎯 템플릿 적용 규칙

| Source Branch | Target Branch | 적용되는 템플릿 |
|--------------|---------------|----------------|
| `feature/BE-*`, `fix/BE-*` | `backend` | `dev_be_pr_template.md` |
| `feature/FE-*`, `fix/FE-*` | `frontend` | `dev_fe_pr_template.md` |
| `backend`, `frontend` | `stage` | `stage_pr_template.md` |
| `stage` | `main` | `prod_pr_template.md` |

## 🛠️ 설정 방법

### 1단계: 저장소 클론

```bash
git clone https://github.com/YOUR_USERNAME/pr-template-practice.git
cd pr-template-practice
```

### 2단계: 브랜치 생성

```bash
# Backend 브랜치 생성
git checkout -b backend
git push origin backend

# Frontend 브랜치 생성
git checkout -b frontend
git push origin frontend

# Stage 브랜치 생성
git checkout -b stage
git push origin stage
```

### 3단계: 브랜치별 기본 템플릿 설정

**✅ 권장 방법: GitHub Actions만 사용 (기본 템플릿 파일 없이)**

각 브랜치에 `.github/PULL_REQUEST_TEMPLATE.md` 기본 파일을 생성하지 않습니다.
대신 `.github/PULL_REQUEST_TEMPLATE/` 폴더에만 템플릿을 보관하고, GitHub Actions가 자동으로 적용합니다.

#### 템플릿 파일 생성

```bash
git checkout main

# 템플릿 폴더 생성
mkdir -p .github/PULL_REQUEST_TEMPLATE

# Backend 개발 템플릿
cat > .github/PULL_REQUEST_TEMPLATE/dev_be_pr_template.md << 'EOF'
## 📋 Backend 개발 작업

### 작업 유형
- [ ] ✨ 새 기능 (feature)
- [ ] 🐛 버그 수정 (fix)
- [ ] ♻️ 리팩토링 (refactor)
- [ ] ✅ 테스트 추가/수정 (test)

### 관련 이슈
- Closes #

### 변경 사항


### API 변경사항
- [ ] API 변경 없음
- [ ] API 추가
- [ ] API 수정
- [ ] API 삭제

### 테스트
- [ ] 단위 테스트 작성
- [ ] 통합 테스트 작성
- [ ] 로컬 환경 테스트 완료

### 리뷰 포인트

EOF

# Frontend 개발 템플릿
cat > .github/PULL_REQUEST_TEMPLATE/dev_fe_pr_template.md << 'EOF'
## 🎨 Frontend 개발 작업

### 작업 유형
- [ ] ✨ 새 기능 (feature)
- [ ] 🐛 버그 수정 (fix)
- [ ] 💄 UI/스타일 변경 (style)
- [ ] ♻️ 리팩토링 (refactor)

### 관련 이슈
- Closes #

### 변경 사항


### 스크린샷
#### Before


#### After


### 반응형 테스트
- [ ] Desktop
- [ ] Tablet
- [ ] Mobile

### 브라우저 테스트
- [ ] Chrome
- [ ] Safari
- [ ] Firefox

### 리뷰 포인트

EOF

# Stage 배포 템플릿
cat > .github/PULL_REQUEST_TEMPLATE/stage_pr_template.md << 'EOF'
## 🚀 Stage 배포 요청

### 배포 대상
- [ ] Backend
- [ ] Frontend
- [ ] Both

### 포함된 PR
- #
- #

### 주요 변경 사항


### Stage 테스트 체크리스트
- [ ] API 연동 테스트
- [ ] 핵심 기능 테스트
- [ ] 성능 테스트
- [ ] 보안 점검

### 롤백 계획


EOF

# Production 배포 템플릿
cat > .github/PULL_REQUEST_TEMPLATE/prod_pr_template.md << 'EOF'
## 🔥 Production 배포 요청

### 배포 버전
- 버전: v

### 배포 대상
- [ ] Backend
- [ ] Frontend
- [ ] Both

### 릴리즈 노트

#### 새로운 기능


#### 버그 수정


#### Breaking Changes
- [ ] Breaking change 없음
- [ ] Breaking change 있음:

### Production 배포 체크리스트
- [ ] Stage 환경에서 24시간 이상 안정 운영
- [ ] QA 팀 최종 승인
- [ ] 제품 책임자 승인
- [ ] DB 백업 완료
- [ ] 롤백 계획 수립
- [ ] 모니터링 설정 완료

### 배포 일정
- 예정 시간: YYYY-MM-DD HH:MM

### 긴급 연락망
- 배포 책임자:
- Backend 담당:
- Frontend 담당:

EOF

# 커밋 및 푸시
git add .github/PULL_REQUEST_TEMPLATE/
git commit -m "chore: PR 템플릿 추가 (Backend/Frontend 분리)"
git push origin main
```

#### 모든 브랜치에 동기화

```bash
# Backend 브랜치
git checkout backend
git merge main --no-ff -m "chore: PR 템플릿 설정 동기화"
git push origin backend

# Frontend 브랜치
git checkout frontend
git merge main --no-ff -m "chore: PR 템플릿 설정 동기화"
git push origin frontend

# Stage 브랜치
git checkout stage
git merge main --no-ff -m "chore: PR 템플릿 설정 동기화"
git push origin stage
```

**중요**: `.github/PULL_REQUEST_TEMPLATE.md` (기본 템플릿 파일)은 어느 브랜치에도 생성하지 않습니다!

### 4단계: Branch Protection Rules 설정

GitHub 저장소 → Settings → Branches → Add rule

#### Main 브랜치
- Branch name pattern: `main`
- ✅ Require a pull request before merging
- ✅ Require approvals: 2
- ✅ Require status checks to pass before merging

#### Stage 브랜치
- Branch name pattern: `stage`
- ✅ Require a pull request before merging
- ✅ Require approvals: 1

#### Backend/Frontend 브랜치
- Branch name pattern: `backend|frontend`
- ✅ Require a pull request before merging
- ✅ Require approvals: 1

## 🧪 테스트 방법

### 시나리오 1: Backend 개발 PR 테스트

```bash
# 1. Feature 브랜치 생성
git checkout backend
git checkout -b feature/BE-001-user-authentication

# 2. 파일 수정
echo "# User Authentication" > backend-feature.md
git add backend-feature.md
git commit -m "feat(BE): 사용자 인증 기능 추가"

# 3. Push
git push origin feature/BE-001-user-authentication

# 4. GitHub에서 PR 생성
# backend ← feature/BE-001-user-authentication
```

**예상 결과**: `dev_be_pr_template.md`의 내용이 자동으로 PR Description에 적용됨

### 시나리오 2: Frontend 개발 PR 테스트

```bash
# 1. Feature 브랜치 생성
git checkout frontend
git checkout -b feature/FE-001-login-page

# 2. 파일 수정
echo "# Login Page" > frontend-feature.md
git add frontend-feature.md
git commit -m "feat(FE): 로그인 페이지 UI 구현"

# 3. Push
git push origin feature/FE-001-login-page

# 4. GitHub에서 PR 생성
# frontend ← feature/FE-001-login-page
```

**예상 결과**: `dev_fe_pr_template.md`의 내용이 자동으로 적용됨

### 시나리오 3: Stage 배포 PR 테스트

```bash
# 1. Backend를 Stage로 PR 생성
# GitHub에서 stage ← backend PR 생성
```

**예상 결과**: `stage_pr_template.md`의 내용이 자동으로 적용됨

### 시나리오 4: Production 배포 PR 테스트

```bash
# 1. Stage를 Main으로 PR 생성
# GitHub에서 main ← stage PR 생성
```

**예상 결과**: `prod_pr_template.md`의 내용이 자동으로 적용됨

## 📝 PR 생성 빠른 링크

### Backend 개발 PR
- [Backend 개발 PR 생성](../../compare/backend...HEAD?template=dev_be_pr_template.md&expand=1)

### Frontend 개발 PR
- [Frontend 개발 PR 생성](../../compare/frontend...HEAD?template=dev_fe_pr_template.md&expand=1)

### 배포 PR
- [Backend → Stage](../../compare/stage...backend?template=stage_pr_template.md&expand=1)
- [Frontend → Stage](../../compare/stage...frontend?template=stage_pr_template.md&expand=1)
- [Stage → Production](../../compare/main...stage?template=prod_pr_template.md&expand=1)

**참고**: GitHub Actions가 자동으로 템플릿을 적용하므로, 이 링크 없이 일반적인 방법으로 PR을 생성해도 됩니다.

## 🔍 동작 원리

### GitHub Actions 워크플로우

`.github/workflows/auto-pr-template.yml` 파일이 다음과 같이 동작합니다:

1. **트리거**: PR이 생성될 때 (`pull_request: opened`)
2. **브랜치 확인**: PR의 target 브랜치(base)를 확인
3. **템플릿 선택**: 브랜치에 따라 적절한 템플릿 파일 선택
4. **자동 적용**: PR Description이 비어있거나 짧으면 템플릿 내용을 자동으로 삽입
5. **알림**: 댓글로 템플릿이 적용되었음을 알림

```yaml
# 핵심 로직 (간략화)
if (base === 'backend' || base === 'frontend') {
  templatePath = 'dev_pr_template.md';
} else if (base === 'stage') {
  templatePath = 'stage_pr_template.md';
} else if (base === 'main') {
  templatePath = 'prod_pr_template.md';
}
```

## 🎓 학습 포인트

### 1. GitHub Actions 기초
- 워크플로우 트리거 이해
- `actions/github-script` 사용법
- PR 자동화 구현

### 2. 브랜치 전략
- Git Flow 변형 구조
- 환경별 브랜치 분리 (dev/stage/prod)
- 브랜치 보호 규칙

### 3. PR 템플릿 관리
- 다중 템플릿 구조
- 상황별 템플릿 적용
- 템플릿 자동화

## 🐛 트러블슈팅

### 문제 1: GitHub Actions가 실행되지 않음

**원인**: Actions 권한 문제

**해결**:
1. Settings → Actions → General
2. Workflow permissions를 "Read and write permissions"로 변경
3. "Allow GitHub Actions to create and approve pull requests" 체크

### 문제 2: 템플릿이 자동으로 적용되지 않음

**원인**: PR Description이 이미 내용이 있음

**해결**: Actions는 PR body가 비어있거나 100자 미만일 때만 작동합니다. 테스트 시 빈 PR로 생성하세요.

### 문제 3: 템플릿 파일을 찾을 수 없음

**원인**: 파일 경로 문제

**해결**: `.github/PULL_REQUEST_TEMPLATE/` 폴더에 템플릿 파일이 있는지 확인

```bash
ls -la .github/PULL_REQUEST_TEMPLATE/
```

## 📚 참고 자료

- [GitHub Actions 공식 문서](https://docs.github.com/en/actions)
- [PR 템플릿 가이드](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)
- [GitHub Script Action](https://github.com/actions/github-script)

## 🤝 기여하기

이 프로젝트는 학습용입니다. 개선 아이디어가 있다면 이슈나 PR을 자유롭게 생성해주세요!

## 📄 라이선스

MIT License

## 👤 작성자

학습용 프로젝트

---

**⭐ 이 저장소가 도움이 되었다면 Star를 눌러주세요!**
