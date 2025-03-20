<p>📚강의 들으면서 헷갈렸던 부분들 정리 및 spring mvc 발전 정리</p>
<hr />
<h2 id="api">API</h2>
<ul>
<li>프로그램(소프트웨어)끼리 데이터를 주고받을 수 있도록 정해진 약속!</li>
<li>(규칙, 명령어, 데이터 형식)</li>
<li>웹사이트에서 어떤 행위(버튼 클릭 등)을 하면 브라우저(클라이언트)는 서버에 데이터를 요청함 -&gt; <code>API 요청(HTTP Requset)</code> 발생</li>
<li>서버는 API를 통해 요청을 처리하고 결과를 HTTP Response로 보내줌</li>
</ul>
<hr />
<h2 id="sendredirect-vs-forward">.sendRedirect() vs .forward()</h2>
<p>forward()</p>
<ul>
<li>현재 요청(request)과 응답(response)를 유치한 채 jsp로 넘겨줄 수 있음</li>
<li>기존 요청 유지</li>
<li>ex) 사용자가 데이터를 입력하고 서블릿으로 보낸 후 , JSP에서 이 데이터를 출력해야할 떄 필요함</li>
</ul>
<p>sendRedirect()</p>
<ul>
<li>새로운 요청을 만듦</li>
</ul>
<hr />
<h3 id="1️⃣-requestdispatcherforwardrequest-response를-사용할-때">1️⃣ RequestDispatcher.forward(request, response)를 사용할 때</h3>
<pre><code class="language-java">RequestDispatcher dispatcher = request.getRequestDispatcher(&quot;/WEB-INF/views/post-form.jsp&quot;);
dispatcher.forward(request, response);</code></pre>
<ul>
<li>forward()는 서버 내부에서 동작하는 방식</li>
<li>브라우저가 직접 WEB-INF/views/post-form.jsp에 접근하는 게 아니라,
  서블릿이 내부적으로 JSP를 실행하고, 그 결과를 브라우저에 전달하는 것!</li>
<li>즉, 브라우저는 JSP 파일의 물리적인 위치를 몰라도 되고, 오직 최종 HTML만 받게 됨.
✔️ 가능함! (WEB-INF 내부 JSP 실행 가능) ✅</li>
</ul>
<br />

<p>2️⃣ sendRedirect()를 사용할 때</p>
<pre><code class="language-java">response.sendRedirect(&quot;/WEB-INF/views/post-form.jsp&quot;);</code></pre>
<p>🚫 이렇게 하면 404 오류 발생! 🚫</p>
<p>이유는?</p>
<ul>
<li>sendRedirect()는 새로운 요청을 발생시키고, 브라우저가 직접 해당 URL로 이동하도록 함.</li>
<li>브라우저가 /WEB-INF/views/post-form.jsp로 요청을 보냄.</li>
<li>하지만 WEB-INF 폴더는 브라우저에서 직접 접근할 수 없도록 막혀 있어서 404 오류가 발생함!</li>
</ul>
<p>❌ 불가능함! (WEB-INF 내부 파일은 브라우저가 직접 접근 불가)</p>
<hr />
<p>📌 결론</p>
<blockquote>
<p>✔️ forward()는 서버 내부에서 JSP를 실행하고 결과를 전달하는 방식이라 WEB-INF 내부 파일을 사용할 수 있음.
✔️ sendRedirect()는 브라우저가 직접 새로운 요청을 보내는 방식이라 WEB-INF 내부 파일에 접근할 수 없음 → 404 오류 발생!</p>
</blockquote>
<p>💡 즉, WEB-INF 내부 파일을 실행하려면 반드시 forward()를 사용해야 함! 🚀🔥</p>
<blockquote>
<p>forward는 url을 직접적으로 변경시키는게 아니라 걍 path의 jsp에 접근해 데이터를 조장한 뒤 그걸 response해서 html을 브라우저에 띄우는 거고
sendRedirect는 예를 들어 사용자가 post로 비즈니스 로직을 처리한 다음 새로운 url로 (ex)/save 로 연결시키면 그 주소에 연결된 servlet(controller)를 GET요청으로 호출하고 거기서 원하는 jsp로 연결시키는겨</p>
</blockquote>
<hr />
<h2 id="📌-정리하면">📌 정리하면…</h2>
<h3 id="🔹-forward">🔹 forward()</h3>
<p>✔️ URL은 바뀌지 않음 (사용자가 입력한 URL 그대로 유지)
✔️ 서버 내부에서만 동작 (브라우저는 변경된 걸 모름)
✔️ 서블릿 → JSP를 실행해서 request 데이터를 활용 → 결과를 response로 브라우저에 보냄
✔️ 기존 request를 유지한 채 JSP에서 동적으로 HTML 생성</p>
<p>👉 즉, forward()는 단순히 서버 내부에서 JSP 실행 후, 그 결과만 response로 보냄!</p>
<hr />
<h3 id="🔹-sendredirect">🔹 sendRedirect()</h3>
<p>✔️ 새로운 요청이 발생하면서 브라우저의 URL이 변경됨
✔️ 기존 request는 사라지고 새로운 GET 요청이 생성됨
✔️ 비즈니스 로직 처리 후, 다른 컨트롤러(서블릿)로 이동할 때 사용
✔️ 사용자에게 다른 페이지로 이동하도록 요청하는 방식</p>
<p>👉 즉, sendRedirect()는 브라우저가 새로운 URL로 다시 요청을 보내면서, 거기서 새로운 비즈니스 로직을 수행하고 결과 페이지로 이동!</p>