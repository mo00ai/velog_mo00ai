<ol>
<li>브랜치 활용하기</li>
</ol>
<ul>
<li>수정은 하고 싶은데 원래 파일은 그대로 놔두고 싶다?</li>
<li>몇 기가짜리 프로젝트도 zip파일 만들어서 복사할거니</li>
<li>---&gt; 브랜치를 활용하걸아
브랜치 === 복사본</li>
</ul>
<p>브랜치 생성 명렁어</p>
<pre><code class="language-git">git branch 브랜치이름
(ex)git branch login</code></pre>
<p>깨알꿀팁) git init은 처음 프로젝트를 생성한 팀장만</p>
<p>현재 프로젝트의 브랜치 목록 확인</p>
<pre><code class="language-git">git branch
출력) 
login
*main</code></pre>
<p>현위치는 *표시 있는 main</p>
<br />

<p>브랜치 이동</p>
<pre><code class="language-git">git switch 브랜치이름</code></pre>
<ul>
<li>권장</li>
<li>최근 더 잘씀 (의미가 더 잘맞음) (최근 개발자)<pre><code>git checkout 브랜치이름</code></pre></li>
<li>조금 오래 된 명령어(오래된개발자)</li>
<li>-&gt; 둘다 동작은 완전히 동일함</li>
</ul>
<br />

<p>브랜치 한 번에 생성 &amp; 이동</p>
<pre><code>git switch -c 브랜치이름
git checkout -b 브랜치이름</code></pre><ul>
<li>이렇게 한 번에 생성하고 이동하는 방법을 더 많이 씀</li>
</ul>
<br />

<blockquote>
<p>이렇게 브랜치를 만들어 놓고 열심히 개발함</p>
</blockquote>
<br />

<p>git add .
git commit -m &quot;로그인&quot;</p>
<br />

<blockquote>
<p>main 브랜치로 이동하면
login 브랜치에서 수정한 코드가 남아있을까?</p>
</blockquote>
<ul>
<li>no, git switch main으로 main브랜치에 돌아가면 login 브랜치 코드가 없음</li>
</ul>
<blockquote>
<p>브랜치가 다르면 서로 다른 파일이다</p>
</blockquote>
<ul>
<li>그래서 main 브랜치에서 git log해서 살펴봐도 login 코드 수정내역이 커밋된 내역이 없음</li>
</ul>
<blockquote>
<p>login 브랜치를 main으로 합칠거임</p>
</blockquote>
<br />

<p>머지하는 법</p>
<ol>
<li><p>main으로 이동</p>
<pre><code class="language-git">git switch (최종브랜치이름)
git switch main</code></pre>
</li>
<li><p>병합</p>
<pre><code>git merge (합칠 브랜치 이름)
git merge login </code></pre></li>
</ol>
<ul>
<li>login 브랜치에서 작성한 코드를 main으로 병합함</li>
</ul>
<br />

<blockquote>
<p>근데 사실!!!!!!! git merge를 잘 안씀
깃허브 뒀다 뭐해!
깃허브는 머지하기 전에 팀원들끼리 확인하고 코드리뷰 할 수있도록도 도와줌
그럼 깃허브를 써야겠줴??</p>
</blockquote>
<blockquote>
<p>그게 바로 <strong><em>pull requset</em></strong></p>
</blockquote>
<p>pull : 당겨서 합친다
= fetch and merge
= fetch : 데이터 가져오기
=  merge : 데이터 합치기
request : 요청하다. </p>
<p>pr : 내 코드를 최종 브랜치에 합쳐줏쇼란 요청</p>
<hr />
<br />

<p>(예시를 보여주시려고 git merge login 전으로 돌아가심)</p>
<p>git reflog</p>
<ul>
<li>과거로 돌아가기 위한 내역 보기</li>
<li>누르면 여러 내역들이 뜸</li>
</ul>
<p>git reset --hard (내역이름-노란색) 
그럼 그 커밋 내역으로 돌아감</p>
<p>git branch 확인하면 login 브랜치가 있는 걸 알수 있음</p>
<br />
---


<br />

<h3 id="pull-request로-머지해보기">pull request로 머지해보기</h3>
<br />

<h4 id="깃허브-생성하고-연동하기">깃허브 생성하고 연동하기</h4>
<ol>
<li>프로젝트 만들어서 터미널에서 git init하기</li>
<li>깃허브에서 새 리포지터리 생성<ul>
<li>팀장일시 settings 에서 collaborator로 팀원들 추가</li>
</ul>
</li>
<li>git remote 깃리포지터리 주소랑
 git branch -M main 해서 마스터 -&gt; 메인 이름 병경</li>
<li>git add . / git commit -m &quot;&quot; / git push origin main
 해서 push 날리고 깃허브 업데이트 하기</li>
</ol>
<h4 id="기능-브랜치-생성login">기능 브랜치 생성(login)</h4>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/c189b03b-4eb5-4221-9699-9f579bc70843/image.png" /></p>
<h4 id="기능-수행하고-login-브랜치에-push">기능 수행하고 login 브랜치에 push</h4>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/3cc4446a-958f-4881-8312-f593f6468cc9/image.png" style="width: 60%;" /></div>

<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/821774d4-e9c7-40f0-b0a1-ceb97a7b3d51/image.png" style="width: 60%;" /></div>

<h4 id="github에서-pull-request-생성하기">github에서 pull request 생성하기</h4>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/9fb7a8fb-efcd-48ad-a680-e79653cb8690/image.png" style="width: 60%;" /></div>

<p>compare and pull request 
-&gt; 초록색 클릭 </p>
<h4 id="pull-request-편집기에서-pr-요청-작성">pull request 편집기에서 pr 요청 작성</h4>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/1693c1bd-a170-41c9-8428-e3a1329eb3f4/image.png" style="width: 60%;" /></div>
경로 잘 확인하기!
`base` : 합침 당할 브랜치 (main), 더 큰 개념
`compare` : 내가 작업했고 합칠 브랜치 (login), 더 작은 개념
able to merge -> 초록색이 뜨면 합칠 수 있다는 것 

<br />

<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/08cdfab2-dcd9-41ad-a014-abb7e7e14a7a/image.png" style="width: 60%;" /></div>

<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/7ca8d69e-4653-4d25-97af-a1d62757ccde/image.png" style="width: 60%;" /></div>

<p>create pull request 클릭</p>
<br />

<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/647288df-e907-4551-9635-546e9144d366/image.png" style="width: 60%;" /></div>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/ec011756-02fb-4b6c-bf80-85a6031e7b4c/image.png" style="width: 60%;" /></div>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/34a7ebc2-6c92-4d47-99e2-d6c9f67b95b4/image.png" style="width: 60%;" /></div>

<p>file changed 탭 
-&gt; main과 login간의 차이를 알아서 분석해줌
빨간색 - 없어지는 거
녹색 - 새롭게 생기는 거
---&gt; 현재는 수정 없이 추가만해서 녹색만 뜸
---&gt; 코멘트도 작성 가능</p>
<br />


<p>암튼 이렇게 코멘트를 작성하며 
코드리뷰 과정을 거쳐서
다시 conversation 탭에서 
merge pull request - confirm merge 초록 버튼을 누르면 머지 됨 </p>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/e43c8d72-5d9b-42b7-8c0b-140953d0fc4d/image.png" style="width: 60%;" /></div>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/1cf7099c-b936-42a4-bb13-f840a84dcbc3/image.png" style="width: 60%;" /></div>


<br />

<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/26ef4c23-e414-4b8b-afb0-b2e362154587/image.png" style="width: 60%;" /></div>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/c1b80da7-f214-4f50-9556-2a6f10b5541b/image.png" style="width: 60%;" /></div>


<p>delete branch 로 브랜치 지워주기
나중에 헷갈릴 수 있음 문제 없으니까 ㄱㅊ 브랜치 지워줘</p>
<blockquote>
<p>git에서도 직접 git branch -d login / git branch -D login(강제삭제)
로 삭제해줘야 됨. delete branch는 깃허브에만 반영되지 로컬엔 반영안됨 pull받아도</p>
</blockquote>
<br />

<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/d97c5333-78f4-41e1-aeae-4aed52e8826a/image.png" style="width: 60%;" /></div>

<blockquote>
<p>깃허브와 로컬은 실시간 연동이 아님
깃허브에선 합쳐졌지만 아직 로컬엔 머지한 결과가 안뜸
깃 명령어를 통해 업로드 하거나 받아야 로컬에도 반영 됨</p>
</blockquote>
<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/bd63b847-daab-401c-8eb7-5b4bcb26e858/image.png" style="width: 60%;" /></div>


<blockquote>
<p>이럼 머지 끝!!!!</p>
</blockquote>
<br />

<hr />
<br />

<div align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/8fffac5b-5e04-4864-ac0f-e30fbc5e86c7/image.png" style="width: 60%;" /></div>

<p>main 브랜치는 <strong><em>배포용</em></strong>/프로덕션용
디립다 main에 머지하면 안됨</p>
<br />

<p><code>main</code> 브랜치(배포) - <code>develop</code> 브랜치 (테스트 용) - <code>기능 브랜치</code>(실제 개발)</p>
<ul>
<li>보통 이렇게 개발함</li>
<li>develope을 dev라고도 씀</li>
</ul>
<br />

<p>항상 로컬에서 먼저 테스트하기
내 로컬에서 먼저 테스트하고 합쳐봐야함</p>
<p>dev브랜치가 항상 최신이기 때문에</p>
<p>합치기 전에 dev브랜치에 있는 내용을 pull 받아옴
그 dev 내 내용과 내 코드들이 충돌나는지 확인하고
그걸 수정해보는게 좋음</p>