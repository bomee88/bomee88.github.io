---
title : "[패스트캠퍼스 수강 후기] 프론트엔드 인강 100% 환급 챌린지 3회차 미션 - 24강 Git & Github (GUI 소스트리)"
date : 2020-08-12
categories : pastcampus 
tags : fastcampus all-in-one-challenge day3 git github GUI sourcetree
---
# 소스트리란 무엇인가?
보통 git과 github를 사용하려면 커맨드창 (까만창)에서 작업해야 한다. 일일이 명령어를 외워야 푸쉬, 풀, 클론등이 가능했는데 이런 번거로움을 줄이고 비주얼적으로 버튼만 누르면 이런 기능들이 가능하게끔 프로그램으로 만들어 놓은 것이 소스트리이다. 게다가 변경된 사항도 비주얼적으로 표시해서 보여줘서 버전을 비교해보기에도 아주 유용하다.
   
# Git GUI 소스트리로 알아볼 내용
1. 소스트리로 로컬 저장소 추가
1. add / commit 에 대해 stage개념과 함께 이해
1. branch로 평행세계 나누기
1. merge로 두개의 branch 합치기
1. 두 branch가 충돌(Conflict)났을 때 해결
1. 예의바른 병합요청 (Pull request) 보내기
1. 남의 저장소 통째로 복사하기 (Fork)
   
# 소스트리 설치 및 확인
[소스트리 설치](https://www.sourcetreeapp.com/) <- 소스트리 사이트로 가서 다운로드 받고 실행 시켜준다.
설치하면서 가입과 로그인을 동시에 진행한다. 소스트리 패널에 내가 작업하고있는 폴더를 끌어 넣으면 히스토리를 바로 볼 수 있다. 
   
# 소스트리로 보는 git의 상태 
git으로 추적하는 파일의 4가지 상태
- untracked
    * 추적안됨
- tracked
    * 수정없음
    * 수정함
    * 스테이지 됨   

작업공간에 있는 `수정함`, `추적안됨` 파일을 스테이지로 올려 `스테이지됨` 으로 변경한다.   

커밋을 하면 `수정없음` 상태로 돌아가서 다시 파일을 수정할 수 있다.   
![step1](/images/200808-1.png)
![step2](/images/200808-2.png)
![step3](/images/200808-3.png)
![step4](/images/200808-4.png)
![step5](/images/200808-5.png)
![step6](/images/200808-6.png)
![step7](/images/200808-7.png)


# 소스트리에서 origin, master의 의미 
>`origin`없이  `master`만 있는 것 : 내컴터에만 있는 것.   
>`origin`, `master` 둘다 있는 것 : 깃헙과 내컴터에 모두 있는 것.   

`master`만 있을 경우 상단에 `push`를 눌러서 origin에 올려준다. 

  
# branch 하기
### branch 란?
여러명이서 한 프로젝트를 작업하면 같은 소스를 동시에 수정할 수도 있다. 이럴 경우 가지를 나눠서 각자 갈라지는 것이다. 이 갈라져 나간 각자의 버전은 `브랜치`라고 부른다. 중심에 있는 브랜치는 `마스터브랜치`로 불리고 이것을 기점으로 a 브랜치, b 브랜치로 나누어졌다가 둘 중 버그 없는 (원하는) 브랜치를 마스터 브랜치로 합치면서 버전을 업데이트 해나간다.
### branch 하기
- CLI에서는 간단하게 아래와 같이 써주면 된다.   
    ```
    git branch
    ```
- GUI(소스트리)에서는 branch버튼을 클릭한다.
    > 브랜치를 만들때 이름을 feat/main_page이런 식으로 폴더명을 지정해서 만들어주면 소스트리에서 브랜치를 볼때 폴더별로 볼 수 있어 편리하다.
- 파일을 수정하고 브랜치 안에서 커밋하고 업데이트 해준다. 
- 히스토리에 돌아와서 보면 마스터브랜치보다 새로 만든 브랜치가 최신으로 업데이트 되어 있는게 보인다. 

# Merge 하기
- 마스터브랜치에 합치고 싶은 거라면 마스터브랜치로 이동해서 새로 만든 a브랜치를 합치겠다고 알려주면 된다.
- 소스트리에서는 간단하게 왼쪽 목록에서 마스터브랜치로 들어가고 히스토리에서 원하는 브랜치의 버전을 오른클릭 한 뒤 `병합`을 눌러주면 된다.
- 이제 상단에 `푸시`버튼을 눌러 마스터 브랜치에 푸시해준다. 
### Conflict (충돌)이 났다면?
두 버전이 같은 곳을 수정했다면 충돌이 난다. 이럴땐 이를 수동으로 고쳐줘야 한다. 고친 뒤에 다시 커밋하고 병합하면 된다. 
### VSC에서도 git GUI가 있다
VSC에서 아래 사진과 같은 곳을 눌러보면 git상태가 나온다. 또 하단에 지금 master 이라고 있는 부분 보면 현재 어떤 브랜치에 위치하고 있는지 상태도 나오고 클릭하면 브랜치를 이동할 수도 있다!
![step7](/images/200808-8.png)

# Fork 하기
저장소를 통째로 복사하는 방법은 Fork이다. 그렇다면 브랜치랑 포크랑은 서로 어떻게 다를까?

### Branch와 Fork의 다른점
|  | Branch | Fork | 
| :---: | :--- | :--- |
| 의의 | 하나의 원본 저장소에서 분기를 나눈다| 여러 원격 저장소를 만들어 분기를 나눈다 |
| 편리한점 | 하나의 원본저장소에서 코드 커밋 이력을 편하게 볼 수 있다 | 원본저장소에 영향을 미치지 않으므로 마음껏 코드를 수정할 수 있다. |
| 불편한점 | 다수의 사용자가 다수의 브랜치를 만들면 관리하기 힘들다. | 원본저장소의 이력을 보려면 따로 주소를 추가해줘야 한다. |

두가지 모두 코드 협업을 위해 분기를 나누는 방식이지만 특성이 각기 다르므로 프로젝트에 맞게 사용하면 된다. 

### Fork 하기
- 원하는 깃헙에 소스가 있다면 접속해서 우측 상단 Fork버튼을 클릭한다. 
- 내 레포지토리에서 URL을 복사해 와서 소스트리에서 clone버튼을 누르고 URL주소를 붙여넣고 로컬 폴더를 선택한 다음 받아온다.
- VSC에서 로컬폴더에 복사한 폴더를 연다. 
- 수정을 한다.
- 소스트리에서 커밋/푸시를 한다.(권한을 받은 경우)
- 권한을 주는 법은 Collaborator 하는 방법과 동일(github -> Settings -> Collaborators -> Add Collaborator)

# Pull Request 하기
### Pull Request란?
포크한 저장소에서 기능개발을 마친 경우 원본 저장소에 코드를 올리고 싶을때 '이 커밋과 저 커밋을 합치는 걸 허락해줘' 라고 요청을 보내는 것이 `풀 리퀘스트`이다. 

### Pull Request 하는 방법
1. 머지하고 싶은 두 브랜치 선택
1. 어떤 변경을 했는지 제목과 내용 서술
1. 단일 저장소에 보낼 수도 있고, 포크한 저장소에서도 보낼 수 있다.
1. (base는 머지를 당할 대상, compare는 새로 만든 대상)
   
- 코드를 함께 작성하는 팀원이 있다면, 직접 머지는 피하고 모든 머지를 풀 리쿼스트를 통해서 한다.
- 동료가 내 풀 리퀘스트(PR)을 보고 코드리뷰할 수 있다.
- 동료의 PR에 수정이 필요하면 댓글을 달아 Change Request할 수 있다. 
- 오픈소스 PR을 보낼때는 '기여 안내문서(Contribution Guideline)'을 반드시 참고해야한다.

# Branch 관리하는 팁
- 보통 `feat/버그이름` 으로 **한 사람이 개발하는 기능 브랜치**를 만든다. (`fix/버그이름`, `hotfix/급한버그`)
- 작업이 끝나면 `dev` (혹은 `master`) 브랜치로 PR을 보낸다.
- `dev` 브랜치에서 큼지막한 작업이 모두 머지되면 `release`(혹은 `latest`) 브랜치로 머지시키고 이를 **실서버에 배포**한다.
- 직접 커밋은 feat(혹은 fix, hotfix)브랜치에만 한다.
- dev나 master, release 브랜치에는 **직접 커밋하지 말고 머지만** 한다.

# Git 더 알아볼 기능들
1. rebase : 묵은 커밋을 새 커밋처럼 조작하고 싶을 때
1. amend : 깜박하고 수정 못 한 파일이 있을때 방금 만든 커밋에 살짝 추가하는 것
1. cherry-pick : 저 커밋에서 하나만 떼서 지금 브랜치에 붙이고 싶을 때
1. reset : 옛날커밋으로 시간을 돌리고 싶을 때, 과거로 강제 커밋
1. reverse : 이 커밋의 변경사항을 되돌리고 싶을 때 (히스토리를 날리지 않고 특정 사항만 되돌리는 명령)
1. stash : 변경 사항을 잠시 킵해두고 아직 커밋은 안만드는 상태

# 마치면서
소스트리 GUI 너무 좋다. 이렇게 눈에 보이니까 정말 쉽고 직관적이고 간단하고 이해가 잘된다. 그동안 CLI로 명령어 수십번 썼다 지웠다 반복했던 내가 바보처럼 느껴질 정도..ㅎㅎㅎ 아무튼 눈에 보이지 않는 git의 개념을 차근차근 문어와 고양이로 섬세하게 설명해주신 진유림 강사님께 소소한 감사의 인사를 올린다.😌
   
오늘은 여기까지, 수강 모습은 아래에..
(오늘 시청영상 24강 09~17까지)
![수강인증이미지](/images/200808-9.jpeg)
   
프론트엔드 개발 올인원 패키지 with React Online. 👉 https://bit.ly/31Cf1hp