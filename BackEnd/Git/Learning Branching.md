# Learning Branching

https://learngitbranching.js.org/

## 메인
### # git 기본
1. Git 커밋 소개
    - 커밋은 Git 저장소에 파일에 대한 스냅샷을 기록합니다. 
        - 디렉토리 전체를 복사하거나 변경분만 저장하는 것이 아닙니다.
    - 커밋은 부모 커밋을 가리킵니다.
        - delta : 이전 버전과 다음 버전의 변경 내역
          
2. Git 에서 브랜치 쓰기
    - branch 는 특정 커밋에 대한 참조로 하나의 커밋과 그 부모 커밋들을 포함하는 작업 내역입니다. 

3. Git 에서 브랜치 합치기(Merge)
    - Git 의 merge 는 두 개의 parent 를 가리키는 특별한 커밋을 만들어 냅니다. 
        - 한 부모의 모든 작업내역과 나머지 부모의 모든 작업, 그리고 그 두 부모의 모든 부모들의 작업내역을 포함합니다.
    - `master > git merge bugfix`
    master branch 에서 실행하며 bugfix branch 를 master branch 로 merge 합니다.

4. 리베이스(rebase)의 기본
    - branch 의 head 를 이동시키는 것으로 merge 보다 강력하고 간결하지만 잘못된 작업시 복구가 어려울 수 있습니다.
    - `bugfix > git rebase master`
    bugfix branch 에서 실행하며 bugfix branch 를 master branch 의 다음으로 rebase 합니다.
    

### # 다음 단계로
1. HEAD 분리하기
    - head 는 현재의 branch 에서 마지막에 작업한 곳을 가르킵니다.
    - checkout 명령어를 통해 head 의 조작이 가능하며 commit hash 값으로의 이동도 가능합니다.
    
2. 상대 참조
    - 한번에 한 커밋 위로 움직이는 `^ (캐럿)` 
    - 한번에 여러 커밋 위로 올라가는 `~<num> (틸드)`
    
3. Git에서 작업 되돌리기
    - git reset
        - 마치 애초에 커밋하지 않은 것처럼 history 를 고쳐 예전 커밋으로 브랜치를 옮기는 것입니다. 
        - history 가 고쳐짐으로 Local 에서 주로 사용 합니다.
        - `C0 - C1 - C2(*)` -> `C0 - C1(*)`
    - git revert
        - 변경분을 되돌리고 새로운 커밋을 합니다. 
        - 주로 커밋을 공유하는 상황에서 사용합니다.
        - `C0 - C1 - C2(*)` -> `C0 - C1 - C2 - C2'(*)`

### # 코드 이리저리 옮기기
1. Cherry-pick 소개
    - 현재 위치(HEAD) 아래에 있는 일련의 커밋들에 대한 복사본을 만드는 것입니다.
    
2. 인터랙티브 리베이스 소개
    - `rebase -i` 옵션을 통해 여러개의 커밋을 조작할 수 있습니다.
    - `rebase -i master~4`

### # 종합선물세트
- `rebase -i` 또는 `cherry-pick` 을 통해 가능합니다.
- `commit --amend` 로 커밋 메세지를 수정할 수 있습니다.
1. 딱 한개의 커밋만 가져오기
2. 커밋들 갖고 놀기
3. 커밋 갖고 놀기 #2
4. Git 태그
    - `git tag tagName branchName`
5. Git describe(묘사)
    - `git describe branchName`
    - 가장 가까운 tag 로 부터의 거리를 출력합니다.

### # 고급 문제
1. 9천번이 넘는 리베이스
    - 다른 branch 에서의 rebase 는 새로운 commit 을 만듭니다.
    - 같은 branch 에서의 rebase 는 새로운 commit 을 만들지 않습니다.

2. 다수의 부모
    - 한번에 한 커밋 위로 움직이는 `^ (캐럿)` 을 사용할 때 merge 로 인해 다수의 부모가 있는 경우 `^2` 를 이용함으로서 다른 부모를 선택할 수 있습니다.
    - 명령어를 합칠 도 있습니다.  
    `git checkout HEAD~^2~2`

3. 브랜치 스파게티
       
## 원격
### Push & Pull -- Git 원격 저장소!
1. Clone 소개
2. 원격 브랜치(remote branch)
3. 
4. 
5. 
6. 
7. 
8. 
    
### "origin"그 너머로 -- 고급 Git 원격 저장소
1. 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
    


