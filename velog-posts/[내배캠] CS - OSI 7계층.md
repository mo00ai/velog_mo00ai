<h2 id="osi">OSI</h2>
<ul>
<li>Open System Interconnection</li>
<li>국체표준화기구(ISO)가 1977년에 정의한 <strong>서로 다른 컴퓨터들이 데이터를 주고받을 수 있도록 표준화된 규칙</strong></li>
</ul>
<h2 id="만들어진-계기">만들어진 계기</h2>
<ul>
<li>네트워크 기술이 발전하면서 컴퓨터 간의 통신이 가능해짐</li>
<li>다양한 회사들이 각기 다른 방식의 통신 프로토콜을 개발</li>
<li>문제: 서로 다른 프로토콜을 사용하면 데이터를 주고받아도 해석할 수 없음<ul>
<li>📌 마치 서로 다른 언어를 사용하는 사람들이 대화하는 것과 같음</li>
</ul>
</li>
<li>이 문제를 해결하기 위해 국제적으로 통일된 '공용어'인 OSI 모델이 등장<ul>
<li>누구나 이 규칙(OSI 계층)을 따르면, 서로 다른 시스템 간에도 원활하게 통신 가능</li>
</ul>
</li>
</ul>
<blockquote>
<p>즉, OSI 모델은 네트워크 통신의 언어를 표준화한 국제 규칙이자,
컴퓨터 간 <strong>&quot;서로 말이 통하게 만든 약속&quot;</strong></p>
</blockquote>
<hr />
<h2 id="osi-7계층">OSI 7계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/c9e2a696-0a4e-4c71-8d58-9f4bc74cb816/image.png" /></p>
<ul>
<li>OSI 는 7계층으로 나뉘어짐<ul>
<li><ol start="7">
<li>Applicaiton Layer : 응용 계층</li>
</ol>
</li>
<li><ol start="6">
<li>Presentation Layer : 표현 계층</li>
</ol>
</li>
<li><ol start="5">
<li>Session Layer : 세션 계층</li>
</ol>
</li>
<li><ol start="4">
<li>Transport Layer : 전송 계층</li>
</ol>
</li>
<li><ol start="3">
<li>Network Layer : 네트워크 계층</li>
</ol>
</li>
<li><ol start="2">
<li>Data Link Layer : 데이터 링크 계층</li>
</ol>
</li>
<li><ol>
<li>Physical Layer : 물리 계층</li>
</ol>
</li>
</ul>
</li>
</ul>
<p><code>OSI 7계층이 적용되는 데이터 통신 상황</code></p>
<ol>
<li><p>웹 어플리케이션(우리 학습)</p>
</li>
<li><p>이메일</p>
</li>
<li><p>파일 전송</p>
</li>
<li><p>메시징 서비스</p>
</li>
<li><p>온라인 게임 </p>
</li>
</ol>
<p>등등</p>
<hr />
<h2 id="7-applicaiton-layer--응용-계층">7. Applicaiton Layer : 응용 계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/f2a92cbb-ec1c-405d-b211-56730231ecfb/image.png" /></p>
<ul>
<li>ex) 사용자가 Hi 라는 문자열을 보냄</li>
<li>ex) Web application에선 사용자가 크롬에 <a href="http://www.naver.com%EC%9D%84">www.naver.com을</a> 검색함(HTTP 요청)    </li>
</ul>
<hr />
<h2 id="6-presentation-layer--표현-계층">6. Presentation Layer : 표현 계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/ba933aa2-8e1b-4d84-8cf3-3e43fea958f2/image.png" /></p>
<ul>
<li>데이터를 응용계층 표현(문자열)에서 컴퓨터가 이해할 수 있는 표현(아스키코드)으로 변환해주는 계층.</li>
<li>데이터의 인코딩과 디코딩이 이루어짐</li>
<li>ex) 문자열을 ASCII 코드로 변환 <ul>
<li>Hi -&gt; 72, 105</li>
</ul>
</li>
</ul>
<hr />
<h2 id="5-session-layer--세션-계층">5. Session Layer : 세션 계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/2d3e3bc0-0552-4806-b6b7-2c73dae5bdf0/image.png" /></p>
<ul>
<li><p>통신하는 두 컴퓨터의 연결을 관리하고 중간에 끊기면 이어주는 처리를 함</p>
</li>
<li><p>세션 충돌 방지등을 담당</p>
</li>
</ul>
<hr />
<h2 id="4-transport-layer--전송-계층">4. Transport Layer : 전송 계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/be493351-7d53-4a61-be83-374ca74ca5b4/image.png" /></p>
<ul>
<li>데이터 전달 시 큰 규모의 데이터는 잘게 쪼개서 패킷 단위로 전송</li>
<li>패킷이 잘 전송됐는지 확인, 유실된 패킷은 재전송</li>
<li>TCP/UDP도 여기에 포함</li>
</ul>
<hr />
<h2 id="3-network-layer--네트워크-계층">3. Network Layer : 네트워크 계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/546b7d65-68a6-4d6d-b351-24f4abddb3d4/image.png" /></p>
<ul>
<li>그림처럼 복잡하고 많은 네트워크 경로 중 가장 빠르고 효율적인 경로를 파악하고 결정함</li>
<li>IP 주소(출발지:나, 목적지:서버)로 목적지를 파악함</li>
</ul>
<hr />
<h2 id="2-data-link-layer--데이터-링크-계층">2. Data Link Layer : 데이터 링크 계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/65ed1fb6-02e4-4621-88c4-6a44a1fb4463/image.png" /></p>
<p>네트워크 계층과의 차이점</p>
<ul>
<li><p>네트워크 : 전체적인 경로</p>
</li>
<li><p>데이터 링크 : 물리적인 기기들 사이의 경로 </p>
</li>
<li><p>패킷을 프레임(fram)으로 구성하고
각 프레임의 에러 검사와 수정 시행</p>
</li>
<li><p>MAC 주소를 사용해서 데이터를 전송</p>
</li>
</ul>
<blockquote>
<p>컴퓨터는 데이터를 물리적인 신호(0과 1)로 인식해야함.
<code>프레임</code>이 데이터를 물리적 형태(0과1)로 바꿔줌으로써 물리적 통신이 가능하게함(물리 계층)
MAC 주소는 네트워크 안에서 정확한 장치로 데이터를 전달.</p>
</blockquote>
<hr />
<h2 id="1-physical-layer--물리-계층">1. Physical Layer : 물리 계층</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/5df1bb3b-0a1f-4d26-a89e-39fc6aa3d558/image.png" /></p>
<ul>
<li>비트 단위의 0과 1을 물리적인 on과 off의 <code>전기신호</code>로 바꿔줌</li>
<li>ex) 0 전압없음, 1 전압있음</li>
<li>이로써 케이블, wifi등 물리적인 수단을 타고 최종적으로 서버에 도착</li>
</ul>
<hr />
<h2 id="캡슐화와-역캡슐화">캡슐화와 역캡슐화</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/d820e971-baae-485b-9fdf-2af3fe67a574/image.png" /></p>
<ul>
<li><p>여기까지의 과정을 <code>캡슐화</code>라고 부름</p>
</li>
<li><p>그리고 서버가 물리신호를 받고 다시 역순으로 HTTP메시지로 만드는 걸(1단계-&gt; 7단계로 올라가는) 걸 역캡슐화라고 부름</p>
</li>
<li><p>이렇게 HTTP 요청을 읽고 HTTP 응답 준비</p>
</li>
<li><p>또 서버에서 HTTP 응답을 똑같이 7-&gt;1계층을 거쳐 사용자 PC로 전송</p>
</li>
<li><p>브라우저가 HTTP 응답을 받아 렌더링 함</p>
</li>
</ul>
<hr />
<h2 id="osi-7계층을-우리가-알아야-하는-이유">OSI 7계층을 우리가 알아야 하는 이유</h2>
<ul>
<li>에러가 어디서 나는지 디버깅할 때 정확한 위치를 짚을 수 있음</li>
<li>HTTP, TCP, IP가 왜 필요한지 체감할 수 있음</li>
<li>네트워크 기반 서비스를 설계할 수 있음</li>
<li>각 계층을 이해함으로써 네트워크 문제를 빠르게 추적하고 해결할 수 있음</li>
</ul>
<hr />
<blockquote>
<p>출처
<a href="https://www.youtube.com/watch?v=gA1KsJ2ak10&amp;list=LL&amp;index=7">https://www.youtube.com/watch?v=gA1KsJ2ak10&amp;list=LL&amp;index=7</a></p>
</blockquote>