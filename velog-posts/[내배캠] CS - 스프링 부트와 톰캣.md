<h1 id="웹-애플리케이션-흐름">웹 애플리케이션 흐름</h1>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/0da2b27a-abf2-473e-9361-4a44858dfcf8/image.png" /></p>
<ul>
<li>사용자가 HTTP 요청을 보내면 웹 서버에서는 정적 리소스를, WAS에선 DB와 연동하여 여러 애플리케이션 로직을 수행 후 동적 리소스를 반환해서 응답함.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/e3f5b17a-e7ad-4c50-9eb0-a8cee86a43fa/image.png" /></p>
<ul>
<li>이 때 개발자가 개발에만 집중할 수 있게 다른 업무들을 WAS가 지원하는 서블릿 객체에게 위임하여 편리하게 개발하도록 함</li>
</ul>
<br />

<hr />
<br />

<h1 id="서블릿-컨테이너">서블릿 컨테이너</h1>
<ul>
<li>이 때 <code>서블릿을 지원하는 WAS</code> -&gt; <code>서블릿 컨테이너</code>라고 함</li>
<li>서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 생명주기를 관리함<blockquote>
<p>대표적인 경량 서블릿 컨테이너이자 WAS가 바로 <strong>톰캣</strong></p>
</blockquote>
</li>
</ul>
<hr />
<h2 id="아파치">아파치</h2>
<ul>
<li>Apache HTTP Serve 오픈 소스 소프트웨어 그룹인 아파치 소프트웨어 재단에서 만든 웹서버 프로그램</li>
<li>정적타입(HTML, CSS, 이미지 등)의 데이터만을 처리하기 때문에 아파치 등장 이후 톰캣을 만듦.</li>
</ul>
<h2 id="톰캣">톰캣</h2>
<ul>
<li>JAVA EE 기반으로 만들어졌으며, JSP와 Servlet을 구동하기 위한 서블릿 컨테이너 역할을 수행</li>
<li>아파치서버와는 다른 응용프로그램과 상호 작용 등 동적인 기능들을 사용하며 DB연결, 애플리케이션 로직 처리 후 JSP 등을 사용하여 동적으로 페이지를 생성 후 클라이언트에게 응답한다.</li>
</ul>
<h2 id="아파치-톰캣">아파치 톰캣</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/5523d26d-a0e2-4322-b928-13956e9df3c2/image.png" /></p>
<ul>
<li>기본적으로 위처럼 아파치와 톰캣의 기능은 나뉘어져 있지만, 톰캣 안에 있는 컨테이너를 통해 일부 아파치의 기능을 발휘하기 때문에 보통 아파치 톰캣으로 합쳐서 부르곤 한다.</li>
</ul>
<blockquote>
<p>그래서 과거엔 아파치 - 프론트엔드, 톰캣- 백엔드로 요청을 분담해서 작업함.
톰캣이 편의를 위해 아파치의 기능을 포함하고 있어도 역할 분리하는 형태가 많았음
‼️ 하지만 이는 과거의 방법</p>
</blockquote>
<p><strong>과거 사용 예시</strong>
클라이언트 요청
     ↓
Apache HTTP Server   정적 파일 처리
     ↓                동적 요청은
Tomcat (WAS)        프록시로 전달
     ↓
Spring, JSP, Servlet 등</p>
<p>-mod_jk, mod_proxy_ajp 같은 모듈로 연결</p>
<ul>
<li>정적 요청은 빠르게 처리하고, 동적은 Tomcat으로 넘김</li>
</ul>
<br />

<p><strong>현재 사용 예시 - 스프링 부트 내장 사용</strong>
클라이언트 요청
     ↓
Spring Boot + 내장 톰캣</p>
<ul>
<li>톰캣만으로도 정적 리소스 서빙 가능</li>
<li>성능에도 큰 문제 없음</li>
<li>Spring boot 덕에 <code>별도 설정 할 필요 없음</code></li>
</ul>
<blockquote>
<p>엄청난 정적 트래픽 처리(이미지 서버), 이미 Apache-Tomcat 조합으로 구축되어있는 경우 등 툭수한 상황에제외하고는 Springboot에 내장된 단독 톰캣만 사용하는 추세</p>
</blockquote>
<hr />
<h1 id="spring-boot-내장-톰캣">Spring boot 내장 톰캣</h1>
<h2 id="과거-방식-외장-톰캣">과거 방식 (외장 톰캣)</h2>
<ol>
<li>STS/이클립스로 Spring MVC 프로젝트 작성</li>
<li>WAR 파일로 패키징 (빌드 or export) - 프로젝트를 압축시켜서 갖다 붙여넣도록</li>
<li>외장 톰캣 설치 (홈페이지에서 설치)</li>
<li>webapps/ 폴더에 WAR 복사</li>
<li>톰캣 실행 → 자동 배포됨</li>
<li>웹 브라우저로 접속해서 확인</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/bd5a8f16-365c-4505-b387-e21a0b699fcd/image.png" /></p>
<p><code>webapps</code></p>
<ul>
<li>애플리케이션 저장소</li>
<li>이 곳에 저장되어있는 .war나 디렉토리 구조는 톰캣 실행시 자동 배포</li>
<li>이 곳에 있는 파일을 톰캣이 웹 애플리케이션으로 인식하고 실행하는 거임</li>
</ul>
<p>참고 : <a href="https://wecanit.tistory.com/36">https://wecanit.tistory.com/36</a>
<a href="https://dev-handbook.tistory.com/32">https://dev-handbook.tistory.com/32</a></p>
<blockquote>
<p>진짜 복잡함... 톰캣에 롬복에 다른 라이브러리까지 해야하면 프로젝트 설정에만 하루죙일 걸림</p>
</blockquote>
<hr />
<h2 id="현재-방식---spring-boot">현재 방식 - Spring boot</h2>
<ul>
<li>외장 톰캣에 프로젝트를 갖다 붙인 과거와는 달리</li>
<li>현재는 Spring boot에 톰캣이 jar(압축파일)로 내장되어 있음</li>
</ul>
<h3 id="spring-boot">Spring boot</h3>
<ul>
<li>최소한의 설정으로 스프링 기반의 애플리케이션을 독립 실행할 수 있도록 돕는 프레임워크</li>
<li>이러한 프레임워크가 되기 위해 톰캣을 내장함.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/7d42e9c3-9cea-43f9-bdd0-9693fb8bf260/image.png" /></p>
<blockquote>
<p>build.gradle의 dependecies 부분
spring-boot-starter-web 안에 톰캣이 내장되어 있음</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/378d0415-e46d-4de4-b42e-529f62b210c7/image.png" /></p>
<hr />
<h2 id="스프링-부트는-어떤-과정으로-톰캣을-실행할까">스프링 부트는 어떤 과정으로 톰캣을 실행할까?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/ffb3e680-241b-49d9-b673-5d738c7f1c8e/image.png" /></p>
<ol>
<li>스프링 웹 프로젝트를 실행 함</li>
</ol>
<ul>
<li>springapplication.java 파일을 run함</li>
</ul>
<ol start="2">
<li><p>스프링 어플리케이션 인스턴스 생성</p>
</li>
<li><p>createApplicationContext() 실행</p>
</li>
</ol>
<ul>
<li>현재 애플리케이션에 적합한 컨텍스트를 생성하는 createApplicationContext() 메서드를 실행</li>
</ul>
<ol start="4">
<li>ServletWebServerApplicaitonContext 생성</li>
</ol>
<ul>
<li>이 메서드에선 내장 웹서버를 설정하고 구동하는 인스턴스를 생성</li>
</ul>
<ol start="5">
<li>Context 내 createWebServer() 메서드 실행</li>
</ol>
<ul>
<li>TomcatServletWebServerFactory 인스턴스 생성</li>
</ul>
<ol start="6">
<li>getWebServer() 실행</li>
</ol>
<ul>
<li>드디어 <strong>Tomcat 인스턴스 생성</strong></li>
<li>톰캣 서버 수명 주기 모니터링 및 관리, 설정</li>
</ul>
<ol start="7">
<li>톰캣 웹 서버 실행, 종료를 제어
<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/522fc059-5d67-4ed4-a9b6-6d6ffcd9ed4f/image.png" /></li>
</ol>
<ul>
<li>6에서 만든 톰캣 인스턴스를 웹서버 초기화 메서드에 사용하면서 본격적으로 톰캣 서버가 실행됨</li>
</ul>
<blockquote>
<p>잠깐! ApplicationContext가 뭔가요?</p>
</blockquote>
<ul>
<li>스프링 전체 환경과 객체(bean)을 관리하는 핵심 컨테이너</li>
<li>스프링이 애플리케이션을 구동할 때, 객체들을 생성(Bean), 의존성 주입, 설정 정보를 가지고 있는 중앙관리자.</li>
</ul>
<hr />
<h2 id="톰캣-내부-구조">톰캣 내부 구조</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/a1b82ccb-39a6-4db6-b079-20f866aa4c61/image.png" /></p>
<p><code>간단 설명</code></p>
<ul>
<li>HTTP 요청 수신 (Coyote) (단순 수신)</li>
<li>서블릿 실행 환경 제공 (Catalina) (서블릭 실행해서 로직 수행 후 결과 담아 코요테 넘김)</li>
<li>우리가 만든 Controller 호출 (Spring의 DispatcherServlet 등)</li>
<li>응답 전송</li>
</ul>
<br />

<p><code>구동 순서</code></p>
<p>🌐 브라우저: <a href="http://localhost:8080/hello">http://localhost:8080/hello</a> 요청
        ↓
🐶 Coyote (커넥터): </p>
<ul>
<li><p>8080 포트에서 HTTP 요청 수신</p>
</li>
<li><p>요청(Request) / 응답(Response) 객체 생성</p>
</li>
<li><p>Catalina에게 전달</p>
<p> ↓</p>
</li>
</ul>
<p>🐱 Catalina (서블릿 컨테이너 엔진): </p>
<ul>
<li><p>요청 URL 기반으로 어떤 서블릿 실행할지 판단</p>
</li>
<li><p>DispatcherServlet 실행 (Spring이라면)</p>
</li>
<li><p>내부 애플리케이션 로직 (Controller, Service 등) 실행</p>
<p> ↓</p>
</li>
</ul>
<p>🧠 애플리케이션 로직 처리 완료</p>
<pre><code>   ↓</code></pre><p>📦 Catalina:</p>
<ul>
<li><p>응답 데이터(HttpServletResponse) 준비 완료</p>
</li>
<li><p>다시 Coyote에게 전달</p>
<p> ↓</p>
</li>
</ul>
<p>📤 Coyote: </p>
<ul>
<li>응답(Http Response)을 클라이언트(브라우저)로 전송</li>
</ul>
<br />
<br />

<hr />
<p>출처 : <a href="https://velog.io/@kdhyo/Apache-Tomcat-%EB%91%98%EC%9D%B4-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EC%A7%80">https://velog.io/@kdhyo/Apache-Tomcat-%EB%91%98%EC%9D%B4-%EB%AC%B4%EC%8A%A8-%EC%B0%A8%EC%9D%B4%EC%A7%80</a></p>