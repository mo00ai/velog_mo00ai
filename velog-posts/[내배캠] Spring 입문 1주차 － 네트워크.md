<h1 id="spring-프로젝트">Spring 프로젝트</h1>
<ul>
<li>Spring Framwork를 사용해서 Web Application을 만드는 것</li>
</ul>
<p>1주차 강의를 통해 Web Application의 구조와 네트워크 통신에 대해서 배우며
Web 전반에 대한 이해를 돕기 위한 네트워크 기초지식을 확립함</p>
<hr />
<h1 id="네트워크-지식이-필요한-이유">네트워크 지식이 필요한 이유</h1>
<ol>
<li><p>우리는 사용자가 요청을 했을 때 해당 요청에 대한 응답을 수행하는 프로그램 즉, 서버를 개발하게 됩니다. </p>
</li>
<li><p>사용자의 요청에서 시작하여 우리가 만든 서버에 도착하고 다시 사용자에게 응답이 되돌아가는 흐름을 잘 파악하고 있다면 서버 개발에 큰 도움이 됩니다.</p>
</li>
<li><p>인터넷 브라우저(클라이언트)와 서버가 데이터를 주고받는 통신 방법인 HTTP(HyperText Transfer Protocol)는 결국, Web 기반에서 동작하기 때문에 네트워크에 대한 지식은 필수입니다.</p>
</li>
</ol>
<p><code>프로토콜(Protocol)이란?</code></p>
<ul>
<li>복잡한 인터넷 세상에서 컴퓨터와 컴퓨터끼리 데이터를 주고받기 위하여 정한 통신규약.</li>
</ul>
<hr />
<h1 id="네트워크">네트워크</h1>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/0e81470e-6c79-4800-8fc6-cda2a24462ab/image.png" /></p>
<ul>
<li>초기 컴퓨터 간 네트워크 연결은 물리적인 형태로 이루어졌습니다.<ul>
<li>USB 케이블과 같은 형태로 물리적으로 연결되면 서로 데이터를 주고받을 수 있습니다.</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/a946e198-b441-43ff-a36f-071a72f8f730/image.png" /></p>
<ul>
<li>하지만, 만약 컴퓨터와 컴퓨터 사이의 거리가 아주 멀리 있다면?<ul>
<li>나의 컴퓨터는 한국에 위치하고, 통신하고자 하는 컴퓨터가 이탈리아에 위치한다면?
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/942e709e-6c75-428b-bf19-1ee1a2128b44/image.png" /></li>
</ul>
</li>
</ul>
<blockquote>
<p>인터넷이 이런 문제점을 해결함</p>
</blockquote>
<hr />
<h2 id="1️⃣-네트워크---인터넷">1️⃣ 네트워크 - 인터넷</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/778908fe-9567-49c9-b539-c917360865a7/image.png" /></p>
<p><strong>인터넷(Internet)</strong>
-인터넷 프로토콜 스위트(TCP/IP)를 기반으로 하여 전 세계적으로 연결되어있는 컴퓨터 네트워크 통신망</p>
<blockquote>
<p>인터넷을 활용해서 멀리 있는 컴퓨터 간의 통신도 가능해짐</p>
</blockquote>
<table>
  <tr>
  <td><img src="https://velog.velcdn.com/images/mo00ai/post/05a05457-4f9f-4d0d-806c-3d64fc29292f/image.png" /></td>
  <td><img src="https://velog.velcdn.com/images/mo00ai/post/6feec9b1-1ce6-4e1e-bfb8-697a65d10e22/image.png" /></td>
  </tr>
</table>

<p>이처럼 해저 케이블, 인공위성으로 유무선 인터넷 통신이 가능해짐</p>
<blockquote>
<p>유/무선 방식으로 이름에 걸맞는 World Wide Web(www)가 구축됨</p>
</blockquote>
<hr />
<h2 id="2️⃣-네트워크---인터넷-프로토콜-ip">2️⃣ 네트워크 - 인터넷 프로토콜 IP</h2>
<h3 id="인터넷-프로토콜i-udp-user-datagram-protocol">인터넷 프로토콜(I### UDP (User Datagram Protocol)</h3>
<ul>
<li>인터넷이 통하는 네트워크에서 어떤 정보를 수신하고 송신하는 통신에 대한 규약</li>
</ul>
<p><strong>🤔IP? 들어본 적 있는데 192.168.0.1과 같은 숫자가 작성된 주소가 아닌가요?</strong></p>
<ul>
<li>그건 IP 자체가 아닌 IP에 필요한 고유 주소인 IP 주소</li>
<li>IP 주소를 쉽게 말하면 각 기기 간의 통신을 식벼할 수 있는 <code>전화번호</code>임</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/4656be35-9ff4-4d4f-ae8c-667f3583cc58/image.png" /></p>
<blockquote>
<p>인터넷 세상속에서는 위 그림 보다 더 복잡하고 많은 단계들을 거치며 데이터를 통신하게 됨
😲그럼 어케야 데이터를 온전하게 잘 전달할 수 있을까?
‼️‼️<code>최소한의 규칙</code>이 필요합니데이‼️‼️</p>
</blockquote>
<hr />
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/8308e0d5-12f4-4247-9f65-b2ccdb0d0909/image.png" /></p>
<p><strong>IP주소</strong></p>
<ul>
<li>각 기기 간의 통신을 식별할 수 있는 전화번호</li>
<li><code>최소한의 규칙</code>을 지킬 수 있는 이유는 <code>IP주소</code> 덕분이다~(따봉 IP주소야 고마워)<blockquote>
<p>인터넷 통신 시에는 지정한 IP 주소에 데이터를 <code>Packet</code> 이라는 단위로 전달합니다.</p>
</blockquote>
</li>
</ul>
<hr />
<p align="center">
  <img src="https://velog.velcdn.com/images/mo00ai/post/873efdc7-fea8-4b46-b77e-f1e4b6896fa7/image.png" width="60%" />
</p>

<p><strong>Packet</strong></p>
<ul>
<li>데이터를 전달하는 단위</li>
<li><code>소스IP(출발지)</code>, <code>대상IP(도착지)</code>를 포함하고 있어서 어떤 컴퓨터에 데이터를 전송할지 판별할 수 있음</li>
<li>Paket은 크게 헤더, 페이로드, 트레일러(수신여부 포함)으로 구분됨</li>
<li>데이터를 주기만 하는 것이 아닌 받고 ‼️<strong><em>응답한다!!!</em></strong>‼️</li>
</ul>
<hr />
<p><strong>IP 방식의 문제점</strong></p>
<ul>
<li>인터넷 프로토콜(IP)를 사용하여 데이터를 통신할 수 있게 되었다.<blockquote>
<p>하지만 IP만으로 모든 것이 해결되지 않음</p>
</blockquote>
</li>
</ul>
<ol>
<li><p><strong>애플리케이션 구분</strong></p>
<ul>
<li>대상 컴퓨터의 어떤 프로그램에 사용될 데이터인지 구분할 수 없다.<img src="https://velog.velcdn.com/images/mo00ai/post/13a8a262-ef18-407b-82b1-b685e10be0b7/image.png" width="60%" />
</li>
</ul>
</li>
<li><p><strong>비연결성</strong></p>
<ul>
<li>수신 대상의 현재 상태에 상관없이 데이터를 전송한다.<img src="https://velog.velcdn.com/images/mo00ai/post/593344e3-2562-4142-95f8-962ac25dabca/image.png" width="60%" />
</li>
</ul>
</li>
<li><p><strong>비신뢰성</strong></p>
<ul>
<li>패킷이 소실되는 경우가 발생한다.</li>
<li>패킷의 손상여부를 송신, 수신측 모두 알 수 없다.<img src="https://velog.velcdn.com/images/mo00ai/post/86c2e361-285c-49ec-8e91-7a2c828e77e8/image.png" width="60%" />    


</li>
</ul>
</li>
</ol>
<ul>
<li>패킷의 순서가 뒤죽박죽이 되어 섞여서 들어오는 경우가 발생한다.<ul>
<li>용량이 큰 데이터의 경우 패킷이 여러개로 나뉘어져 전송된다.<img src="https://velog.velcdn.com/images/mo00ai/post/e3aa6997-5e18-4410-8c56-ca6a061bdf94/image.png" width="60%" />
→ 패킷이 손실되거나, 오류가 발생하여도 데이터의 재전송을 진행하지 않습니다.

</li>
</ul>
</li>
</ul>
<blockquote>
<p>이런 ❌<code>인터넷 프로토콜(IP)</code>❌ 문제점들을 해결해주는 것이 바로 🙆‼️<code>TCP 프로토콜</code>‼️🙆</p>
</blockquote>
<hr />
<h2 id="3️⃣-네트워크---tcp">3️⃣ 네트워크 - TCP</h2>
<h3 id="tcptransmission-control-protocol">TCP(Transmission Control Protocol)</h3>
<ul>
<li>서버와 클라이언트 간에 데이터를 <code>신뢰성</code> 있게 전달하기 위해 만들어진 프로토콜. </li>
<li>IP 방식에서의 패킷 손실, 오류가 생겨도 데이터를 재전송하지 않는 등의 문제를 보완</li>
</ul>
<hr />
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/9242f09c-7525-4f63-bbb5-3d024474d952/image.png" /></p>
<p><strong>3 Way HandShake</strong></p>
<ol>
<li>SYN 접속 요청</li>
<li>ACK 요청 수락 → ACK가 없다면 연결 실패.</li>
<li>ACK → ACK 함께 데이터 전송 가능</li>
</ol>
<blockquote>
<ul>
<li>1컴퓨터가 2컴퓨터에게 syn 접속 요청</li>
</ul>
</blockquote>
<ul>
<li>2 컴퓨터 ACT 요청 수락 및 1컴퓨터에게 syn 접속 요청 보냄</li>
<li>1 컴퓨터 ack 요청 수락</li>
</ul>
<ul>
<li>SYN, ACK 용어 설명<ul>
<li><strong>SYN (Synchronize)</strong><ul>
<li>클라이언트가 서버에게 연결을 요청하는 첫 번째 단계이다.</li>
<li>클라이언트는 서버에게 &quot;연결을 시작하고 싶다&quot;는 의사를 나타내기 위해 SYN 플래그가 설정된 패킷을 전송한다.</li>
<li>패킷에는 시퀀스 번호도 포함되어 있고 데이터 전송 순서를 관리할 준비를 한다.</li>
</ul>
</li>
<li><strong>ACK (Acknowledge)</strong><ul>
<li>서버가 클라이언트의 SYN 패킷을 받고, 이를 확인했다는 신호를 보내는 단계이다.</li>
<li>서버는 클라이언트의 SYN 요청을 수락하며, 자신도 연결을 시작하고 싶다는 뜻을 담아 SYN 플래그와 함께 ACK 플래그가 설정된 패킷을 클라이언트에게 전송한다.</li>
<li>이때, 서버는 클라이언트의 시퀀스 번호에 1을 더한 값을 ACK로 응답한다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>⚠️<code>주의사항</code></p>
</blockquote>
<ul>
<li>3 Way HandShake는 물리적으로 연결되는 것이 아닙니다.</li>
<li>최소한의 논리적인 연결을 통하여 연결이 되었다고 가정하는 것 입니다.</li>
</ul>
<hr />
<p><strong>데이터 전송 여부</strong>
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/cbb00dff-24c7-40bf-b5bf-6126c056ba6b/image.png" />
→ TCP를 통해 통신하면 데이터를 잘 받았다는 응답을 반환해준다.</p>
<hr />
<p><strong>패킷 순서</strong>
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/4fd3fa78-00e4-42a3-8f11-8726c6cef0e4/image.png" /> 
→ 패킷이 나뉘어져 올지라도 순서를 보장한다.</p>
<blockquote>
<p>TCP는 신뢰성이 있지만 연결하는 과정, 데이터 전송에 시간이 많이 소요된다. TCP는 현재 단계 이상의 최적화를 하기 힘들다. (최소한의 논리적인 연결이 필요하기 때문) 
→ ‼️3 way handshake 과정을 거치는 만큼 속도가 느리다.</p>
</blockquote>
<hr />
<h2 id="4️⃣-네트워크---udp">4️⃣ 네트워크 - UDP</h2>
<h3 id="udp-user-datagram-protocol">UDP (User Datagram Protocol)</h3>
<ul>
<li>비연결형, 신뢰성이 없는 전송 프로토콜</li>
<li>TCP의 신뢰성 보장 기능은 많은 애플리케이션에 유용했지만, 실시간 통신이나 스트리밍 애플리케이션에서는 <code>빠른 전송</code>이 중요했기 때문에 UDP는 이러한 요구를 충족하기 위해 개발되었다.</li>
</ul>
<blockquote>
<p>현대에서는 UDP를 많이 사용하는 추세이다. HTTP3 에서 채택한 방식, HTTP에도 버전이 있다!
ex) 실시간 스트리밍 서비스, 온라인 게임, 인터넷 전화 
특징 : 실시간성 보장 중요</p>
</blockquote>
<ul>
<li><p><strong>UDP의 특징</strong></p>
<ol>
<li><p>IP 방식과 거의 비슷하다. </p>
<ul>
<li>3 way handshake를 하지 않는다.<ul>
<li>데이터 전송, 응답, 순서를 보장하지 않는다.(비신뢰성)</li>
</ul>
</li>
</ul>
</li>
<li><p>추가적인 기능이 거의 없다.</p>
<ul>
<li>기능이 없고 연결을 하지 않는 대신 속도가 빠르다.</li>
</ul>
</li>
<li><p><strong>IP와 차이점</strong>으로 <strong>PORT</strong> 가 존재한다.</p>
<ul>
<li>TCP에도 <strong>PORT</strong>가 존재한다.</li>
</ul>
</li>
<li><p>데이터 무결성 검사 → <strong>체크섬(Checksum)</strong>을 포함하고 있다.</p>
<ul>
<li>잘못된 데이터가 전송되지 않도록 만들어준다.</li>
</ul>
</li>
</ol>
</li>
</ul>
<hr />
<h2 id="5️⃣-네트워크---port">5️⃣ 네트워크 - PORT</h2>
<h3 id="port">PORT</h3>
<ul>
<li>같은 IP 내에서 프로세스 구분을 하기 위해서 사용</li>
</ul>
<blockquote>
<p>🤔 같은 IP에서 동시에 여러가지 프로그램이 실행되고 있다면 IP 주소가 같은데, 패킷의 도착지를 어떻게 식별할 수 있을까요?
-&gt; 현재 전송하고자 하는 패킷이 어떤 곳에 필요한 패킷인지 IP만으로는 해결이 되지 않습니다. 이때 프로그램을 구분하기 위해 사용되는 것이 바로 <strong>PORT</strong>입니다!</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/14b3f09e-6803-4ee5-91d0-6b0e9b217731/image.png" /></p>
<blockquote>
<p>→  쉽게 말해서 PORT는 아파트 호수와 같은 역할을 수행한다. </p>
</blockquote>
<p align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/70f774e1-6b0b-4b52-bd67-314d17dcffb8/image.png" width="60%" />


<hr />
<ul>
<li><p><strong>TCP/IP Packet 구조</strong></p>
<ul>
<li><p>소스 PORT, 대상 PORT를 포함한다.</p>
<p align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/2194a994-9a95-4bf2-910a-f8287cd2ecf5/image.png" width="60%" />


</li>
</ul>
</li>
</ul>
<ul>
<li><strong>자주 사용되는 PORT</strong><ol>
<li><strong>0 ~ 65535 할당 가능</strong></li>
<li><strong>이미 사용되고 있는 포트 (0 ~ 1023)</strong> <ul>
<li>국제 도메인 관리기구에 의해 관리된다, 사용하지 않는것이 좋다.</li>
<li><code>FTP</code> - 20, 21 (TCP)</li>
<li><code>SSH</code> - 22 (TCP)</li>
<li><code>텔넷</code> - 23 (TCP)</li>
<li><code>SMTP</code> - 25 (TCP)</li>
<li><code>DNS</code> - 53 (TCP/UDP)</li>
<li><code>DHCP</code> - 67 (UDP)</li>
<li><code>HTTP</code> - <strong>80 (TCP)</strong></li>
<li><code>HTTPS</code> - <strong>443 (TCP)</strong></li>
<li><code>RDP</code> - 3389 (TCP/UDP)</li>
</ul>
</li>
</ol>
</li>
<li>실제 개발을 진행할 때 사용되지 않는 나머지 포트를 사용하여 개발하면 됩니다.</li>
</ul>
<hr />