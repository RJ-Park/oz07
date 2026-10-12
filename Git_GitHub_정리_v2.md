# Git & GitHub 요점 정리 v2 — GitHub 사용하기

## 1. GitHub 접속과 내 페이지

1. [github.com](https://github.com) 접속 → **Sign in**으로 로그인
2. 로그인 후 첫 화면이 **대시보드(Dashboard)**: 내 저장소 목록, 최근 활동이 보임
3. 오른쪽 위 **프로필 사진 → Your profile**을 누르면 내 페이지(`github.com/아이디`)로 이동
   - **Repositories** 탭: 내가 만든 저장소 목록
   - 커밋한 날이 초록색 칸으로 표시되는 **기여 그래프(잔디)** 도 여기서 확인
4. 새 저장소 만들기: 오른쪽 위 **+ → New repository**

---

## 2. GitHub에 올리는 이유

| 이유 | 설명 |
|---|---|
| **작업 기록 관리** | Git으로 남긴 커밋 기록을 그대로 온라인에 보관 → 컴퓨터가 고장 나도 기록이 남음 |
| **어디서든 코드 공유** | 집·학원 등 여러 곳(여러 컴퓨터)에서 작업해도 같은 저장소로 코드를 주고받을 수 있음 |
| **과정까지 공유** | 코드 파일만 주고받으면 **최종 결과물만** 넘어가지만, GitHub로 공유하면 **전체 작업 내역과 커밋**까지 확인 가능 |
| **사용 내역 확인** | 누가 언제 무엇을 바꿨는지, 코드와 Git 사용 내역을 웹에서 손쉽게 확인 |
| **오픈소스 공유** | 내가 만든 코드를 오픈소스로 공개하고, 다른 사람의 오픈소스에 기여 가능 |

> 💡 코드 파일만 보내면 "결과", GitHub로 공유하면 "결과 + 과정"이 함께 감.

---

## 3. README에 적는 것들

`README.md`는 저장소에 들어오면 가장 먼저 보이는 **프로젝트 소개서**.

**주로 적는 내용**

- 프로젝트 이름과 한 줄 설명
- 진행 기간
- 주요 기능
- 사용 기술(언어, 라이브러리)
- 설치·실행 방법
- 폴더 구조
- 만든 사람 / 연락처

```markdown
# OZ coding school AI BootCamp
## Git & GitHub Example
- Dates: 26. 10. 06 ~ 26. 10. 08
```

### GitHub의 README 자동 생성을 쓰지 않는 이유

저장소를 만들 때 **Add a README file**을 체크하면, GitHub 쪽 저장소에 **첫 커밋이 생성됨.**
그런데 내 컴퓨터에서 `git init`으로 따로 시작한 저장소에도 별도의 커밋이 있기 때문에, 두 저장소의 기록이 **서로 관련 없는 기록**이 되어 push가 거절됨.

```
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/...'
```

> ✅ 로컬에서 만든 저장소를 올릴 때는 **빈 저장소**(README, .gitignore, license 모두 체크 해제)로 만들고, README는 로컬에서 작성 후 업로드.

---

## 4. 로컬 저장소를 원격 저장소에 연결하기

### Quick setup에 나오는 주소의 의미

빈 저장소를 만들면 **Quick setup** 화면이 나오고, 그 안에 `https://github.com/아이디/저장소이름.git` 형태의 주소가 있음.

- 이 주소가 **원격 저장소의 위치(URL)** 임.
- 내 컴퓨터의 Git에 "이 주소로 올리고 받아라"라고 알려줄 때 사용함.
- HTTPS 주소와 SSH 주소 두 가지 방식이 있으며, 수업에서는 HTTPS를 사용.

### 연결 순서 (VS Code 터미널)

Quick setup의 **"…or push an existing repository from the command line"** 부분을 그대로 사용 가능.

```bash
# 0. 프로젝트 폴더에서 (처음 한 번만)
git init

# 1. 원격 저장소 주소를 origin이라는 이름으로 등록
git remote add origin https://github.com/아이디/저장소이름.git

# 2. 현재 브랜치 이름을 main으로 변경 (master로 만들어진 경우 대비)
git branch -M main

# 3. main 브랜치를 origin에 올리고, 앞으로 기본 업로드 위치로 설정
git push -u origin main
```

- **`origin`**: 원격 저장소 주소에 붙이는 **별명**. 이름은 자유지만 관례적으로 `origin`을 사용
- `git remote -v`: 연결된 원격 저장소 이름과 주소 확인
- `-u`: 한 번 설정해 두면 다음부터는 `git push`, `git pull`만 입력해도 됨

---

## 5. Clone과 Fork의 차이

| | **Clone** | **Fork** |
|---|---|---|
| 복사 위치 | 원격 저장소 → **내 컴퓨터(로컬)** | 다른 사람의 저장소 → **내 GitHub 계정** |
| 하는 곳 | 터미널: `git clone 주소` | GitHub 웹: 저장소 오른쪽 위 **Fork** 버튼 |
| 권한 | 원본 저장소에 **push 권한이 있을 때** | 원본 저장소에 **push 권한이 없을 때** |
| 주 용도 | 팀 내부 협업, 내 저장소를 다른 컴퓨터로 가져오기 | 오픈소스 기여 → Pull Request로 반영 요청 |

```bash
# Clone: 원격 저장소 전체(파일 + 커밋 기록)를 로컬로 복사, origin 자동 연결
git clone https://github.com/아이디/저장소이름.git

# Fork 후에는 내 계정의 포크를 clone하고, 원본 저장소를 upstream으로 추가
git clone 내_포크_저장소_URL
git remote add upstream 원본_저장소_URL
```

> 💡 Fork는 GitHub 안에서의 복사, Clone은 GitHub → 내 컴퓨터로의 복사. 보통 **Fork 후 Clone**으로 같이 씀.

---

## 6. Fetch란?

**`git fetch`**: 원격 저장소의 최신 변경 내역을 **가져오기만 하고, 내 작업 파일에는 합치지 않는** 명령어

```bash
# 원격의 최신 커밋·브랜치 정보 가져오기
git fetch origin

# 원격에만 있는 커밋 확인
git log --oneline main..origin/main

# 확인 후 내 브랜치에 합치기
git merge origin/main
```

| | `git fetch` | `git pull` |
|---|---|---|
| 하는 일 | 원격 내용을 **가져오기만** 함 | 가져온 뒤 **바로 합침** |
| 내 파일 변화 | 없음 (`origin/main`만 갱신) | 있음 |
| 관계 | — | **`git pull` = `git fetch` + `git merge`** |

> 💡 "다른 사람이 뭘 올렸는지 먼저 보고 합치고 싶을 때"는 fetch, "바로 최신으로 맞추고 싶을 때"는 pull.

---

## 7. main에서 작업한 내역 올리기

```bash
# 1. 바뀐 파일 확인
git status

# 2. 올릴 파일 스테이징
git add .

# 3. 커밋(버전 기록)
git commit -m "Add login page"

# 4. GitHub의 main에 업로드 (-u 설정했다면 git push)
git push origin main
```

- push 전에 다른 사람이 main에 먼저 올렸다면 push가 거절됨 → `git pull`로 받은 뒤 다시 push
- 팀 프로젝트에서는 main에 바로 올리지 않고 **브랜치 → push → Pull Request**로 올리는 것이 일반적.

---

## 8. GitHub와 로컬의 파일 개수가 다른 이유

내 폴더에는 있는데 GitHub에는 없는 파일이 생기는 대표적인 이유

| 이유 | 설명 |
|---|---|
| **`.gitignore`로 제외한 파일** | `.env`, `.DS_Store`, `__pycache__/` 등은 Git이 추적하지 않으므로 올라가지 않음 |
| **숨김 폴더 `.git`** | 로컬에만 있는 Git 데이터베이스. GitHub에 파일로 올라가지 않음 |
| **아직 add·commit하지 않은 파일** | push는 **커밋만** 올리므로, 커밋하지 않은 새 파일·수정 내용은 올라가지 않음 |
| **커밋은 했지만 push하지 않음** | 로컬에만 커밋이 쌓여 있는 상태 (`git status`에서 "앞에 있습니다"로 표시) |
| **빈 폴더** | Git은 파일만 추적하므로 내용이 없는 폴더는 올라가지 않음 |
| **보고 있는 브랜치가 다름** | GitHub는 기본으로 main을 보여 줌. 다른 브랜치에 올린 파일은 브랜치를 바꿔야 보임 |

**실제 예시 (oz07 저장소)**

```
로컬 폴더                GitHub
.env          ← .gitignore로 제외 → 없음
.DS_Store     ← .gitignore로 제외 → 없음
.git          ← 로컬 전용         → 없음
.gitignore                         .gitignore
README.md                          README.md
first.txt ...                      first.txt ...
```

---

## 9. 공개 저장소에 올리면 안 되는 것들

Public 저장소는 **전 세계 누구나** 볼 수 있음.

| 종류 | 예시 |
|---|---|
| **비밀 정보** | API 키, 비밀번호, 토큰, DB 접속 정보 → 보통 `.env`에 보관하고 `.gitignore`로 제외 |
| **개인정보·민감 데이터** | 이름, 연락처, 주민번호, **환자 데이터·의료 영상** 등 |
| **용량이 큰 파일** | 원본 데이터셋, 학습된 모델 가중치, 압축 파일 (GitHub는 100MB 넘는 파일을 거부) |
| **자동 생성 파일** | `__pycache__/`, `venv/`, `node_modules/`, 빌드 결과물, `*.log` |
| **개인 환경 파일** | `.DS_Store`, 에디터 설정 폴더(`.vscode/` 등) |
| **저작권이 있는 자료** | 강의 자료 원본 등 공유 허락을 받지 않은 파일 |

```gitignore
# .gitignore 예시
.env
.DS_Store
__pycache__/
venv/
*.log
data/
```

> ⚠️ 비밀 정보를 실수로 올렸다면 파일을 지우고 다시 커밋해도 **이전 커밋 기록에 남아 있습니다.** 해당 키나 비밀번호는 즉시 폐기하고 새로 발급받아야 함.

---

## 10. 커밋하지 않고 push하면 나오는 메시지

파일을 수정만 하고(또는 add만 하고) **커밋하지 않은 채** push하면 다음 메시지가 나옴.

```
$ git push origin main
Everything up-to-date
```

**이유**: `git push`는 작업 중인 파일이 아니라 **커밋을 올리는** 명령어. 새 커밋이 없으니 "GitHub와 이미 같은 상태(올릴 게 없음)"라고 알려주는 것. 수정한 파일은 여전히 로컬에만 있음.

```bash
# 해결: 커밋을 먼저 만든 뒤 push
# Changes not staged / Changes to be committed 확인
git status
git add .
git commit -m "Update README"
git push origin main
```

**참고: 저장소에 커밋이 하나도 없을 때 push하면**

```
error: src refspec main does not match any
error: failed to push some refs to 'https://github.com/...'
```

`git init`만 하고 첫 커밋을 안 했거나 브랜치 이름이 다를 때 나옴. 올릴 `main` 브랜치(커밋)가 아직 없다는 의미로, 첫 커밋을 만들거나 `git branch -M main`으로 이름을 맞춰야 함.

---

## 11. GitHub 협업 기능

| 기능 | 설명 |
|---|---|
| **Collaborator** | Settings → Collaborators에서 팀원을 초대하면 같은 저장소에 push 가능 |
| **Branch protection rules** | main에 바로 push하지 못하게 막고, **PR을 거쳐야만** 병합되도록 설정 (Require a pull request before merging) |
| **Pull Request (PR)** | 내 브랜치의 변경 사항을 main에 반영해 달라고 요청. 변경 내용 설명, 리뷰 요청, 병합 전 검증 단계 |
| **Code Review** | 병합 전에 팀원이 코드를 확인하고 코멘트·승인. 버그 예방, 코드 품질 유지, 팀 규칙 공유 |
| **Issue** | 할 일, 버그 리포트, 기능 요청을 기록·관리. PR에 `Resolve #번호`를 적어 연결 |
| **Fork** | push 권한이 없는 저장소에 기여할 때 내 계정으로 복사해서 작업 후 PR |

**Collaborator 방식 협업 흐름**

```bash
# 1. 코드 가져오기
git clone 원본_저장소_URL

# 2. 내 작업 브랜치 생성
git switch -c feature/mybranch
git add .

# 3. 작업 후 커밋
git commit -m "Add my feature"

# 4. 원격에 내 브랜치 올리기
git push origin feature/mybranch
# 5. GitHub에서 feature/mybranch → main 으로 Pull Request 생성
# 6. 리뷰·승인 후 Merge
```

---

## 12. 협업자의 작업물을 내 로컬에 반영하는 방법

### 1) main에 병합된 내용 받기 (가장 기본)

```bash
git switch main

# = git fetch + git merge
git pull origin main
```

### 2) 먼저 확인하고 합치기

```bash
git fetch origin

# 새로 올라온 커밋 확인
git log --oneline main..origin/main
git merge origin/main
```

### 3) 협업자의 브랜치를 내 컴퓨터에서 직접 보기 (PR 리뷰할 때)

```bash
git fetch origin

# 원격 브랜치와 같은 이름의 로컬 브랜치가 자동 생성됨
git switch feature/팀원의브랜치
```

### 4) Fork 방식일 때 원본 저장소의 최신 코드 받기

```bash
git pull upstream main
```

### 5) 내 작업 브랜치에도 최신 main 반영하기

```bash
git switch feature/mybranch
git merge main
```

> 💡 **작업 시작 전 `git pull`** 을 습관으로 하면 충돌이 크게 줄어듦.