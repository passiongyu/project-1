버전 

제품에는 버전이 있다. 

==결과물에 특정 부분에 어떤 유의미한 변화(추가, 변경, 삭제)가 일어나면 이것은 새로운 결과물이고 새로운 버전이 될 수 있다.==
버전관리를 하는 이유: 
유의미한 결과물은 버전으로 만들면 좋다. 
내 이전 코드내역이 버전으로 만들어져있으니 이전 코드내역 백업이 된다. 
버전이 있어야 되돌아가는 것도 가능하고 어떤 것이 추가되었는지 확인도 가능하고 이상이 있을 경우 되돌아갈 수도 있다. 그리고 버전의 변경사항을 여러 개발자가 같이 확인할 수 있어서 겹치게 개발한건 없는지도 확인 가능하고 협업이 가능하게된다. 

즉, 유의미한 변경이 일어나면 이것들을 버전으로 만들고 관리하면 좋다. 

버전이 되기까지 거쳐가는 세 개의 공간

- Working Directory(작업공간)	
  - Working Directory의 모든 변경사항들을 버전으로 만들기보다 버전이 될 파일들을 선별해서 선별된 파일들을 버전으로 만드는게 좋고 합리적이다.
- Staging Area
  - 버전이 될 후보들이 올라오는 공간 
  - Working Directory에서 선별 
- Repository


명령어: git <명령어>
깃 사용자 정보 등록
 전역 리포지토리
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
 현재 리포지토리만
  git config user.name "Your Name"
  git config user.email "you@example.com"
 
- git init: 특정 폴더에서 폴더 하위에 있는 것들을 버전관리하기 위한 초기화 명령어 (버전관리하겠다) 
  - 이제 부터 이 폴더의 버전을 관리할 수 있다. 
- git status: 버전관리되고 있는 폴더의 상태를 알려줘 , 변경된게 있는지 알려줘. 
  - untracked file: 버전관리 되고 있지 않은 파일 
  - change to be committed: staging area에 올라감. 
- git rm —cached <file> : 다시 스테이지에서 내리기. 
  - 추적 내역에서 제외한다. ex)node_modules같은거 잘못 추가했을 때 (단, 로컬에서는 삭제되지 않음) 
- git restore --staged <file> : 스테이징된 내용을 취소하고 이전 커밋 상태로 되돌려라. 
- git add 대상이름 : Working directory에서 변경사항이 있는 파일을 체크하고 그 파일들을 Staging Area 옮긴다. 
  - git add . : 현대 위치한 폴더에 있는 모든 변경사항있는 파일들을 Stage에 올려라. 
- git commit -m “커밋메시지” : Staging Area에서 Repository옮긴다. 버전이 만들어진다. 
  - 이 버전을 왜 만들었고 어떤 의미를 가지고 있는 버전인지 메시지로 써준다. 
- git commit -am “commit message” : add와 커밋을 동시에 하기 (단, 한번이라도 commit을 한 대상에 대해서만 가능. 
- git log: 지금까지 만들어진 커밋 내역 확인 
  - 커밋(버전)을 식별할 수 있는 문자열 등이 출력된다. 

gitbub에 push하기 
새 버전이 만들어진 곳에서
- git remote add origin <url> : 내 로컬 저장소에 원격저장소 정보를 추가한다.
  - origin은 원격저장소의 별칭이다. 
  - url은 원격 저장소의 주소이다. ex)https://github.com/mingyu/project.git
- git push -u origin master : 원격저장소 master에 push한다. 
  - 로컬 브랜치(mster)의 버전관리내역을 원격저장소(origin)에 업로드(push)하는 명령.

되돌리기 
HEAD는 현재 작업중인 브랜치/커밋 중 가장 최근 커밋을 가리킨다. 
^: 하나전으로 되돌리기 
- git reset —hard HEAD^: 하드모드 리셋. 커밋도 리셋되고 staging area, working directory모두 그전 커밋으로 리셋이 된다. 
- git reset —mixed HEAD^: 보통모드로 리셋. mixed생략가능. 커밋은 일단 리셋됨. staging area도 사라짐. working directory는 그대로 있음. 
- git reset —soft HEAD^: 커밋만 리셋됨. staging area, working directory는 그대로 남아있음. 

Branch
브랜치를 만들면 그 커밋의 파일버전 상태에서 가지가 뻗어나와서 새로운 작업단위로 버전관리 가능.
참고)마스터에서 최소 한번 커밋하고 브랜치 만들어야함. 
어떤 브랜치로 체크아웃 하는것에 따라 실제 로컬파일 현황도 달라진다. 

- git branch: 현재 branch 목록 보기 
- git branch <브랜치이름> : 새 브랜치 만들기 
- git checkout <브랜치이름> : 특정 브랜치로 체크아웃. 

어떤 브랜치를 어디로 합칠지도 정해야한다. -> 병합의 결과가 되는 브랜치로 체크아웃한다. 
-> 합치는 명령어를 쳐준다. 
- git merge <브랜치이름>: <특정브랜치이름>에서 작업한 내역을 현재 브랜치로 반영해주세요. 

diff명령어 
- git diff: 변경 내역들끼리의 비교 결과를 보여줍니다. 각 커밋들과의 비교를 위해 사용. 
- git diff <비교대상commit해쉬> <기준commit해쉬> : 비교대상 커밋에 비해 기준 커밋이 뭐가 달라졌는지 출력. 
- git diff <비교대상 branch이름> origin/<branch이름> : 원격 저장소와 로컬 저장소간의 비교 
- git diff HEAD HEAD^ : 현재 커밋과 그전 커밋과의 비교. 
- git diff HEAD: 현재 작업중인 수정된 내용과 이전 커밋한 내용과 비교 
- git diff <비교대상 branch이름> <기준 branch이름> 

revert명령어 
- git revert <되돌리고 싶은 commit>
  - 되돌리고 싶은 commit을 인자로 넣고 revert를 하면 그 커밋한 반대로 내역을 반영해주는 커밋을 생성. 
  - commit1 -> commit2 -> commit3 으로 커밋했으면 반대로 하나씩 revert해줘야함. 아니면 commit1이 했던 **변경 내용만 반대로 적용하는 새 커밋**이 생깁니다.
  - git revert HEAD~N..HEAD 최근 N개의 커밋 되돌리기 
git reset은 되돌린 버전 이후의 버전들이 모두 사라지게 되지만, git revert는 되돌린 버전 이후의 버전들은 모두 유지가 되고, revert되었다는 사실을 담은 commit이 새로 추가됨. 
ex)3번 commit으로 reset-> 4, 5번 커밋은 삭제되지만 3번 commit으로 revert를 하면 4, 5번 commit은 유지.  
안전한건 revert가 더 안전하고 깔끔하게 내역 관리하려면 reset을 사용. 



## 깃허브(원격 저장소)

사용이유: 
공유가능. 안전. 커뮤니티성. 
즉, 하나의 깃허브에 버전 관리를 동시에 하면 같은 버전상태를 공유할 수 있어서 어떤 변경사항이 추가되어서 버전이 어떻게 변했는지, 변경사항중에 겹치는게 있어서 충돌이 있는지 있으면 어떻게 병합해서 버전을 추가했는지 관리가 가능하다. 

원격저장소는 원격에 있는 또다른 repository라고 보면된다. 

==로컬 repository -> 원격 repository. 버전 내역들을 로컬에만 저장하는게 아니라 똑같이 원격 저장소에도 저장 및 반영== 
==로컬에 버전관리내역(.git)을 원격에 버전관리내역(.git)에 반영한다.== 

마치 내 로컬파일을 구글 클라우드 드라이브에 저장한 것과 유사하다. 

순서

내 local repository에서 변경을 하고 commit을 하여 새 버전을 만들면 ->
push를 통해 remote repository 버전에 반영을 한다. 

Repository끼리의 상호작용 종류
- git remote: 원격저장소 조회(추가)하기: 
  - git remote (-v): 내 로컬 repository와 상호작용하고 있는 원격 저장소들의 목록을 조회.
  - git remote add origin <url>: <url>에 있는 원격 저장소를 origin이라는 이름으로 추가하기. 
  - git remote rm prac2: 원격저장소 prac2지우기. 
- git push: 원격저장소에 밀어넣기
  - git push -u origin master: 내 repository의 master브랜치를 origin의 master브랜치로 push해라 -u는 디폴트 설정. -> 다음부터는 git push만 해도 되도록. 
  - git push origin new-branch2:feature-1 -> 원격origin의 feature-1브랜치에다가 내 로컬 new-branch2를 push하기. 
- 원격저장소 갖고 와서 합치기: git pull
  - git pull (origin master): origin을 내 repository의 master 브랜치로 갖고와라(merge)(동기화)
  - 만약 충돌이 나면 충돌났다고 로컬파일에 표시가 된다. 
  - repository들끼리는 서로 pull request를 날린다. 그리고 local repository와 원격 repository를 pull 했는데 충돌이 나면 병합해서 새 버전으로 merge된다. 
  - 사실상 git fetch + git merge
![](image.png)<!-- {"width":540} -->
이렇게 repository끼리 버전이 다르면 fast-forward merge가 일어나지 않고 새로운 merge commit이 일어나다. 또 하나 눈여겨 볼 것은 repository들, branch들은 저렇게 버전 사슬을 한 줄씩 가지고 있다. 그리고 서로 버전을 만들면서 상호작용한다. 

- 원격저장소 일단 갖고만 오기: git fetch
  - git fetch (origin master): 동기화시키지는 말고(로컬저장소를 변화시키진 않고) (merge하지는 말고) origin을 내 repository의 master브랜치로 일단 갖고 와라. 
  - 이후 git checkout origin/master 해본다. (or git checkout FETCH_HEAD) 그러면 fetch한 내용을 확인할 수 있는 브랜치로 이동한다. 그리고 로컬에서 파일을 확인해본다. 
- 원격저장소 복사하기 : git clone
  - git clone <url> : <url>에 있는 원격 저장소 내용을 현재 디렉토리에 복사해오기(origin 자동 생성) 단, 그 폴더에 하위에 원격저장소 폴더가 생긴다.

## Branch로 알아보는 git의 협업 원리

작업단위(Branch)로 나눈다. -> 각자 작업한다. -> 합친다. 


## 협업의 세 가지 시나리오
- 내 로컬 저장소는 변했는데 원격 저장소는 변함 없는 경우 -> push
- 내 로컬 저장소는 변함없는데 원격 저장소는 변한 경우 -> pull로 동기화 후 push하기 
- 내 로컬 저장소도 변했는데 원격 저장소도 변한 경우 
  - 기여하고 싶은 프로젝트를 내 계정으로 fork한다.
  - 내 로컬 repository로 clone해온다. 
  - 로컬repository에서 브랜치를 새로 생성해주고 체크아웃해준다. 
  - 코드 수정한다. 
  - 커밋하고 그 브랜치를 내 계정으로 push한다. 
  - 내 계정에서 pull request버튼으로 pull request를 날린다. 
  - 원본 주인이 merge한다. 
  - pull request날린 branch는 지워준다. git branch -d newbranch


rebase: 합치고자 하는 branch의 최신 commit으로 base를 옮긴다. -> 머지 커밋이 생기지 않는다. 
