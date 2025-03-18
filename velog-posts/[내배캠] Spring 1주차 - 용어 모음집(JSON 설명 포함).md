<h1 id="용어-모음집-1강">용어 모음집 1강</h1>
<h2 id="프로그래밍-명명규칙casing">프로그래밍 명명규칙(Casing)</h2>
<p>📚 프로그래밍 세계에서는 각각의 언어, 환경에 알맞는 명명 규칙이 존재한다.</p>
<ol>
<li><p><strong>snake_case</strong></p>
<ul>
<li>Python이나 <strong>DB Table, Column</strong>에 사용된다.</li>
<li>문자와 문자 사이를 <code>_</code> 언더바로 이어준다.</li>
<li>모든 단어는 소문자이거나 대문자이다.</li>
</ul>
</li>
<li><p><strong>camelCase</strong></p>
<ul>
<li><strong>Java</strong>, JavaScript, TypeScript에서는 변수, 함수, 메서드 이름을 만들 때 사용한다.</li>
<li>문자와 문자 사이를 대문자로 이어준다.</li>
</ul>
</li>
<li><p><strong>PascalCase</strong></p>
<ul>
<li>대부분의 프로그래밍 언어에서 클래스 이름을 지정하는 데 파스칼 케이스가 사용된다.</li>
<li>문자의 처음 시작을 대문자로 한다.</li>
<li>문자와 문자 사이를 대문자로 이어준다.</li>
</ul>
</li>
<li><p><strong>kebab-case</strong></p>
<ul>
<li>문자와 문자 사이를 <code>-</code> 대시로 이어준다.</li>
<li>모든 단어는 소문자이다.</li>
</ul>
</li>
</ol>
<ul>
<li><strong>Java의 명명법</strong></li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/7502dfc6-a5a9-4448-8bf1-ac9cb7aa9ef6/image.png" /></p>
<hr />
<h2 id="json">JSON</h2>
<p>📚 JSON은 클라이언트와 서버가 통신할 때 사용하는 데이터 양식이다. 클라이언트와 서버가 사용하는 언어에 관계 없이 통일된 데이터를 주고받을 수 있도록 만들어준다.</p>
<p>💡과거 웹 초기 시절부터 사용된 XML의 단점
    - 헤더와 태그 등의 여러 요소로 가독성이 떨어짐
    - 불필요한 용량을 잡아먹음</p>
<blockquote>
<p>이에 대응해 간결하고 통일된 양식으로 각광을 받고 있는 것이 <code>JSON</code>이다.</p>
</blockquote>
<ul>
<li><strong>요약</strong><ul>
<li>JSON은 사람, 기계 모두 이해하기 쉬우며 용량이 작다.</li>
<li>XML을 대체해서 데이터 전송 등에 많이 사용한다.</li>
<li>마치 전세계 공통어로 영어를 사용하는것처럼 Web의 세계에서는 JSON(<strong>J</strong>ava<strong>S</strong>cript <strong>O</strong>bject <strong>N</strong>otation)을 공통어로 사용한다.</li>
</ul>
</li>
</ul>
<hr />
<ul>
<li><strong>그림예시</strong>
 <img alt="" src="https://velog.velcdn.com/images/mo00ai/post/f65247b9-0f82-4de2-8d1a-91b30b07aba3/image.png" /><ul>
<li>클라이언트 to 서버의 통신에 JSON을 사용한다.</li>
<li>서버 to 서버의 통신에도 JSON을 사용한다.</li>
</ul>
</li>
</ul>
<hr />
<ul>
<li><p><strong>MSA(MicroService Architecture)</strong></p>
<ul>
<li><p>아주 작은 단위로 서비스를 잘게 나누어 운영하는 아키텍처</p>
<p><a href="https://www.sktenterprise.com/bizInsight/blogDetail/dev/2714">SKT Enterprise</a></p>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/53f9fea0-76a0-44ce-9a1b-0a24e28342da/image.png" /></p>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>👉 해당 아키텍처를 가지게 되면 구성된 Application마다 어떠한 언어를 사용하는지에 상관없이 서로 통신을 할 수 있는데 이것이 가능한 이유는 <strong>JSON 형태로 데이터 통신을 하기 때문이다</strong>.</p>
</blockquote>
<hr />
<ul>
<li><p><strong>JSON 구조</strong></p>
<pre><code class="language-jsx">  {
    &quot;user&quot;: [
      {
        &quot;first_name&quot;: &quot;wonuk&quot;,
        &quot;last_name&quot;: &quot;Hwang&quot;,
        &quot;age&quot;: 100,
        &quot;phone_agree&quot;: false,
        &quot;hobby&quot;: [&quot;Java&quot;, &quot;Spring&quot;]
      },
      {
        &quot;firstName&quot;: &quot;sparta&quot;,
        &quot;lastName&quot;: &quot;Team&quot;,
        &quot;age&quot;: 200,
        &quot;phone_agree&quot;: true,
        &quot;hobby&quot;: [&quot;React&quot;, &quot;Spring&quot;, &quot;Node&quot;]
      },
    ]
  }</code></pre>
<ul>
<li><strong><code>snake_case, camelCase</code></strong> 모두 사용이 가능하다.<ul>
<li>우리가 만드는 Application 내에서 변환해주는 <strong>무엇인가</strong>가 있다.</li>
</ul>
</li>
<li><strong><code>key-value</code> 형태</strong>로 구성되어 있다.</li>
<li><code>null, number, string, array, object, boolean</code> 형태의 데이터를 사용할 수 있다.</li>
</ul>
</li>
</ul>
<br />


<hr />
<h3 id="scale-up-scale-out">Scale Up, Scale Out</h3>
<p>📚 서버의 성능 향상을 위한 두 가지 방법이다.</p>
<ul>
<li><p><strong>Scale Up</strong></p>
<ul>
<li>수직적 확장
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/cccb1b77-71fc-4bc0-abd0-92f11f7fb813/image.png" /></li>
<li>단일 서버의 하드웨어의 사용을 높인다. (CPU, Memory 등의 스펙을 높인다)</li>
<li>요청에 대한 처리를 더욱 빠르게 할 수 있도록 만든다.</li>
</ul>
</li>
<li><p><strong>Scale Out</strong></p>
<ul>
<li>수평적 확장
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/59392b6f-80b3-4b34-a6de-4a75d1c2be42/image.png" /></li>
<li>같은 사양의 서버(인스턴스)를 여러 대 배치한다.</li>
<li>동시에 더 많은 사용자 요청을 처리할 수 있도록 만든다.</li>
</ul>
</li>
</ul>
<hr />
<h3 id="stateful-stateless">Stateful, Stateless</h3>
<aside>
📚 클라이언트와 서버간의 통신 상태(state) 유지 여부에 따라 나뉘는 특성이다.

</aside>

<ul>
<li><p><strong>Stateful(상태 유지)</strong></p>
<ul>
<li>클라이언트의 상태를 유지한다.
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/9aad96e9-4759-4bcc-af18-05b8b79b2429/image.png" /></li>
<li>상담원은 수강생의 요청들을 기억(<strong>상태 유지</strong>)하여 다음 질문들에 대한 처리가 가능하다.</li>
</ul>
</li>
<li><p><strong>Stateful 방식의 문제점</strong></p>
<ul>
<li>같은 서버가 유지되어야 한다.</li>
<li>상태를 유지하고 있던 서버가 종료된다면?
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/71603d31-c515-44a3-a93d-551aa3bce886/image.png" /></li>
<li>서버는 다양한 이유로 동작하지 않을 수 있다.<ul>
<li>시스템 에러, 비지니스 로직 문제, 리소스 부족 문제 등</li>
</ul>
</li>
<li>요청 트래픽이 몰리게되면 상태를 유지하는것에 Resource가 많이 소모된다.<ul>
<li>리소스가 버티지 못하면 서버가 종료되거나, 다음 요청에 대한 처리가 느려진다.</li>
</ul>
</li>
</ul>
</li>
<li><p><strong>Stateless(무상태)</strong></p>
<ul>
<li>클라이언트의 상태를 유지하지 않는다.
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/a592c0cc-d225-44ae-9a7f-41d45799d834/image.png" /></li>
<li>어떻게 서로 다른 상담원들이 수강생의 요청을 알 수 있을까요?</li>
</ul>
</li>
<li><p><strong>Stateless 방식의 실제 요청방식</strong>
  <img alt="" src="https://velog.velcdn.com/images/mo00ai/post/44df979d-abe9-463f-b55f-c0dd77c517f6/image.png" /></p>
<ul>
<li>강의를 신청하려는 수강생이 상담한 직원이 아닌 다른 직원이 와도 신청할 수 있게 되었다.</li>
</ul>
</li>
<li><p><strong>Stateless 방식의 장단점</strong>
  <img alt="" src="https://velog.velcdn.com/images/mo00ai/post/7d5a263b-3435-4ab8-8fa8-0cf270ac0a04/image.png" /></p>
<ul>
<li>장점<ul>
<li>같은 서버를 유지할 필요가 없다.</li>
<li>Scale Out 수평 확장성이 높다.<ul>
<li>갑자기 요청량이 증가하여도 서버를 증설 하기 쉽다.</li>
</ul>
</li>
</ul>
</li>
<li>단점<ul>
<li>클라이언트가 데이터를 추가적으로 전송해야 한다.<ul>
<li>전송되는 데이터의 양이 많아진다.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li><p><strong>Stateless 방식의 한계점</strong></p>
<ul>
<li>WebApplication을 만들때 서버의 확장성을 고려하여 최대한 Stateless하게 만들어야 한다.</li>
<li>하지만, 실제로는 로그인과 같은 <code>상태를 유지</code>해야하는 경우가 발생한다.</li>
<li>추후에 배울 <strong>Cookie, Session, Token</strong> 등을 활용하여 이러한 한계를 극복한다.<ul>
<li>상태 유지를 최소화 시켜야 한다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<hr />
<h3 id="connection-connectionless">Connection, Connectionless</h3>
<p>📚 클라이언트와 서버 간의 연결(Connection) 유지 여부에 따라 나뉘는 특성이다.</p>
<ul>
<li><p><strong>Connection(연결)</strong>
  <img alt="" src="https://velog.velcdn.com/images/mo00ai/post/b00d60b9-9d6a-4a69-be8e-a5b199cbf232/image.png" /></p>
<ul>
<li>서버는 클라이언트와 연결을 유지하기 위해서 자원을 소모한다.</li>
<li>하지만, 수많은 사람들이 서비스를 이용해도 실제 서버에서 동시에 처리하는 요청은 작다.<ul>
<li>클라이언트 2, 3이 아무런 요청이 없어도 연결을 유지한다.</li>
</ul>
</li>
</ul>
</li>
<li><p><strong>Connection 장단점</strong></p>
<ul>
<li>장점<ul>
<li>새로운 연결 과정을 거치지 않아도 된다.</li>
<li>그만큼 요청에 대한 응답 속도가 빨라진다.</li>
</ul>
</li>
<li>단점<ul>
<li>클라이언트가 지속적으로 요청을 보낼거라는 보장이 없다.</li>
<li>즉, 연결을 위한 자원이 낭비된다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<hr />
<ul>
<li><strong>Connectionless(비연결)</strong>
  <img alt="" src="https://velog.velcdn.com/images/mo00ai/post/589b147b-2e3b-420c-b089-504af0e962d6/image.png" /><ul>
<li>클라이언트와 서버는 연결을 유지하지 않는다.</li>
<li>서버는 최소한의 자원만을 사용한다.
ex) 브라우저가 켜진 상태에서 인터넷이 종료되어도 홈페이지가 정상적으로 노출된다.</li>
</ul>
</li>
</ul>
<ul>
<li><p><strong>Connectionless 장단점</strong></p>
<ul>
<li><p>장점</p>
<ul>
<li>서버 자원을 효율적으로 사용할 수 있다.</li>
</ul>
</li>
<li><p>단점</p>
<ul>
<li><p>요청이 추가적으로 오게되면 연결(3 way handshake)을 새로 해야한다.</p>
<p>  → 요청에 대한 응답 시간이 증가한다.</p>
</li>
<li><p>웹 사이트의 HTML, CSS, JS, 이미지 등의 정적 자원 모두를 다시 다운로드 한다.</p>
<p>  → <strong>캐시, 브라우저 캐싱로 해결한다. 쉽게 말해 임시저장 (추후 다룰 예정)</strong></p>
</li>
<li><p>현재는 <strong>HTTP 지속연결(Persistent Connections)</strong>로 문제를 해결한다.</p>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<hr />
<ul>
<li><strong>HTTP 지속연결(Persistent Connections)</strong><ul>
<li>하나의 요청에 필요한 요청들이 모두 응답될 때 까지 연결을 유지한다.</li>
<li>연결을 한번만 맺고 끊기 때문에, Connectionless 방식보다 연결 횟수가 적다.
  → 그만큼 속도가 빨라졌다.
ex) HTML 요청 + CSS 요청 + JS 요청 + 이미지 요청
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/009cafb1-90e2-4ef8-bcda-4b16b2aefa97/image.png" /></li>
</ul>
</li>
</ul>