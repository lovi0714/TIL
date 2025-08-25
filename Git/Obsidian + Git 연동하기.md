
#### 0. Git 이 설치되어있다는 가정 하에 진행한다.

> 설치 확인 : git --version


#### 1. Github에 레포지토리 생성

+ 원하는 이름으로 레포지토리를 생성한다. ex) TIL
+ public / private는 원하는대로 진행한다.

#### 2. Obsidian에서 Vault 열기 (작업 대상 폴더 열기)

+ Obsidian에서 작업 대상 폴더를 열어준다.
+ cmd나 git bash를 통해 해당 경로로 이동한다.

```bash

# 1
git init # 깃 초기화

# 2
git remote add origin 1번에서 생성한 원격주소 입력 # 원격 레포 연결

# 3
#(선택 사항 / .gitignore 생성, 경로는 Vault 루트)

# OS 잡파일
.DS_Store
Thumbs.db
desktop.ini

# Obsidian 캐시 및 로컬 상태
.obsidian/cache/
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.trash/

# 4
git add . # 모두 스테이징

# 5
git commit -m "init" # 최초 커밋

# 6
git push -u origin main # 원격 브랜치에 푸쉬


## github 인증 설정
# 나는 Git Credential Manager 활성화 설정을 통해 로그인해서 진행했다.
git config --global credential.helper manager # 팝업창이 뜸


```

#### Obsidian git 플러그인 설정

+ 설정 -> 커뮤니티 플러그인 -> git 검색하여 설치 및 활성화
+ 자동 동기화 설정도 있는데, 개인적으로는 불호여서 터미널 대신 GUI로 `commit`, `push` 하려고 설치했다.
