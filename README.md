# GitHub 저장소 생성부터 Merge Conflict 해결까지 완벽 가이드

이 문서는 GitHub 저장소 생성, Git 계정 설정, 작업물 Push, 브랜치 생성/Merge, 그리고 Conflict 해결까지의 전체 과정을 다룹니다.

---

## 📋 목차

1. [GitHub 저장소 생성](#1-github-저장소-생성)
2. [Personal Access Token (PAT) 발행](#2-personal-access-token-pat-발행)
3. [Git Bash 글로벌 계정 설정](#3-git-bash-글로벌-계정-설정)
4. [저장소 Clone 및 연결](#4-저장소-clone-및-연결)
5. [작업물 Push](#5-작업물-push)
6. [브랜치 생성 및 작업](#6-브랜치-생성-및-작업)
7. [Merge 및 Conflict 해결](#7-merge-및-conflict-해결)

---

## 1. GitHub 저장소 생성

### 1.1 GitHub 웹사이트에서 저장소 생성

**단계:**

1. GitHub 계정으로 로그인 (https://github.com)
2. 오른쪽 상단 **+** 버튼 클릭
3. **New repository** 선택

### 1.2 저장소 설정

```
Repository name: my-project
Description: 프로젝트 설명 입력
Visibility: Public 또는 Private 선택
Initialize this repository with:
  ☑ Add a README file
  ☑ Add .gitignore
  ☑ Choose a license
```

**권장 설정:**
- **Public**: 오픈소스 프로젝트
- **Private**: 개인/팀 프로젝트
- README 파일은 필수로 체크
- .gitignore는 프로젝트 언어에 맞춰 선택

### 1.3 저장소 생성 완료

생성 후 저장소 주소 복사:
```
https://github.com/username/my-project.git
```

---

## 2. Personal Access Token (PAT) 발행

### 2.1 토큰 생성 페이지 접속

**단계:**

1. GitHub 계정 설정 (https://github.com/settings/profile)으로 이동
2. 왼쪽 사이드바에서 **Developer settings** 클릭
3. **Personal access tokens** → **Tokens (classic)** 클릭
4. **Generate new token** → **Generate new token (classic)** 클릭

### 2.2 토큰 설정

```
Token name: git-bash-token (또는 자유로운 이름)

Expiration: 30 days / 60 days / 90 days / No expiration

Select scopes:
  ☑ repo (전체 저장소 접근)
    ☑ repo:status
    ☑ repo_deployment
    ☑ public_repo
    ☑ repo:invite
    ☑ security_events
  ☑ write:packages
  ☑ read:packages
  ☑ delete:packages
```

**권장 설정:**
- Expiration: 90 days (보안을 위해 정기적 갱신)
- Scopes: repo 전체 체크 (로컬 작업에 필요)

### 2.3 토큰 복사 및 저장

```
ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

<span style="color:red">⚠️ 중요: 토큰은 이 화면에서만 보이므로 반드시 복사하여 안전하게 보관</span>

---

## 3. Git Bash 글로벌 계정 설정

### 3.1 Git Bash 열기

```bash
# Windows: 시작 메뉴 → Git Bash 검색 후 실행
# Mac/Linux: 터미널 열기
```

### 3.2 글로벌 사용자 정보 설정

```bash
# 사용자 이름 설정
git config --global user.name "Your Name"

# 이메일 설정
git config --global user.email "your.email@example.com"

# 설정 확인
git config --global --list
```

**확인 결과:**
```
user.name=Your Name
user.email=your.email@example.com
```

### 3.3 인증 정보 저장 설정 (선택사항)

토큰 매번 입력을 피하기 위해 자격증명 저장:

```bash
# Windows: Credential Manager에 저장
git config --global credential.helper wincred

# Mac: Keychain에 저장
git config --global credential.helper osxkeychain

# Linux: 암호화된 캐시에 저장
git config --global credential.helper cache
```

---

## 4. 저장소 Clone 및 연결

### 4.1 저장소 Clone

```bash
# 작업할 폴더로 이동 (예: C:\Users\YourName\Documents)
cd ~/Documents

# 저장소 Clone
git clone https://github.com/username/my-project.git

# Clone된 폴더로 이동
cd my-project
```

### 4.2 원격 저장소 확인

```bash
# 원격 저장소 정보 조회
git remote -v

# 출력 예시:
# origin  https://github.com/username/my-project.git (fetch)
# origin  https://github.com/username/my-project.git (push)
```

### 4.3 초기 설정 확인

```bash
# 현재 저장소의 설정 확인
git config --local --list

# 현재 브랜치 확인
git branch -a

# 커밋 이력 확인
git log --oneline
```

---

## 5. 작업물 Push

### 5.1 파일 생성/수정

```bash
# 새로운 파일 생성 (예: dummy_personal_data.md)
touch dummy_personal_data.md

# 파일 내용 추가 (에디터로 편집)
# 내용 작성 후 저장
```

### 5.2 변경사항 Staging

```bash
# 특정 파일 Staging
git add dummy_personal_data.md

# 또는 모든 변경사항 Staging
git add .

# Staging된 파일 확인
git status
```

**출력 예시:**
```
On branch main

Changes to be committed:
  new file:   dummy_personal_data.md
```

### 5.3 커밋 생성

```bash
# 커밋 메시지와 함께 커밋
git commit -m "feat: 개인정보 더미데이터 파일 추가"

# 또는 자세한 커밋 메시지
git commit -m "feat: 개인정보 더미데이터 파일 추가

- 100명의 더미 개인정보 포함
- 표 형식으로 정렬
- 테스트 및 개발용"
```

### 5.4 커밋 이력 확인

```bash
# 최근 커밋 확인
git log --oneline -5

# 출력 예시:
# a1b2c3d feat: 개인정보 더미데이터 파일 추가
# e4f5g6h initial commit
```

### 5.5 원격 저장소에 Push

```bash
# main 브랜치에 Push
git push origin main

# 또는 현재 브랜치에 Push
git push
```

**첫 번째 Push 시 인증:**
```
Username for 'https://github.com': username
Password for 'https://github.com': [PAT 토큰 입력]
```

<span style="color:green">✅ Push 완료! GitHub 웹사이트에서 파일이 업로드된 것을 확인</span>

---

## 6. 브랜치 생성 및 작업

### 6.1 로컬 브랜치 생성

```bash
# 새로운 브랜치 생성
git branch feature/add-colors

# 또는 생성과 동시에 체크아웃
git checkout -b feature/add-colors

# 또는 최신 Git (2.23+)
git switch -c feature/add-colors

# 현재 브랜치 확인
git branch

# 출력:
# main
# * feature/add-colors
```

### 6.2 브랜치에서 작업

```bash
# 파일 수정 (기존 파일 또는 새 파일)
# 에디터에서 내용 수정

# 변경사항 확인
git diff dummy_personal_data.md

# Staging
git add dummy_personal_data.md

# 커밋
git commit -m "style: 글자 색상 HTML 태그 추가"

# 커밋 확인
git log --oneline -3
```

### 6.3 원격 브랜치에 Push

```bash
# 로컬 브랜치를 원격에 Push
git push -u origin feature/add-colors

# 또는
git push origin feature/add-colors

# -u 옵션: upstream 설정 (다음부터 git push만으로 가능)
```

**출력 예시:**
```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 356 bytes | 178.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: Create a pull request for 'feature/add-colors':
remote:      https://github.com/username/my-project/pull/new/feature/add-colors
```

### 6.4 다른 브랜치에서 충돌 파일 생성

<span style="color:orange">⚠️ Conflict를 시뮬레이션하기 위해 다른 브랜치를 생성</span>

```bash
# main 브랜치로 돌아가기
git checkout main

# 또는
git switch main

# 다른 브랜치 생성
git checkout -b feature/update-version

# 같은 파일(dummy_personal_data.md)을 다르게 수정
# 에디터에서 내용 수정

# Staging 및 커밋
git add dummy_personal_data.md
git commit -m "docs: 버전 정보 업데이트"

# 원격에 Push
git push -u origin feature/update-version
```

---

## 7. Merge 및 Conflict 해결

### 7.1 Pull Request (PR) 생성

**GitHub 웹사이트에서:**

1. 저장소 접속 (https://github.com/username/my-project)
2. **Pull requests** 탭 클릭
3. **New pull request** 버튼 클릭
4. **Compare** 드롭다운에서 브랜치 선택
   - Base: `main`
   - Compare: `feature/add-colors`
5. **Create pull request** 클릭
6. PR 제목과 설명 입력
7. **Create pull request** 클릭

**PR 설명 템플릿:**
```markdown
## 변경 사항
- 글자 색상 HTML 태그 추가
- 색상 코드 참고표 작성

## 체크리스트
- [x] 코드 테스트 완료
- [x] 문서 업데이트
- [ ] 리뷰어 지정

## 관련 이슈
Closes #123
```

### 7.2 첫 번째 PR Merge (충돌 없음)

```bash
# 로컬에서 main으로 이동
git checkout main

# main 브랜치 업데이트
git pull origin main

# feature/add-colors 브랜치 Merge
git merge feature/add-colors

# 출력:
# Merge made by the 'recursive' strategy.
#  dummy_personal_data.md | 15 +++++++++++++++
#  1 file changed, 15 insertions(+)
```

### 7.3 원격 저장소에 Merge된 내용 Push

```bash
# main에 Merge된 내용 Push
git push origin main

# 확인
git log --oneline -5
```

### 7.4 두 번째 PR에서 Conflict 발생 시뮬레이션

```bash
# main 브랜치에서 feature/update-version을 Merge 시도
git checkout main
git pull origin main

git merge feature/update-version
```

**Conflict 발생 시 출력:**
```
Auto-merging dummy_personal_data.md
CONFLICT (content): Merge conflict in dummy_personal_data.md
Automatic merge failed; fix conflicts and then commit the result.
```

---

## 8. Merge Conflict 해결 방법

### 8.1 Conflict 상태 확인

```bash
# Conflict 상태 확인
git status

# 출력:
# On branch main
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#   (use "git merge --abort" to abort the merge)
# 
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#           both modified:   dummy_personal_data.md
```

### 8.2 Conflict 파일 내용 확인

```bash
# Conflict가 있는 파일 확인
cat dummy_personal_data.md

# 또는 VS Code 등 에디터에서 열기
```

**Conflict 마크업 예시:**
```markdown
<<<<<<< HEAD
# 개인정보 더미데이터 (v2.0)

현재 브랜치의 내용입니다.
=======
# 개인정보 더미데이터 (v3.0 FINAL)

병합할 브랜치의 내용입니다.
>>>>>>> feature/update-version
```

**마크업 설명:**
- `<<<<<<< HEAD`: 현재 브랜치(main) 내용 시작
- `=======`: 구분선
- `>>>>>>> feature/update-version`: 병합할 브랜치 내용 끝

### 8.3 Conflict 해결 - 방법 1: 수동 편집

```bash
# 에디터에서 파일 열기 (VS Code 권장)
code dummy_personal_data.md
```

**해결 전:**
```markdown
<<<<<<< HEAD
# 개인정보 더미데이터 (v2.0 업데이트)
=======
# 개인정보 더미데이터 (v3.0 FINAL VERSION)
>>>>>>> feature/update-version
```

**해결 후 (두 내용 모두 포함):**
```markdown
# 개인정보 더미데이터 (v3.0 FINAL VERSION)
```

또는

```markdown
# 개인정보 더미데이터 (v3.0 FINAL VERSION)

- v2.0: 초기 버전
- v3.0: 최종 버전 (검증 완료)
```

### 8.4 Conflict 해결 - 방법 2: Git 명령어 사용

**현재 브랜치 선택:**
```bash
# 모든 파일에서 현재 브랜치(HEAD) 버전 사용
git checkout --ours dummy_personal_data.md
```

**병합할 브랜치 선택:**
```bash
# 모든 파일에서 병합할 브랜치 버전 사용
git checkout --theirs dummy_personal_data.md
```

### 8.5 Conflict 해결 - 방법 3: VS Code Merge Editor 사용

VS Code에서 자동으로 제공하는 병합 UI 사용:

```
[Accept Current Change] [Accept Incoming Change] [Accept Both Changes] [Compare]
```

- **Accept Current Change**: HEAD 버전 유지
- **Accept Incoming Change**: 병합할 브랜치 버전 사용
- **Accept Both Changes**: 두 내용 모두 포함
- **Compare**: 변경사항 비교

### 8.6 Conflict 해결 - Merge 완료

```bash
# 파일 Staging (충돌 해결 표시)
git add dummy_personal_data.md

# 상태 확인
git status

# 출력:
# On branch main
# All conflicts fixed but you are still merging.
#   (use "git commit" to conclude the merge)
# 
# Changes to be committed:
#         modified:   dummy_personal_data.md
```

### 8.7 Merge Commit 생성

```bash
# Merge 커밋 생성
git commit -m "Merge branch 'feature/update-version' into main

Resolved conflict in dummy_personal_data.md
- 두 브랜치의 변경사항 통합
- v3.0으로 최종 확정"

# 또는 기본 메시지로 커밋
git commit
```

### 8.8 원격 저장소에 Push

```bash
# Merge 완료된 내용 Push
git push origin main

# 확인
git log --oneline -5
```

---

## 9. Merge 취소하기 (필요한 경우)

### 9.1 Merge 중단 (아직 커밋 전)

```bash
# Merge 취소
git merge --abort

# 또는
git reset --hard HEAD
```

### 9.2 Merge 커밋 취소 (이미 커밋함)

```bash
# 이전 커밋으로 되돌리기
git revert -m 1 <merge-commit-hash>

# 예시:
git revert -m 1 a1b2c3d

# -m 1: 병합된 브랜치의 첫 번째 부모(main)를 유지
```

---

## 10. 기타 유용한 Git 명령어

### 10.1 브랜치 관리

```bash
# 모든 로컬 브랜치 조회
git branch -a

# 원격 브랜치만 조회
git branch -r

# 브랜치 삭제 (로컬)
git branch -d feature/add-colors

# 강제 삭제
git branch -D feature/add-colors

# 원격 브랜치 삭제
git push origin --delete feature/add-colors
```

### 10.2 커밋 이력 조회

```bash
# 최근 5개 커밋 조회
git log --oneline -5

# 그래프 형태로 조회
git log --oneline --graph --all

# 특정 파일의 변경 이력
git log --oneline dummy_personal_data.md

# 커밋 상세 정보
git show <commit-hash>
```

### 10.3 변경사항 확인

```bash
# 인덱스(Staging)에 포함되지 않은 변경사항
git diff

# Staging된 변경사항
git diff --cached

# 특정 파일의 변경사항
git diff dummy_personal_data.md

# 두 브랜치 비교
git diff main feature/add-colors
```

### 10.4 커밋 수정

```bash
# 마지막 커밋 메시지 수정
git commit --amend -m "수정된 커밋 메시지"

# 마지막 커밋에 파일 추가
git add forgotten_file.txt
git commit --amend

# 이전 커밋으로 되돌리기
git revert <commit-hash>
```

---

## 11. Conflict 해결 체크리스트

Conflict 상황을 대비한 체크리스트:

```
[ ] git status로 현재 상태 확인
[ ] Conflict 파일 확인 (<<<<<<, =======, >>>>>>)
[ ] 에디터에서 파일 열기
[ ] 어느 변경사항을 유지할지 결정
[ ] Conflict 마크업 삭제
[ ] 파일 저장
[ ] git add로 해결 표시
[ ] git status로 상태 재확인
[ ] git commit으로 Merge 커밋 생성
[ ] git push로 원격에 반영
[ ] GitHub 웹사이트에서 최종 확인
```

---

## 12. 트러블슈팅

### 12.1 "fatal: unable to access repository"

**원인:** 인증 정보 오류

**해결:**
```bash
# 저장소 URL 확인
git remote -v

# URL 변경 (HTTPS → SSH 또는 반대)
git remote set-url origin git@github.com:username/my-project.git

# 또는
git remote set-url origin https://github.com/username/my-project.git

# 자격증명 다시 입력
git push
```

### 12.2 "Your branch is ahead of 'origin/main'"

**원인:** 로컬 커밋이 원격보다 앞서 있음

**해결:**
```bash
# 원격에 Push
git push origin main
```

### 12.3 "You have unmerged paths"

**원인:** 아직 Conflict이 해결되지 않음

**해결:**
```bash
# 1. Conflict 파일 확인
git status

# 2. 파일 편집하여 해결

# 3. Staging
git add .

# 4. Commit
git commit -m "Resolve merge conflict"
```

### 12.4 "Permission denied (publickey)"

**원인:** SSH 키 설정 누락

**해결:**
```bash
# HTTPS로 변경
git remote set-url origin https://github.com/username/my-project.git

# 또는 SSH 키 생성
ssh-keygen -t ed25519 -C "your.email@example.com"
# GitHub Settings > SSH and GPG keys에 공개키 추가
```

---

## 13. 권장 Git 작업 흐름 (Git Flow)

### 13.1 전체 작업 과정

```
1. main에서 브랜치 생성
   git checkout -b feature/new-feature

2. 기능 개발 및 커밋
   git add .
   git commit -m "feat: 새로운 기능 추가"

3. 원격에 Push
   git push -u origin feature/new-feature

4. GitHub에서 Pull Request 생성
   - base: main
   - compare: feature/new-feature

5. 코드 리뷰 및 승인

6. Merge
   - GitHub에서 "Merge pull request" 클릭
   - 또는 로컬에서 merge

7. 로컬 main 업데이트
   git checkout main
   git pull origin main

8. 불필요한 브랜치 삭제
   git branch -d feature/new-feature
   git push origin --delete feature/new-feature
```

---

## 📚 참고 자료

- **Git 공식 문서**: https://git-scm.com/doc
- **GitHub 가이드**: https://docs.github.com
- **Git 시각화**: https://git-school.github.io/visualizing-git/
- **Merge Conflict 가이드**: https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts

---

## 🎯 주요 포인트 정리

| 단계 | 주요 명령어 | 설명 |
|------|----------|------|
| **토큰 발행** | GitHub Settings | PAT 발행 및 보관 |
| **설정** | `git config --global` | 사용자 정보 등록 |
| **Clone** | `git clone <url>` | 저장소 다운로드 |
| **작업** | `git add`, `git commit` | 파일 수정 및 커밋 |
| **Push** | `git push origin main` | 원격에 업로드 |
| **브랜치** | `git checkout -b` | 새로운 브랜치 생성 |
| **Merge** | `git merge` | 브랜치 병합 |
| **Conflict** | 수동 편집 또는 `git checkout` | 충돌 해결 |

---

**작성일**: 2024년 3월 21일  
**버전**: 1.0  
**마지막 업데이트**: 2024년 3월 21일

<span style="color:green">✅ 이 가이드를 따라하면 GitHub 협업의 모든 과정을 완벽하게 이해할 수 있습니다!</span>
