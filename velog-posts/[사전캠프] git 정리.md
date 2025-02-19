<p>vsc 이용해서 깃코드 넣기
깃 터미널(단축키 ctrl ) 열기 -&gt; bash 설정</p>
<p>/Users/mo00ai
/ : 루트 디렉터리(폴더) - 제일 첫 슬래시</p>
<p>home &gt; 바탕화면</p>
<p>ls -&gt; 현재 폴더 밑에 있는 폴더/파일 목록 보여줘 (숨긴거 못보여줌)</p>
<p>ls -a (list all) -모든 폴더파일 보여줘 숨겨진 것도 다
-&gt;&gt;&gt; . 으로 시작하는 파일 -&gt; 숨겨진 파일</p>
<p>cd 폴더 명 -&gt; 폴더로 이동
---&gt; 리눅스 타이핑은 대충 치고 tab 누르면 단어 자동완성 해줌<del>~</del> 개꿀띠</p>
<p>cd . 현재 디렉토리
cd .. 상위 경로 이동</p>
<p>pwd -&gt; 현재 경로 확인</p>
<p>clear -&gt; 터미널 창 초기화</p>
<p>mkdir 폴더명 - 폴더 생성</p>
<p>touch 파일명.html 등 - 파일 생성</p>
<br />
<br />

<hr />
<br />
<br />


<p>Git 필수 명령어</p>
<p>git init
-초기화하다
-프로젝트 시작전 딱 한번만 입력하면 됨</p>
<ul>
<li>아무데서나 git init하면 안됨</li>
<li>내 프로젝트 경로인지 명확하게 확인한후에(pwd) 입력</li>
</ul>
<p>git init 후
.git 이란 폴더가 생김
-&gt; 이후 코드 변경을 git에서 추적함</p>
<p>git status </p>
<ul>
<li>저장되기 전 상황을 확인하는 명령어</li>
</ul>
<p>ctrl k -&gt; clear-&gt; 터미널 창 청소 공백</p>
<br />

<p>git add 파일명 -&gt; 스테이지에 커밋될 파일이 추가됨
git commit -m &quot;메세지 작성&quot; -&gt; 커밋(확정)</p>
<p>please tell me who you are -&gt;&gt; 계정 설정 안해서 나는 에러
<br /></p>
<p>git config --global user.name &quot;유저이름&quot;
git config --global user.email &quot;아이디@이메일&quot;
-&gt; 계정 설정
깃허브랑 동일하게 설정하는게 안헷갈린다~</p>
<br />

<p>git add index.html hello.html
-&gt; 두개의 파일을 스테이지에 올릴 수 있음</p>
<p>git add .
-&gt;.(현재경로) 내에 있는 아직 add되지 않은 사항들을 모두 스테이지 위에 한꺼번에 올림</p>
<p>커밋하고 git status로 항상 마무리하는 걸 추천
-&gt; 커밋하고 상태 확인 좀 꼭 해~~</p>
<br />


<p>workin directory -현재 작업중인 폴더
staging area - add 해서 올라가는 장소 스테이지
repository - 저장소 (깃 저장소) .git/</p>
<br />

<p>git log -&gt; 저장내역 확인(커밋내역 확인)
q 버튼 누르면 git log 창에서 나가짐 -&gt; 기본 터미널로 이동</p>
<p>노란색 comit dkfjsla;fj;kdsafj -&gt; 커밋 아이디
git reset 커밋 아이디
-&gt; 커밋 아이디 상태로 돌아갈 수 있음</p>
<p>git reflog 
-&gt; 깃에서 했던 모든!!! 내역들 다 나옴
여기서 reset 바로 전 노란색 커밋 아이디 복사하고 
git reset 커밋 아이디 -&gt; 하면 reset 전으로 또 돌아갈 수 도 있음~ </p>
<p>깃허브에 커밋내용 올릴려면
깃허브에 리포지터리 만들고
맨밑에 git remmote 어쩌구 코드 복붙해서 터미널로 실행시키면 파일들 다 올라감</p>
<br />
<br />

<hr />
<br />
<br />

<p>git push 
-&gt; 커밋내용을 github 레포지터리에 업로드 하겠다는 것</p>
<br />

<p><code>용어 정리</code>
local repository -&gt; pc 로컬 폴더, git-lecture
remote repository -&gt; 깃허브 저장소
git push origin main(브랜치명)</p>
<br />

<p>git remote add origin &lt;github 주소&gt; --주소 쓰기 귀찮다면?
= 길다란 깃허브 주소를 origin 이란 이름으로 부르겠다
= git push origin main(브랜치명) - 짧고 편하게 축약버전
git branch -M main
git push -u origin main</p>
<br />

<p>git remote -v</p>
<ul>
<li>등록되어있는 리포지터리를 볼 수 있음</li>
</ul>
<p>git remote add abc 리포지터리 주소</p>
<ul>
<li>abc 이름으로 리포지터리 url 을 저장하겠다</li>
</ul>
<p>git remote -v</p>
<ul>
<li>현재 등록되어있는 repository 이름과 주소들을 확인하 ㄹ수 있음</li>
</ul>
<p>git remote remove abc(주소명)</p>
<ul>
<li>주소 삭제</li>
</ul>
<p>팁!!!
화살표로 위에 줄을 쓸 수 있음 (방향키 위)</p>
<p>현재 내 커밋내용을 main 브랜치에 origin이란 이름으로 업로드해줘</p>
<br />



<p>git branch -M main
기본 브랜치 master - 디폴트 브랜치명
현재 브랜치명(master)을 main으로 바꾼다!</p>
<ul>
<li>기본 브랜치 명을 단순히 바꿀때 사용!</li>
<li>가급적이면 main 으로 개명해서 쓰는 걸 권장함 master가 노예제도를 떠올리게 해서 불편하게 느끼는 외국인이 많아서 그럼</li>
</ul>
<p>git push -u origin main</p>
<ul>
<li>git push origin main -&gt; 이것 마저도 귀찮다</li>
<li>git push -&gt;&gt; 이거만 쳐도 알아서 git push origin main 해줫음 좋겠어<del>~ 할 때 쓰지만 비추천함</del></li>
<li>개인 플젝할때만 써도 ㄱㅊ지만 팀플은 절대 비추</li>
</ul>
<br />

<hr />
<br />

<p>충돌</p>
<p>A- 팀장</p>
<ol>
<li>초기 프로젝트 코드 작성</li>
<li>깃허브에 레포지토리 생성</li>
<li>업로드 푸싱</li>
</ol>
<p>팀장이 할 일
git hub repository 들어가서
settings 의 collaborators 들어가서
add people로 팀원들의 email or 유저네임 추가
-&gt; 팀원들이 이메일확인해서 수락하면 콜라보레이터 추가됨</p>
<br />

<p>팀원이 깃허브의 코드를 내 컴에 복제해서 작업하기
-&gt; git clone</p>
<p>-&gt;리포지터리에 녹색 code 버튼으로 zip 파일 다운로드 받아서 쓰는 방법도 있음 하지만 귀찮음 very</p>
<p>code 누르고 https의 url 복사
작성할 프로젝트 폴더 만들고 들어가야함
git clone url 해서 복붙하면 됨</p>
<br />

<p><code>안중요</code>
mkdir member-b -&gt; 멤버비 폴더 생성
cd member-b -&gt; 멤버 비 폴더 안으로 이동</p>
<p>vsc 로 폴더 열어서 프로젝트 실행
이 상태에서 터미널 열기</p>
<p>pwd -&gt;현재 경로가 member-b 인거 확인</p>
<br />

<p>git clone &lt;깃허브주소&gt; .
-&gt; 현재 경로에다가 파일만 복제 해줘
-&gt; (띄어쓰기).    필수</p>
<p>클론은 딱 한 번만 하면 됨</p>
<br />


<p>팀원이 이 작업 수행
-코드 수정
-코드 저장 명렁어 실행 (git add, git commit)
-git push origin main명</p>
<br />

<p>다른 사람이 변경한 코드 내 코드에도 가져오기
---&gt;&gt;&gt; git pull</p>
<ul>
<li>팀원이 수정하고 push한 수정사항을 pull로 가져오기</li>
</ul>
<p>다른 사람이 이미 git push 하고 내가 git push 하려고 하면 발생하는 에러
팀장도 수정하고 팀원도 수정함.
팀장이 push를 했음(옵션으로 다른 수정사항(팀원들 수행) 무시하고 푸쉬) 하면 다른 팀원들의 수정사항이 모두 날라갈뻔함~---&gt; 충돌(에러) 내서 깃이 이걸 막아줌</p>
<p>---&gt; git pull before pushing again (에러 힌트)</p>
<p>그래서 팀원의 수정사항 push한 걸 내가 pull해서 받음!(팀장)</p>
<ul>
<li>내꺼가 젤 최신</li>
</ul>
<p>그럼 내가 그걸 다시 깃허브에 push함 -&gt;&gt;&gt; 팀장 껄로 최종으로 올라감</p>
<br />


<p>pull했을 때 자주 뜨는 에러
reconcile divergent branches -&gt; 어케 합칠지 알려줘</p>
<p>해결방법
git config pull.rebase false (리베이스 안함)
git pull origin main
-리베이스 하고 풀하면 pull 잘 될거임</p>
<p>rebase 잘못 쓰면 다 날라감</p>
<p>git config pull.rebase false 
git config pull.rebase true
git config pull.ff only</p>
<p>~
~
~
~
~
~
이런
vim editer 뜨면
esc :wq (enter) -&gt; 빔에디터에서 나와짐</p>
<br />

<p>git pull 해서 가져왔는데 코드가 이상해짐<del>~ 어캄</del>
에러 : automatic merge failed
-&gt; 코드 합치는 거 실패함
-&gt; 깃이 자동으로 깃허브 코드랑 로컬이랑 합쳐주는데 미안 충돌해서 못해줘
-&gt; 충돌 고치고 커밋 다시해줘</p>
<br />


<p>-&gt; 화면 보면
&lt;&lt;&lt;&lt;&lt;&lt;head
aaaa
=====
ddddd</p>
<blockquote>
<blockquote>
<blockquote>
<blockquote>
<blockquote>
<blockquote>
<blockquote>
<blockquote>
<p>kdfja;lfkjdaklfjad;lfk</p>
</blockquote>
</blockquote>
</blockquote>
</blockquote>
</blockquote>
</blockquote>
</blockquote>
</blockquote>
<h1 id="1">1</h1>
<p>2</p>
<p>1번 코드랑 2번 코드 중 뭐로 고쳐줄까</p>
<p>그래서 둘 중 하나 고르면 고른 코드로 고쳐줌</p>
<br />

<p>쌤이 충돌내는 예시 보여줌
깃허브 내에서 코드 고치면 안됨 ~ -&gt; 백퍼 충돌남
깃허브 내에서 자체로 코드 고치고 , vsc로 또 파일 코드 수정함
그 뒤로 add/ commit /git remote -v/ git pull origin main
-&gt;&gt;충돌나요~~</p>
<p>git config pull.rebase false
git pull origin main 
-&gt; 충돌~</p>
<br />

<p>충돌 해결 방법</p>
<p>1) 1,2 중에 선택해서 해결하는 방법
-&gt; 되돌리고 싶으면 ctrl z 가능
-&gt; 꼭 써야되는 기능은 아님, 걍 vsc가 쉽게 작업하라고 도와주는 거임
-&gt; 충돌해결은 꼭 add하고 커밋해야됨! 푸쉬까지해야 충돌해결이 끝나는 , 그리고 push -&gt; 그럼 충돌해결
-&gt; 이 선택이 내가 원하는 코드로 만든 다음에 커밋하면 됨요</p>
<br />


<p>충돌이 발생하는 이유는?
같은 파일의 같은 위치에 코드가 변경되었기 때문</p>
<br />


<p>working directory - pc에 있는 기본 로컬 디렉토리</p>
<p>커밋 되기 전 깃 상태 확인 -&gt; git status
깃 커밋내역 확인 -&gt; git log</p>
<p>github desktop gui -&gt; 터미널로 먼저 깃과 친해지고 이용하는 걸 추천</p>
<p>브랜치를 알아야 충돌 안되게 합치는 방법을 알 수 있음
근데 브랜치 있어도 실수하면 충돌도 날 수 있기도 함~</p>
<p>충돌 안나는 법</p>
<ul>
<li>각자 다른 파일에서 관리하면 충돌 날 일이 없음</li>
</ul>
<p>현업에서 reset 이나 revert 중에 뭘 더 사용하나요</p>
<ul>
<li>이건 리더 따라서</li>
</ul>
<p>같은 파일 다른 위치의 코드들이 충돌이 날수도 있다는거군요?
-&gt; 같은 위치에서 보통 나지만 다른 위치에서도 날 수 있음
-&gt; 보통 common 패키지를 동시에 수정할 경우 많이 충돌났던것 같아요</p>
<p>깃에 푸쉬 풀 다 된 최종이었는데 내가 다른 팀원이랑 겹치는 부분을 수정해서 수정하기 전으로 돌아가고 싶음 -&gt; rest 커밋아이디 해서 해당 커밋 시점으로 돌아가면 될 듯 </p>
<br />
<br />
<br />

<hr />
<br />
<br />
<br />



<p>git 대표 개념</p>
<br />


<p><code>add</code></p>
<ul>
<li>내 로컬 스테이지에 업로드</li>
</ul>
<p><code>commit</code></p>
<ul>
<li>내 로컬 스테이지에 저장</li>
</ul>
<p><code>push</code></p>
<ul>
<li>온라인에 백업함(깃허브에 올림)</li>
</ul>
<p><code>pull</code></p>
<ul>
<li>push된 수정사항을 내려받음 </li>
<li>수정사항이 하나 발생하면 그걸 푸쉬 후 그걸 풀해서 베이스 프로젝트를 항상 최신으로 업데이트 하는게 중요함.</li>
</ul>
<p><code>init</code></p>
<ul>
<li>최초로 프로젝트 생성시 깃을 사용하기 위해 하는 작업 깃 시작한다 이 말씀임</li>
</ul>
<p><code>remote</code>  </p>
<ul>
<li>나의 로컬 깃을 깃허브라는 온라인 드라이브에 올릴 때 사용</li>
<li>사전에 깃허브에서 repository 만들어 두고 팀원들 초대 메일 날릴 것</li>
</ul>
<p><code>clone</code></p>
<ul>
<li>팀원이 깃허브에 올린 최초 프로젝트를 다운로드 받을 때 필요함</li>
</ul>
<p><code>fetch</code></p>
<ul>
<li>원격 저장소(GitHub 등)에서 최신 커밋 정보를 가져오지만, 로컬 브랜치에 바로 반영하지 않는 명령어</li>
<li>내 로컬 저장소와 원격 저장소의 차이를 확인할 수 있지만, 내 코드에는 아무런 변화가 생기지 않아.
🚨 변경사항을 로컬에 적용하려면 git merge 또는 git pull을 추가로 실행해야 해!</li>
</ul>
<p>git fetch와 git pull 차이점</p>
<p>git fetch :    원격 저장소의 최신 상태만 가져오고, 로컬 브랜치에는 적용하지 않음
git pull : fetch + merge 를 한 번에 실행해서 로컬 브랜치에도 적용함</p>
<ul>
<li>잘 사용 안할 듯 성격 급해서</li>
</ul>
<p><code>reset</code></p>
<ul>
<li>해당 커밋 아이디로 이동</li>
<li>언젠가 필요한 날이 올 듯</li>
</ul>
<br />
<br />

<hr />
<br />
<br />


<p>오늘 깃 쓰면서 자주 쓴 명렁어들</p>
<p>git status</p>
<ul>
<li>깃 상태 확인 (누가 커밋했는지 푸쉬 해야할지 풀해야할지 알수있음)</li>
</ul>
<p>git add .</p>
<ul>
<li>스토리지에 올릴 때 모든 파일 올려놓기 위해서 . 찍음 아님 직접 파일 이름 적어야함</li>
<li>근데 튜터님 says 개별로 세세하게 커밋하고 커밋메세지 작성하는 걸 추천하심</li>
</ul>
<p>git commit - &quot;메세지내용&quot;</p>
<ul>
<li>커밋 날리면서 커밋 메세지 남김</li>
</ul>
<p>git pull origin dev(브랜치명)</p>
<ul>
<li>이 브랜치로 현 상황 깃허브에 올리겠단 뜻임</li>
</ul>
<p>git checkout dev(브랜치명)</p>
<ul>
<li>dev(브랜치명)으로 이동하겠다(위치를 바꾸겠다)는 뜻임 </li>
</ul>
<p>git push origin dev </p>
<ul>
<li>dev에 push 하겠다는 뜻임
(깃허브에는 달라진 점이 없음, pull해야 깃허브에 반영됨)</li>
</ul>
<br />
<br />


<hr />
<br />
<br />
<br />



<p>브랜치 설명</p>
<p>main - 최종! 정말 완성 배포하기 전에 완성 코드 올리는 브랜치
dev - 완성 전 단계로 팀원별/기능별 브랜치들을 push/pull해서 합쳐보는 브랜치
feture-기능명/팀원명 : 맡은 기능별, 팀원별 브랜치. 여기서 작업한 뒤에 dev에 합치는 작업을 함. </p>
<ul>
<li>오늘 우리 팀원이 push pull 만 사용하고 merge를 사용하지 않은 이유)</li>
<li>main dev만 만들고 각자 브랜치를 안만들었기 때문!)
(merge는 브랜치를 합치는 명렁언데 우린 각자 로컬에서 dev에 업로드 했으니까 할수 없었따!)</li>
</ul>
<br />
<br />

<hr />
<br />
<br />
<br />

<p>헷갈렸던 부분 지피티에게 물어본 결과!!</p>
<p>✅ git merge가 필요한 상황 &amp; 예제
👉 git merge는 두 개의 브랜치를 합칠 때 사용하는 명령어야.
👉 특히 팀 프로젝트에서 각자 다른 브랜치에서 작업한 후 dev나 main에 합칠 때 필요!</p>
<p>🔹 1. feature 브랜치를 dev에 합치는 경우</p>
<p>📌 상황:</p>
<p>팀원이 feature-login 브랜치에서 로그인 기능을 개발했고, 이제 dev 브랜치에 합쳐야 함.
현재 브랜치는 dev, feature-login 브랜치의 변경 사항을 병합할 예정.</p>
<p>📌 병합 과정</p>
<p>git checkout dev           # dev 브랜치로 이동
git pull origin dev        # 최신 dev 브랜치 코드 가져오기 (충돌 방지)
git merge feature-login    # feature-login 브랜치를 dev에 병합
git push origin dev        # 병합된 내용을 GitHub에 업로드
✔️ git checkout dev → 병합할 기준 브랜치로 이동
✔️ git pull origin dev → 원격 최신 상태 반영 (충돌 방지)
✔️ git merge feature-login → feature-login 브랜치를 현재 브랜치(dev)에 병합
✔️ git push origin dev → 병합된 내용을 원격 저장소(dev)에 반영</p>
<p>📌 만약 충돌이 발생하면?</p>
<p>충돌 해결 후
git add .
git commit -m &quot;충돌 해결: feature-login 병합&quot;
git push origin dev</p>
<p>🔹 2. 여러 팀원이 dev에 작업한 후 main에 합치는 경우</p>
<p>📌 상황:</p>
<p>팀원들이 dev 브랜치에서 개발을 진행했고, 기능이 완성되었음.
이제 dev 브랜치를 main에 병합해서 배포할 예정.</p>
<p>📌 병합 과정</p>
<p>git checkout main          # main 브랜치로 이동
git pull origin main       # 최신 main 코드 가져오기
git merge dev              # dev 브랜치를 main에 병합
git push origin main       # 병합된 main 브랜치를 원격 저장소에 반영
✔️ main 브랜치로 이동한 후 dev 브랜치를 병합하면 최신 기능이 main에 추가됨.
✔️ 보통 main은 운영(배포)용 브랜치이므로 dev에서 충분히 테스트한 후 병합하는 게 좋아!</p>
<p>🔹 3. git fetch 후 merge로 최신 코드 반영
📌 상황:</p>
<p>내가 dev 브랜치에서 작업하고 있는데, 팀원이 dev에 새로운 코드를 push함.
git pull을 하면 자동으로 merge까지 되는데, 충돌이 걱정되면 fetch 후 merge를 직접 할 수도 있음.
📌 병합 과정</p>
<p>git fetch origin          # 원격 저장소에서 최신 상태 가져오기
git diff dev origin/dev   # 내 로컬 dev와 원격 dev의 차이 확인
git merge origin/dev      # 원격 dev 브랜치를 내 로컬 dev에 병합
✔️ fetch 후 diff를 사용해서 어떤 변경이 있는지 확인 가능
✔️ merge를 직접 실행하면 충돌이 발생했을 때 내가 컨트롤 가능</p>
<br />
<br />
<br />


<hr />
<br />
<br />
<br />


<h4 id="내-질문">내 질문</h4>
<p>그냥 push하고 팀장이 pull해서 업데이트 다른 팀원이 pull 받고 수정해서 또 push 하고 팀장이  pull 받고 다른 팀원이 pull받아서 또 push 
이렇게 안하고 merge를 하는 이유는 뭐야?</p>
<ul>
<li>미니 프로젝트(팀소개) 경우엔 우리가 main dev만 써서 그랬음</li>
<li>merge는 브랜치를 브랜치와 합칠 때 씀</li>
<li>우리는 개인/기능별 브랜치 없이 걍 로컬에서 바로 dev로 push 했기 때문에 dev&gt;main 이면 모를까 각자의 것을 dev에 올릴 땐 merge를 쓸 수 없음</li>
</ul>
<br />

<h4 id="지피티-답변">지피티 답변</h4>
<p>✅ push → pull만으로 협업하지 않고 merge를 하는 이유
팀원들이 각자 push하고, 팀장이 pull한 후 다시 push하는 방식도 가능하지만,
팀 프로젝트에서 각자의 브랜치를 만들고 merge하는 방식이 더 좋은 이유가 있어! 🚀</p>
<p>🔹 1. 여러 명이 동시에 작업할 때 충돌 방지
📌 push와 pull만 하면 충돌(Conflict)이 더 자주 발생함
→ 여러 명이 같은 파일을 동시에 수정하면, 같은 줄에서 충돌이 발생할 가능성이 높아!</p>
<p>🔴 잘못된 방식 (push → pull 반복)</p>
<p>A가 main에서 작업 후 push
B도 같은 파일을 수정했는데, push하려니 충돌 발생
B가 pull 후 충돌을 해결하고 push
다시 C가 pull 후 충돌을 해결하고 push 📌 ➡ 팀원들이 같은 파일을 건드릴수록 충돌 해결이 복잡해짐!</p>
<p>✅ 해결 방법 (merge를 이용한 브랜치 전략)</p>
<p>각자 개별 브랜치(feature-로그인, feature-댓글) 에서 작업 후, dev에서 merge
dev에서 충돌을 해결하고, main에 병합</p>
<br />

<p>팀원 각자 개별 브랜치 생성 후 작업
git checkout -b feature-login</p>
<p>작업 후 커밋
git add .
git commit -m &quot;로그인 기능 추가&quot;
git push origin feature-login</p>
<p>dev 브랜치에서 병합 후 팀장이 관리
git checkout dev
git merge feature-login
git push origin dev
✔️ 이렇게 하면 각자 개별 브랜치에서 작업하고, dev에서 통합 관리 가능
✔️ main을 직접 건드리지 않으면서 안정적인 개발이 가능함!</p>
<br />
<br />

<hr />
<br />
<br />


<h4 id="내-질문-1">내 질문</h4>
<p>그럼 각자의 브랜치 작업을 dev에서 merge하고 dev에서 충돌을 해결한댔잖아
그럼 그건 어케 해결해? 파일에 그 꺽새로 &gt;&gt;&gt;&gt; aa === bb &lt;&lt;&lt;&lt;&lt;&lt; 이런 식으로 동시에 뜨니까 그걸 다같이 보면서 의견 조율해서 해결해 나가는 거야?</p>
<br />

<h4 id="지피티-답변-1">지피티 답변</h4>
<p>✅ git merge 충돌(Conflict) 해결하는 방법
👉 dev 브랜치에서 여러 팀원의 작업을 merge하다 보면 같은 파일의 같은 부분이 수정되면 충돌 발생!
👉 충돌이 나면 Git이 자동으로 병합하지 못하고, 개발자가 직접 수정해야 해!
👉 보통 팀원들과 의견 조율해서 결정하지만, 작업 방식에 따라 해결하는 방법이 다를 수 있음.</p>
<br />

<p>🔹 1. 충돌이 발생하는 경우
📌 예제 (두 명의 팀원이 feature-로그인, feature-회원가입 브랜치에서 같은 파일을 수정함)</p>
<p>🚀 A(로그인 담당) - feature-로그인 브랜치</p>
<p>function greet() {
    console.log(&quot;Hello, user!&quot;);
}
🚀 B(회원가입 담당) - feature-회원가입 브랜치</p>
<p>function greet() {
    console.log(&quot;Welcome, new member!&quot;);
}</p>
<p>📌 이제 feature-로그인을 dev에 merge한 다음, feature-회원가입을 merge하면 충돌 발생!</p>
<p>git merge feature-회원가입
🚨 충돌이 발생하면 Git이 자동으로 병합하지 못하고 아래처럼 파일이 변함</p>
<p>function greet() {
&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD
    console.log(&quot;Hello, user!&quot;);
=======
    console.log(&quot;Welcome, new member!&quot;);
-&gt;&gt;&gt;&gt;&gt; feature-회원가입
}</p>
<p>✔️ 위쪽(HEAD) = 현재 dev 브랜치의 코드 (feature-로그인 브랜치에서 가져온 코드)
✔️ 아래쪽(feature-회원가입) = feature-회원가입 브랜치에서 추가된 코드</p>
<br />
<br />

<p>🔹 2. 충돌 해결하는 방법
✅ 2-1. 직접 수정해서 해결
✔️ 팀원과 상의해서 최적의 코드로 수정하고 저장</p>
<p>function greet() {
    console.log(&quot;Hello, user! Welcome, new member!&quot;);
}
✔️ 수정이 끝났으면 Git에 변경 사항 반영</p>
<p>git add .
git commit -m &quot;충돌 해결: greet() 메시지 병합&quot;
git push origin dev
🚀 이제 dev 브랜치에 병합된 코드가 최종 버전이 됨.
<br />
✅ 2-2. 하나의 변경 사항만 유지
👉 만약 한 쪽 코드만 남겨야 한다면, 삭제할 부분을 지우고 저장
👉 예를 들어, feature-로그인의 코드만 유지하려면:</p>
<p>function greet() {
    console.log(&quot;Hello, user!&quot;);
}
📌 그 후 git add . → git commit -m &quot;충돌 해결&quot; → git push 하면 해결됨.</p>
<br />

<p>✅ 2-3. VS Code에서 쉽게 해결하는 방법
🚀 VS Code를 사용하면 GUI로 충돌 해결 가능!</p>
<p>충돌 발생 시, VS Code에서 해당 파일을 열면 충돌 부분을 자동으로 표시해줌.
&quot;Accept Current Change&quot; / &quot;Accept Incoming Change&quot; / &quot;Accept Both Changes&quot; 옵션 선택 가능.
Accept Current Change → 현재 dev 브랜치 코드 유지
Accept Incoming Change → feature-회원가입 코드 유지
Accept Both Changes → 둘 다 합침
✔️ 선택 후 저장하고, git add . &amp;&amp; git commit -m &quot;충돌 해결&quot; 실행하면 완료! 🚀
<br />
<br /></p>
<p>🔹 3. 협업 시 충돌 해결 전략
충돌이 발생했을 때 어떻게 해결할지 미리 팀원들과 정해두면 편함!
1️⃣ 작업 시작 전 git pull origin dev 해서 최신 코드 받아오기
2️⃣ 팀원이 같은 파일을 수정할 경우, 미리 협의 후 진행
3️⃣ 충돌 발생 시, 팀원들과 이야기해서 최선의 코드로 병합
4️⃣ VS Code 등의 Git 도구를 활용하면 편리하게 해결 가능!</p>
<p>🎯 결론
✔️ Git 충돌(&gt;&gt;&gt;&gt; HEAD ... &lt;&lt;&lt;&lt;)이 발생하면 직접 코드 수정 후 저장해야 함
✔️ 팀원들과 상의해서 최적의 코드로 병합 후 git add . &amp;&amp; git commit -m &quot;충돌 해결&quot; 실행
✔️ VS Code를 사용하면 &quot;Accept Change&quot; 기능으로 쉽게 해결 가능
✔️ 사전에 git pull origin dev를 자주 해서 충돌을 예방하는 것도 중요!</p>
<br />
<br />

<blockquote>
<p>지피티가 있어 행복합니다..
  깃에 대해 엄청 많은 걸 얻은 것 같다
  이러고 담주에 또 특강 들으면 백지 상태 되겄지만 ㅋ</p>
</blockquote>