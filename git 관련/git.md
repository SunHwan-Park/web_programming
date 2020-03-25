# git

> 분산 버전관리시스템(DVCS)

## 기초 명령어

### 저장소 생성

* init

```bash
~/Desktop/git
$ git init
Initialized empty Git repository in C:/Users/multicampus/Desktop/git/.git/
~/Desktop/git (master)
$ git init
```

### 버전 관리

```bash
$ git status
On branch master

# commit이 아직 없다. (버전이력이 없다.)
No commits yet

# Untracked files -> 현재 버전에 등록되어있지 않은 파일
Untracked files:
	# 커밋될 곳에 포함시키려면(staging area) add 명령어를 써.
  (use "git add <file>..." to include in what will be committed)
        a.txt

# 정리멘트 - 커밋 할 것도 없고, 다만 새로 생긴 파일은 있어.
nothing added to commit but untracked files present (use "git add" to track)

```

```bash
$ git add .
$ git status
On branch master

No commits yet

# 커밋 될 변경 사항
Changes to be committed:
	# unstage하려면 아래의 명령어를..
  (use "git rm --cached <file>..." to unstage)
        # 새로운 파일 a.txt 입니다.
        new file:   a.txt
```

```bash
$ git commit -m 'Init'
[master (root-commit) ebd83a4] Init
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
 
$ git status
On branch master
# 커밋할 것 없고, 작업 공간도 깨-끗.
nothing to commit, working tree clean

$ git log --oneline
ebd83a4 (HEAD -> master) Init
```

### 원격 저장소

* 원격 저장소 등록

  * git아, 원격저장소에(remote) 추가해줘(add) origin이라는 이름으로 url을

  ```bash
  $ git remote add origin {url}
  ```

  ```bash
  $ git remote -v
  ```

* push

  ```bash
  $ git push origin master
  ```


* pull

  ```bash
  $ git pull origin master
  ```

  

### 원격 저장소 복제

```bash
$ git clone {url}
```

* clone 명령어는 pull의 역할을 하는 것이 아니라 init의 역할을 하는 것
  * 로컬에서 저장소를 초기화 하는 방법
    * `git init` - 특정 폴더를 저장소로 활용
    * `git clone` - 특정 원격 저장소를 복제

<img src="images/git.png" alt="git" style="zoom:60%;" />