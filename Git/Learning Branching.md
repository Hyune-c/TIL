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

|                                             | git reset                                                    | git revert                                       |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------ |
| 설명                                        | 마치 애초에 커밋하지 않은 것처럼 history 를 고쳐<br />예전 커밋으로 브랜치를 옮기는 것입니다. (Local) | 변경분을 되돌리고 새로운 커밋을 합니다. (Remote) |
| 실행 후 커밋 히스토리 <br />C0 - C1 - C2(*) | C0 - C1(*)                                                   | C0 - C1 - C2 - C2'(*)                            |

### # 코드 이리저리 옮기기

### # 종합선물세트

### # 고급 문제

