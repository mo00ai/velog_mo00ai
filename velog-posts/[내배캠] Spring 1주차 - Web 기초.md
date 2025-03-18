<h2 id="web-기초">Web 기초</h2>
<h2 id="dnsdomain-name-system">DNS(Domain Name System)</h2>
<aside>
📚 DNS는 도메인 이름과 IP 주소를 서로 변환하는 역할을 수행한다. 즉, 사람이 읽을 수 있는 도메인 이름을 컴퓨터가 읽을 수 있는 IP 주소로 변환한다.

</aside>

<ul>
<li><p><strong>DNS가 나오게된 이유</strong></p>
<ol>
<li>컴퓨터 간의 통신을 위해선 IP 주소가 필요하다.<ul>
<li>IP 주소는 사이트마다 특징도 없고 길어서 외우기가 힘들다.</li>
<li>IP 주소가 변경된다면 새로운 IP에 접근할 수 없다.</li>
</ul>
</li>
<li>IP는 변경되는 주소이다.<ul>
<li>일반적으로 가정집에서 사용되는 IP는 유동IP 입니다.</li>
<li>만약 IP가 변경된다면 새로운 IP에 접근할 수 없습니다.</li>
</ul>
</li>
</ol>
</li>
<li><p><strong>DNS 동작 순서</strong></p>
<ol>
<li>원하는 이름의 도메인을 구매 후, DNS 서버에 등록한다.
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/1a9eb9da-e7be-438c-a949-53a4a5c34990/image.png" /></li>
<li>도메인 명을 입력하면 DNS 서버는 IP 주소를 반환한다.
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/62c40a0b-f752-48fa-abca-c62802e2c972/image.png" /></li>
<li>IP가 변경되면 DNS 서버에 등록된 IP 주소만 바뀌면 된다.</li>
<li>우리는 IP주소의 형태가 아닌 <a href="https://spartacodingclub.kr/">https://spartacodingclub.kr/</a> 의 도메인 이름 형태로 웹에 접속한다.<ul>
<li>일반적으로 URL이라 알고있는것이 바로 DNS를 활용한 예이다.</li>
</ul>
</li>
</ol>
</li>
</ul>
<hr />
<h3 id="uriuniform-resource-identifier">URI(Uniform Resource Identifier)</h3>
<aside>
📚 **인터넷 자원(Resource)을 나타내는 고유 식별자(Identifier)를 뜻한다.**

</aside>

<ul>
<li><strong>Uniform</strong>: 자원(Resource)을 식별하는 통일된 방식을 의미한다.</li>
<li><strong>Resource</strong>: 자원(페이지, 텍스트, 이미지, 동영상, 파일 등)을 의미한다.</li>
<li><strong>Identifier</strong>: 식별자를 의미한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/a1b2cd68-6390-47d9-92de-3da3d0af17f5/image.png" /></p>
<blockquote>
<p>💡 ISBN 이란? International Standard Book Number로 국제 표준도서번호를 뜻한다.</p>
</blockquote>
<ul>
<li><strong>URI(Uniform Resource Identifier)</strong><ul>
<li>인터넷 자원(Resource)을 식별할 수 있는 문자열을 뜻한다.</li>
<li>URI는 Locator, Name 혹은 둘 다 추가로 분류될 수 있다.</li>
</ul>
</li>
</ul>
<ul>
<li><p><strong>URL(Uniform Resource Locator)</strong></p>
<ul>
<li>자원(Resource)의 위치를 의미한다. ex) 튜터가 있는곳은 사무실</li>
<li>일반적으로 도메인주소로 알려져있다.</li>
<li>프로토콜을 포함한다.(<a href="https://spartacodingclub.kr/">https://spartacodingclub.kr/</a>)</li>
</ul>
</li>
<li><p><strong>URL 방식의 한계</strong></p>
<ul>
<li>자원(Resource)의 위치를 변경하면 기존 URL은 사용할 수 없다.</li>
<li>브라우저 검색창에 스파르타 코딩클럽 홈페이지를 검색하면<code>https://spartacodingclub.kr/</code> 사이트가 노출된다.</li>
<li>만약 이 주소를 <code>https://spartacodingclub2.kr/</code> 로 바꾼다면 기존 경로를 아는 사람들은 검색 페이지의 URL이 업데이트되지 않으면 페이지를 찾을 수 없다.</li>
<li>이러한 한계를 극복하기 위해서 <strong>URN</strong>이 등장하게 되었다.</li>
</ul>
</li>
<li><p><strong>URN(Uniform Resource Name)</strong></p>
<ul>
<li>자원(Resource)의 이름(Name)을 의미한다. ex) 튜터</li>
<li>리소스의 위치가 변경되어도 이름으로 리소스를 찾기 때문에 잘 동작한다.</li>
<li>프로토콜을 포함하지 않는다.</li>
<li>URN으로 실제 리소스에 접근하는 방법은 대중화 되어있지 않다.</li>
</ul>
</li>
</ul>
<blockquote>
<p>💡 현재 대부분은 대중화된 URL을 사용하여, URI를 URL과 같은 의미로 사용한다.</p>
</blockquote>
<hr />
<h3 id="urluniform-resource-locator">URL<strong>(Uniform Resource Locator)</strong></h3>
<aside>
📚 프로토콜을 포함한, 자원(Resource)의 위치를 나타낸다.

</aside>

<ul>
<li><strong>URL 구조</strong></li>
</ul>
<blockquote>
<p>⭐ <strong>scheme:[//[user[:password]@]host[:port]][/path][?query][#fragment]</strong>
<a href="https://www.google.com:443/search?q=%EC%8A%A4%ED%8C%8C%EB%A5%B4%ED%83%80+%EC%BD%94%EB%94%A9%ED%81%B4%EB%9F%BD/">https://www.google.com:443/search?q=스파르타+코딩클럽/</a></p>
</blockquote>
<ul>
<li><p><strong>scheme</strong></p>
<ul>
<li>주로 프로토콜을 사용한다. 웹에서는 <code>http, https, ftp</code>를 주로 사용한다.</li>
<li>참고 : <code>http**s**</code>는 <code>http</code>에 보안(Secure)을 추가한 것.</li>
</ul>
</li>
<li><p><strong>user[:password]</strong></p>
<ul>
<li>사용자 정보</li>
<li>URL은 보안에 취약하여 사용하지 않는다.</li>
</ul>
</li>
<li><p><strong>host[:port]</strong></p>
<ul>
<li>호스트명 : 도메인 명(<a href="http://www.google.com">www.google.com</a>) 또는 IP 주소를 직접 사용한다.</li>
<li>http : 80, https : 443 포트 사용</li>
<li>포트는 일반적으로 생략한다.</li>
</ul>
</li>
<li><p><strong>[/path]</strong></p>
<ul>
<li><p>리소스의 경로</p>
</li>
<li><p><strong>계층 구조</strong>로 구성되어있다.</p>
</li>
<li><p><em>ex) <code>프로토콜://쇼핑몰주소/products/macbookPro</code>*</em></p>
</li>
<li><p><em>ex) <code>https://nbcamp.spartacodingclub.kr/backend</code>*</em></p>
</li>
</ul>
</li>
<li><p><strong>[?query]</strong></p>
<ul>
<li><p><strong>key=value</strong> 형태로 구성된다.</p>
</li>
<li><p><strong>Query Parameter, Query String</strong> 이라고도 한다.</p>
<ul>
<li>두 가지 모두 같은 말입니다. 자주 혼용되는 단어이니 잘 기억해주세요.</li>
</ul>
</li>
<li><p>?로 시작되고 &amp;으로 구분된다.</p>
</li>
<li><p><em>ex)*</em> <code>?key1=value1**&amp;**key2=value2**&amp;**key3=value</code></p>
</li>
</ul>
</li>
<li><p><strong>[#fragment]</strong></p>
<ul>
<li><p>html 내부 북마크 등에 사용한다.</p>
<ul>
<li>전달받은 URL로 접속 시 특정 위치(fragment)로 이동할 수 있음</li>
</ul>
</li>
<li><p><em>ex)*</em> <code>http://www.google.com/index.html#image</code></p>
</li>
</ul>
</li>
</ul>
<hr />
<h2 id="정리">정리</h2>
<h3 id="브라우저에-url을-입력하면-어떤일이">브라우저에 URL을 입력하면 어떤일이?!?</h3>
<aside>
⭐ 웹 브라우저에 URL을 입력하면 어떤 순서로 요청이 흘러가는지 알아봅니다.

</aside>

<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/f60d2ff6-d56d-4f1e-97d1-f24873d04d49/image.png" /></p>
<ol>
<li>[<code>https://www.google.com:443/search?q=스파르타+코딩클럽&amp;hl=ko</code>] URL을 입력한다.
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/b54a0961-1cf9-4ae8-b363-c5384ec5c6bb/image.png" /></li>
</ol>
<ol start="2">
<li><strong>DNS 서버</strong>를 조회하여 <code>www.google.com</code> 에 해당하는 IP 주소를 응답받는다.<ul>
<li>포트 번호는 생략되어있다.</li>
<li><code>https</code>에서 사용되는 <strong>PORT</strong>는 <strong>443</strong>이다.</li>
</ul>
</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/bb0f777d-8b0b-46fc-853f-2064f8488f4b/image.png" /></p>
<ol start="3">
<li>웹 브라우저에서 <strong>HTTP 요청 메세지</strong>를 생성한다.<ul>
<li>스파르타 코딩클럽 검색해줘! 하는것과 같다.</li>
</ul>
</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/1812eedb-52f3-424e-9e26-79987307ac27/image.png" /></p>
<ol start="4">
<li>요청 패킷(HTTP 메세지가 포함되어 있다)을 구글 서버로 전송한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/55add544-31df-44d7-b187-2c62309512ba/image.png" /></p>
<ol start="5">
<li>구글 서버에서 HTTP 요청 메세지를 기반으로 <strong>응답 HTTP 메세지</strong>를 만들어 응답한다.<ul>
<li>어디보자.. 스파르타 코딩클럽 검색해달라고? 그래 검색 결과는 이거야!</li>
</ul>
</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/6ccc7994-2bcc-40f4-b320-b3191e93f6b6/image.png" /></p>
<ol start="6">
<li>응답패킷 도착 → HTML 이 응답으로 온다.<ul>
<li>응답 결과가 브라우저에 그려진다.</li>
</ul>
</li>
</ol>