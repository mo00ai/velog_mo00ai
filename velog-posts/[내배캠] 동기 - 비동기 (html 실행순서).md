<p>드디어 이 개념에 대해 이해했다......근데 안정확할 수도 있고
나만을 위해 만든 정리본임</p>
<br />

<hr />
<br />

<p>동기</p>
<ul>
<li>순차적으로 진행됨 -&gt; 다음 작업이 지연됨</li>
</ul>
<p>비동기 </p>
<ul>
<li>작업 순서를 조정함. 동시진행해서 동기의 단점을 보완
근데!!!! <strong>기본적으로 동기 코드들 다 진행되고 맨 마지막에 실행</strong></li>
<li><em>이벤트 루프*</em>라는 놈이 글케 정함 ㅇㅇ</li>
</ul>
<br />

<p>예를 들면</p>
<pre><code class="language-js">console.log(&quot;1. 동기 코드 실행 시작&quot;);

setTimeout(() =&gt; {
    console.log(&quot;3. 비동기 코드 실행 (2초 후)&quot;);
}, 2000);

console.log(&quot;2. 동기 코드 실행 끝&quot;);</code></pre>
<pre><code>1. 동기 코드 실행 시작
2. 동기 코드 실행 끝
3. 비동기 코드 실행 (2초 후)</code></pre><p>이런 식으로 1,2 동기 코드들이 실행되면 3 비동기가 젤 마지막에 실행됨</p>
<p>그럼 여기서</p>
<blockquote>
<p>엥? 비동기가 뭔가 동기보다 효율적으로 코드를 활용해서 더 좋은 거 같은디 이건 별로 인거 아닌가? 맨 마지막에 고정으로 실행되면 어따 써 했는데</p>
</blockquote>
<blockquote>
<p>비동기 발전 과정은
저런 거에 -&gt; promise -&gt; async, await 으로 발전한다
처음엔 비동기 코드 순서 지정을 못했는데  나중엔 개발자가 순서 지정할 수 있도록 발전한거임</p>
</blockquote>
<p>그럼 여기서 또</p>
<blockquote>
<p>엥? 그래 지금은 async 사용해서 개발자가 순서 지정할 수 있도록 한다 치자
그럼 async 개발 전 과거엔 비동기 코드를 왜 썼는데? 쓸모 없잖아</p>
</blockquote>
<p>그건 바로!!</p>
<br />

<p>비동기 코드들이 주로 <strong>ui, ajax 관련해서 사용됐기 때문임!</strong>
이제 이해가 가쥐?</p>
<br />

<h4 id="html">html</h4>
<p>HTML 파일이 브라우저에서 읽힘 (위에서 아래로 순차적으로 실행됨).
DOM 트리(DOM Tree) 생성
태그들이 해석되면서 DOM 요소가 만들어짐.
document.addEventListener(&quot;DOMContentLoaded&quot;, function() { ... }) 실행 가능!
CSSOM (CSS Object Model) 생성
CSS가 로드되고 적용됨 (스타일 반영됨).
이미지 &amp; 리소스 로드
<code>&lt;img&gt;</code> 태그의 이미지, 동영상, 웹폰트 등의 외부 리소스를 다운로드함.
window.onload 실행</p>
<br />

<p>그니까 그 전에 비동기 코드를 썼던 개발자들은
html/css/데이터 등 모든게 다 준비되면 그 뒤에</p>
<p>✔ 이벤트 처리 → 클릭, 스크롤, 키보드 입력 등
✔ 애니메이션 &amp; 타이머 → setTimeout(), setInterval()
✔ AJAX 요청 (fetch 등장 전) → XMLHttpRequest 사용해서 서버와 데이터 주고받기</p>
<p>이 처리들을 할 수 있으니까 이를 위해 사용된 거임</p>
<br />

<p>근데 ajax에 대한 데이터 처리 관리를 좀 더 심화하기 위해
조금도 개발자가 개입한 발전한 형태의 promise, async같은게 도입된거임!</p>
<br />

<hr />
<br />

<h4 id="dom-요소들은-또-무엇이더냐">DOM 요소들은 또 무엇이더냐?</h4>
<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;ko&quot;&gt;
&lt;head&gt;
    &lt;title&gt;DOM 요소 예제&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;h1 id=&quot;title&quot;&gt;안녕하세요!&lt;/h1&gt;
    &lt;button id=&quot;btn&quot;&gt;클릭&lt;/button&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
<p>이게 기본 html</p>
<pre><code class="language-html">&lt;html&gt;
 ├── &lt;head&gt;
 │     ├── &lt;title&gt;
 ├── &lt;body&gt;
 │     ├── &lt;h1 id=&quot;title&quot;&gt;
 │     ├── &lt;button id=&quot;btn&quot;&gt;</code></pre>
<p>DOM(Document Object Model)이란, HTML을 객체(노드)로 표현한 구조!
즉, 웹 페이지를 JavaScript에서 조작할 수 있도록 만든 트리 구조</p>
<p>이렇게 만들어야</p>
<pre><code class="language-javascript">// h1 요소 가져오기
const title = document.getElementById(&quot;title&quot;);
console.log(title.innerText);  // &quot;안녕하세요!&quot;

// 버튼 요소 가져오기
const button = document.getElementById(&quot;btn&quot;);
button.addEventListener(&quot;click&quot;, function () {
    title.innerText = &quot;클릭했어요!&quot;;  // h1 내용 변경</code></pre>
<p>javascript에서 조작할 수 있음</p>