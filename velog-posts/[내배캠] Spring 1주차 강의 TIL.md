<p>📚 강의를 들으면서 헷갈렸던 부분들만 정리해서 작성</p>
<hr />
<h2 id="http-상태-코드">HTTP 상태 코드</h2>
<p>1xx</p>
<ul>
<li>요청 수신 후 처리중인 상태</li>
<li>잘 사용안함</li>
</ul>
<p>2xx</p>
<ul>
<li>정상 처리 완료
(여러 종류있으니 강의 자료 확인)</li>
</ul>
<hr />
<h2 id="3xx">3xx</h2>
<h3 id="리다이렉션">리다이렉션**</h3>
<ul>
<li>요청을 완료하려면 추가 행동이 필요한 상태</li>
<li>3xx 응답 + Location HTTP Header가 있으면 Location 위치로 리다이렉트 한다.</li>
</ul>
<img src="https://velog.velcdn.com/images/mo00ai/post/8cd99539-cb5c-43e8-bbbb-796ea627c020/image.png" width="60%" />

<hr />
<p><strong>리다이렉션 종류</strong></p>
<ul>
<li>300 사용 안함</li>
</ul>
<hr />
<p><strong>영구 리다이렉션</strong></p>
<ul>
<li>URL이 영구적으로 변경된 경우, 기존 URL을 사용하지 않는다.</li>
</ul>
<p>ex) /event → /event1</p>
<ul>
<li>301 Moved Permanently</li>
</ul>
<img src="https://velog.velcdn.com/images/mo00ai/post/63aed219-ac56-4274-858a-c52af230ebef/image.png" width="60%" />

<p>요청 메서드가 GET으로 변하고 본문이 제거될 수 있다.</p>
<hr />
<ul>
<li>308 Permanent Redirect</li>
</ul>
<img src="https://velog.velcdn.com/images/mo00ai/post/3ff98a50-cb08-4f90-8d63-a5883e2f675f/image.png" width="60%" />

<p>리다이렉트시 요청 메서드와 본문이 유지된다.</p>
<blockquote>
<p>영구 리다이렉션 - 진짜 url을 바꿀 경우
우리 사이트의 원래 주소가 <a href="http://www.naver.com%EC%9D%B4%EC%97%88%EB%8B%A4%EB%A9%B4">www.naver.com이었다면</a> <a href="http://www.neverever.com%EC%9C%BC%EB%A1%9C">www.neverever.com으로</a> 바꾸는 거임
<a href="http://www.naver.com%EC%9C%BC%EB%A1%9C">www.naver.com으로</a> 접속했던 사람들을 <a href="http://www.neverever%EB%A1%9C">www.neverever로</a> 유도</p>
</blockquote>
<hr />
<p><strong>일시 리다이렉션</strong></p>
<ul>
<li>URI가 일시적으로 변경된 경우</li>
</ul>
<p>ex) 게시글 작성 후 게시글 목록 페이지로 이동, PRG 패턴</p>
<ul>
<li>PRG(Post, Redirect, Get) 패턴이란?<ul>
<li>게시글 작성(Post) → 응답(Redirect) → 리다이렉트 요청(Get)</li>
</ul>
</li>
<li>PRG 패턴을 적용하지 않는다면?<ul>
<li>새로고침을 하게되면 요청이 중복으로 처리된다.</li>
</ul>
</li>
</ul>
<img src="https://velog.velcdn.com/images/mo00ai/post/2f0b3293-d4ab-42dc-b3a1-c92d10068608/image.png" width="60%" />

<ul>
<li>PRG 패턴을 적용 한다면?<ul>
<li>새로고침을 하면 GET 요청을 한다.</li>
</ul>
</li>
<li>대표 상태코드<ul>
<li>302 Found<ul>
<li>요청 메서드가 GET으로 변할 수 있다.</li>
<li>모호해서 명확한 303, 307이 등장하게 되었다.</li>
<li>이미 사용하고 있는곳이 많다. GET으로 변해도 상관없다면 사용해도 무방하다.</li>
</ul>
</li>
<li>303 See Other<ul>
<li>요청 메서드가 GET으로 변경된다.</li>
</ul>
</li>
<li>307 Temporary Redirect<ul>
<li>리다이렉트시 요청 메서드와 본문이 유지된다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>일시적인 리다이렉션일 경우엔 2가지로 나뉨</p>
</blockquote>
<hr />
<ol>
<li>이벤트, 점검처럼 일정 기간동안 다른 url로 유도할때
naver.com/event
naver.com/server-check
원래 naver.com url이 아니라 일시적으로 사용자들을 다른 url 접근하도록 유도해야할때! 사용함<blockquote>
<p>리소스가 잠깐 다른 url로 이동해야 할 때 사용</p>
</blockquote>
</li>
</ol>
<p>-&gt; 예 : 서버 이전 중 임시 url 사용.</p>
<h3 id="✅-일시적인-리다이렉션302-303-307은-이런-상황에서-사용됩니다">✅ 일시적인 리다이렉션(302, 303, 307)은 이런 상황에서 사용됩니다:</h3>
<ol>
<li>사이트 점검 중</li>
</ol>
<ul>
<li>원래 페이지(example.com)가 점검 중이면,
  → 일시적으로 점검 안내 페이지(example.com/maintenance)로 리다이렉트.</li>
<li>점검이 끝나면, 다시 원래 페이지로 정상 접속되도록 설정.</li>
</ul>
<ol start="2">
<li>이벤트나 프로모션 진행 중</li>
</ol>
<ul>
<li>쇼핑몰에서 특별 이벤트를 할 때,
  → 사용자가 example.com으로 접속하면, 이벤트 페이지(example.com/event)로 일시적으로 리다이렉트.</li>
<li>이벤트가 끝나면 원래 페이지로 정상적으로 접속되도록.</li>
</ul>
<ol start="3">
<li>임시적으로 URL 구조가 바뀔 때</li>
</ol>
<ul>
<li>리소스가 잠깐 다른 URL로 이동해야 할 때 사용.
  → 예: 서버 이전 중 임시 URL 사용.</li>
</ul>
<hr />
<h3 id="⚡-왜-이렇게-할까">⚡ 왜 이렇게 할까?</h3>
<ol>
<li><p>DNS나 도메인 설정을 따로 건드릴 필요 없이 서버에서 리다이렉트만 설정하면 끝!
 → 비용도 안 들고, 작업도 훨씬 단순.</p>
</li>
<li><p>사용자 경험(UX) 향상
 → 사용자가 이벤트를 모르고 chatgpt.com에 접속해도, 바로 이벤트 페이지로 유도할 수 있음.</p>
</li>
<li><p>SEO 영향 최소화
 → 302/303/307 같은 일시적 리다이렉션을 사용하면, 검색 엔진은 &quot;아, 이건 임시로 이동한 거구나&quot; 하고 원래 URL을 계속 기억.
 → 이벤트가 끝나고 리다이렉션을 해제해도 SEO에 악영향이 없음.</p>
</li>
</ol>
<blockquote>
<p>지피티가 이리 잘 설명해주신다^^</p>
</blockquote>
<hr />
<blockquote>
<p>근데?? 이럴 경우 말고도 일시적인 리다이렉션을 적용하는 경우가 있음!
바로바로 PRG 패턴!</p>
</blockquote>
<h2 id="prg-패턴">PRG 패턴</h2>
<ul>
<li>Post/Redirect/Get의 약자</li>
<li>웹 개발에서 폼 중복 제출을 방지하기 위해 사용하는 패턴</li>
</ul>
<h3 id="✅-prg-패턴이-필요한-이유">✅ PRG 패턴이 필요한 이유?</h3>
<ol>
<li>폼을 제출하는 기본 흐름</li>
</ol>
<ul>
<li>사용자가 회원가입, 댓글 작성 등에서 POST 요청을 보냄.</li>
<li>서버가 데이터를 처리하고 바로 결과 페이지를 응답으로 보여줌.</li>
</ul>
<p>2.문제 발생!</p>
<ul>
<li>이 상태에서 사용자가 <strong>새로고침(F5)</strong>을 하면, 브라우저는 POST 요청을 다시 보냄.</li>
<li>결과적으로 데이터가 중복 제출되는 문제가 발생할 수 있음.<ul>
<li>예: 상품 결제 시 중복 결제, 댓글 중복 작성 등</li>
</ul>
</li>
</ul>
<pre><code class="language-java">// 폼 페이지
@GetMapping(&quot;/form&quot;)
public String showForm() {
    return &quot;form&quot;; // form.html 렌더링
}

// 폼 데이터 처리
@PostMapping(&quot;/submit&quot;)
public String handleSubmit(@ModelAttribute User user) {
    userService.save(user); // 데이터 저장
    return &quot;redirect:/result&quot;; // PRG 패턴: 리다이렉트로 이동
}

// 결과 페이지
@GetMapping(&quot;/result&quot;)
public String showResult() {
    return &quot;result&quot;; // result.html 렌더링
}</code></pre>
<hr />
<p>✅ 여기서 리다이렉트가 핵심!</p>
<ul>
<li>return &quot;redirect:/result&quot;; → 이게 바로 PRG 패턴의 핵심!
  → POST 요청 후 바로 결과 페이지로 가지 않고,
  → 302 리다이렉트를 통해 /result로 이동하도록 설정한 것.</li>
<li>이렇게 하면 사용자가 결과 페이지에서 새로고침을 해도, GET 요청만 다시 발생하고 POST는 반복되지 않아요.</li>
</ul>
<hr />
<p>🚩 만약 PRG 패턴을 안 쓰면?</p>
<ol>
<li>사용자가 폼을 제출(POST)하고 바로 결과 페이지를 받음.</li>
<li>결과 페이지에서 새로고침하면, 브라우저가 마지막 요청(POST)을 다시 시도함.</li>
<li>데이터가 중복으로 저장되는 문제가 발생! ❌</li>
</ol>
<hr />
<p>✅ PRG 패턴을 안 썼을 때의 기본 동작 흐름</p>
<ol>
<li>사용자가 폼을 작성하고 제출</li>
</ol>
<ul>
<li>예: 회원가입, 댓글 작성, 상품 주문 등에서 POST 요청을 보냄.</li>
<li>POST /submit 요청으로 서버에 데이터를 전달.</li>
</ul>
<ol start="2">
<li>서버가 POST 요청을 받아 데이터 처리</li>
</ol>
<ul>
<li>데이터베이스(DB)에 데이터를 저장하고,</li>
<li>바로 결과 페이지를 반환 (result.html 등).</li>
</ul>
<ol start="3">
<li>사용자는 결과 페이지를 확인</li>
</ol>
<ul>
<li>&quot;등록이 완료되었습니다!&quot; 같은 메시지를 본다.</li>
</ul>
<ol start="4">
<li>여기서 새로고침(F5)을 누르면?</li>
</ol>
<ul>
<li>브라우저는 마지막 요청을 그대로 다시 전송함.</li>
<li>즉, POST /submit 요청이 다시 한 번 서버로 전송됨!</li>
</ul>
<ol start="5">
<li>서버는 다시 동일한 데이터로 처리</li>
</ol>
<ul>
<li>서버는 클라이언트의 요청을 다시 처리하면서,</li>
<li>같은 데이터를 또 한 번 DB에 저장함.</li>
</ul>
<hr />
<p>⚠️ 왜 이런 문제가 발생할까?</p>
<ul>
<li>HTTP 프로토콜의 기본 동작 때문!<ul>
<li>새로고침(F5)은 <strong>&quot;마지막으로 보낸 요청을 다시 보낸다&quot;</strong>라는 의미.</li>
<li>마지막이 POST 요청이었다면, 서버는 그 요청을 다시 정상적으로 처리해 버림.</li>
<li>서버 입장에서는 &quot;똑같은 요청이 다시 왔네? 그러면 또 처리해줘야지!&quot;가 되는 것.</li>
</ul>
</li>
<li>브라우저는 POST 요청이 데이터베이스에 어떤 영향을 미치는지 알 수 없음.
→ 단순히 &quot;내가 보낸 마지막 요청을 다시 보내야지!&quot; 하고 처리해 버림.</li>
</ul>
<blockquote>
<p>새로고침은 마지막 요청 재실행이고
prg를 쓰지 않았을 때 암만 결과 페이지를 잘 보여줘도 post 요청이 마지막 요청인건 변하지 않으니까
리다이렉션을 통해 get 요청을 다시 하도록 유도해서 새로운 페이지를 보여줌으로 인해 새로고침시 마지막 요청이 post가 아니도록 하는거임</p>
</blockquote>
<hr />
<h2 id="set-cookie-vs-cookie">Set-Cookie vs Cookie</h2>
<ol>
<li><p>서버 → 클라이언트</p>
<ul>
<li>서버가 응답 시 Set-Cookie로 쿠키를 설정.</li>
</ul>
</li>
<li><p>클라이언트 저장</p>
<ul>
<li>클라이언트가 받은 쿠키를 브라우저에 저장.</li>
</ul>
</li>
<li><p>클라이언트 → 서버</p>
<ul>
<li>이후 해당 쿠키가 유효하면 요청 시 Cookie 헤더를 통해 서버로 전송.</li>
<li>관리자 권한/ 게시글 작성자만 볼 수 있도록 고유 ID가 식별이 필요할 때 사용</li>
</ul>
</li>
</ol>