---
title : "[패캠올인원챌린지] 프론트엔드 개발자과정 day3 - 24강 Git & Github (feat. GUI)"
date : 2020-08-12
categories : pastcampus all-in-one-challenge day2 git github GUI
---

# Git GUI로 알아볼 내용
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


# git이  


  
# 다른 사람이 만든 저장소 받아오기 (클론)
1. 아래 소스와 같이 클론.
1. 클론 한 뒤 폴더에서 파일 하나 생성해보고 add->commit->push 과정을 거쳐본다.
1. github에서 제대로 올라갔는지 확인한다.
1. 상대방은 내 업데이트를 pull해서 사용할 것이다. 
```
git clone https://github.com/ID/NAME.git //폴더 생성하며 클론하기
git clone https://github.com/ID/NAME.git . //띄어쓰고 쩜하면 현재폴더에 클론하기
```
* 클론을 하면 원격 저장소의 코드를 내 컴터에 받아올 수 있다(.git도 자동으로 생긴다). 
* 클론 받고 난 뒤 새로운 업데이트가 있다면 풀로 당겨올 수 있다. 
* 수정 후 다시 푸쉬(권한이 있는 경우 가능)
* 푸쉬 권한 주기 : github -> Settings -> Collaborators -> Add Collaborator

# 원격저장소에서 업데이트 가져오기 (Pull)
```
git pull origin master
```
pull로 당겨오면 업데이트 된 부분이 바로 나온다. 찍어보고 싶으면 git log.

# 마치면서
마크다운 수업을 듣고 깃/깃헙 수업을 들으니 블로그의 완전체가 완성된 것 같은 기분.. 이제 무적이닷😌
소스트리 GUI부터는 내일 들어야 할 것 같다. 왜냐면 조카를 봐줘야 되기 때문에.. 두시간째 유튜브 보여주는 중인데 이젠 안되겠당🤪 애엄마한테 혼날것같당 
   
오늘은 여기까지, 수강 모습은 아래에..
![수강인증이미지](/images/200807-1.png)
![수강인증이미지](/images/200807-2.jpeg)
![수강인증이미지](/images/200807-3.jpeg)