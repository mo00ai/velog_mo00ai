<p>📚강의 들으면서 헷갈렸던 부분 정리</p>
<hr />
<h1 id="쿼리-파라미터-vs-requestbody-쓰는-경우">쿼리 파라미터 vs RequestBody 쓰는 경우</h1>
<table>
<thead>
<tr>
<th>요청 방식</th>
<th>데이터 위치</th>
<th>URL 바뀜?</th>
<th>주로 사용하는 경우</th>
</tr>
</thead>
<tbody><tr>
<td><strong>쿼리 파라미터 (<code>GET</code>)</strong></td>
<td><code>?key=value</code> (URL에 포함)</td>
<td>✅ O</td>
<td>검색, 필터링, 페이지네이션</td>
</tr>
<tr>
<td><strong>요청 본문 (<code>POST</code>, <code>PUT</code>)</strong></td>
<td>HTTP body에 포함</td>
<td>❌ X</td>
<td>로그인, 회원가입, 데이터 저장</td>
</tr>
</tbody></table>
<blockquote>
<p>민감 정보는 url에 보이면 안되니 숨길 수 있게 http body 에 포함시켜서 데이터를 보냄</p>
</blockquote>
<hr />
<h2 id="spring-bean-등록">Spring Bean 등록</h2>
<ul>
<li>Spring이 객체를 생성하고, 관리할 수 있도록 등록하는 것</li>
</ul>
<hr />
<h1 id="component-어노테이션">@Component 어노테이션</h1>
<ul>
<li>✔️ Spring이 자동으로 객체를 생성하고 관리하도록 하는 어노테이션!</li>
<li>✔️ 해당 클래스를 Spring Bean으로 등록함.</li>
<li>✔️ @Component가 붙은 클래스는 Spring이 자동으로 스캔(@ComponentScan)해서 Bean으로 등록!</li>
</ul>
<pre><code class="language-java">@Component // Spring이 이 클래스를 Bean으로 관리함
public class MyService {</code></pre>
<ul>
<li>✔️ 이 코드에서 MyService는 <strong>Spring이 자동으로 생성해서 관리하는 객체(Bean)</strong>가 됨.</li>
<li>✔️ 다른 곳에서 이 클래스를 @Autowired로 주입하면 Spring이 자동으로 객체를 제공함.</li>
<li>MyService 객체는 개발자가 new로 직접 만들 필요 없이, Spring이 자동으로 생성하고 관리함!<blockquote>
<p>싱글톤 패턴을 기본적으로 적용함</p>
</blockquote>
</li>
</ul>
<h3 id="📌-결론-spring-bean을-왜-쓰는-거야"><strong>📌 결론: Spring Bean을 왜 쓰는 거야?</strong></h3>
<p>1️⃣ <strong>객체를 <code>new</code>로 직접 만들 필요가 없음!</strong><br />   → <code>@Component</code>만 붙이면 Spring이 자동으로 생성 &amp; 관리<br />2️⃣ <strong>객체를 필요할 때 <code>@Autowired</code>로 쉽게 가져다 쓸 수 있음!</strong><br />   → 복잡한 객체 생성을 신경 쓸 필요가 없어짐<br />3️⃣ <strong>Spring이 객체를 한 번만 생성해서 관리 (싱글턴 패턴 기본 적용!)</strong><br />   → 불필요한 객체 생성을 줄이고 메모리 관리 최적화  </p>
<hr />
<h3 id="📌-한-줄-요약"><strong>📌 한 줄 요약</strong></h3>
<p>👉 <strong>Spring Bean은 Spring이 대신 만들어서 관리해주는 객체야!</strong><br />👉 <code>@Component</code>를 붙이면 <strong>Spring이 자동으로 객체를 생성 &amp; 관리</strong>하고,<br />👉 <code>@Autowired</code>로 다른 곳에서 <strong>간편하게 가져다 쓸 수 있음!</strong> 🚀😊 </p>
<hr />
<h3 id="📌-component의-확장-어노테이션">📌 <code>@Component</code>의 확장 어노테이션</h3>
<p>Spring에서는 역할별로 좀 더 구체적인 <code>@Component</code> 어노테이션이 있음.  </p>
<table>
<thead>
<tr>
<th>어노테이션</th>
<th>역할</th>
</tr>
</thead>
<tbody><tr>
<td><code>@Component</code></td>
<td>기본적인 Bean 등록</td>
</tr>
<tr>
<td><code>@Service</code></td>
<td><strong>서비스 계층</strong>(비즈니스 로직) 관리</td>
</tr>
<tr>
<td><code>@Repository</code></td>
<td><strong>DAO 계층</strong>(데이터 저장/조회) 관리</td>
</tr>
<tr>
<td><code>@Controller</code></td>
<td><strong>Spring MVC의 컨트롤러</strong> 관리</td>
</tr>
</tbody></table>
<p>✔️ 사실 <strong>이 확장 어노테이션들도 내부적으로 <code>@Component</code> 포함하고 있음!</strong>  </p>
<h3 id="📌-그런데-왜-controller-대신-component를-쓰는-거야">📌 그런데 왜 <code>@Controller</code> 대신 <code>@Component</code>를 쓰는 거야?</h3>
<p>일반적으로 Spring MVC에서는 <strong>컨트롤러에 <code>@Controller</code>를 사용</strong> 
그런데 <strong>Spring 2.5 이전 버전에서는 <code>@Controller</code>가 없었고, <code>@Component</code>를 사용해야 했음.</strong>  </p>
<p>즉, <strong>Spring의 옛날 방식(구형 Spring MVC)에서 사용하던 방법이야.</strong><br />지금은 <code>@Controller</code>를 사용하는 게 일반적이지만, 옛날 코드에서는 이런 방식도 볼 수 있어!  </p>
<hr />
<h3 id="📌-component를-컨트롤러에-사용하는-경우-요약">📌 <code>@Component</code>를 컨트롤러에 사용하는 경우 요약</h3>
<p>1️⃣ <code>@Component(&quot;/example-controller&quot;)</code>를 사용하면 <strong>Spring이 이 클래스를 Bean으로 등록하고, URL까지 자동 매핑</strong><br />2️⃣ 하지만 <strong>Spring MVC에서는 <code>@Controller</code> + <code>@RequestMapping</code>을 쓰는 게 더 일반적</strong><br />3️⃣ <code>@Component</code>를 컨트롤러에 다는 방식은 <strong>구형(Spring 2.5 이전) 방식이라 지금은 잘 쓰이지 않음!</strong>  </p>
<p>✅ <strong>즉, 가능은 하지만, 최신 Spring에서는 <code>@Controller</code>를 쓰는 게 정석!</strong> 🚀🔥</p>
<hr />
<h2 id="requestentity-vs-requestbody-차이점">RequestEntity vs @RequestBody 차이점</h2>
<h1 id="responseentity-vs-responsebody-차이점">ResponseEntity vs @ResponseBody 차이점</h1>
<p><strong>HttpEntity 류들</strong></p>
<blockquote>
<p>요청의 바디 + 헤더 + 요청 정보를 함께 가져올 수 있음(ex)HttpStatus</p>
</blockquote>
<p><strong>Body 종류들</strong></p>
<blockquote>
<p>요청의 바디 데이터를 직접 가져옴</p>
</blockquote>
<blockquote>
<p>그래서 보통 response를 반환할 때 entity로 날림<br /><strong>http status code(ok, not exist) 반환해서 사용자가 식별할 수 있으니깐</strong></p>
</blockquote>
<hr />
<h1 id="spring-웹-프로젝트에서-예외-처리-방식-정리"><strong>Spring 웹 프로젝트에서 예외 처리 방식 정리</strong></h1>
<ol>
<li><p><strong>일단 <code>throws</code> 또는 <code>throw</code>로 예외를 던짐</strong></p>
<ul>
<li>메서드에서 <code>throws</code>를 선언하거나, 직접 <code>throw</code>로 예외를 던지면 <strong>Spring이 기본적으로 처리</strong>함.</li>
<li>특별한 처리를 하지 않으면 <code>500 Internal Server Error</code> 응답을 반환함.</li>
</ul>
</li>
<li><p><strong>Spring의 기본 예외 처리(<code>BasicErrorController</code>)가 알아서 예외를 받아서 처리</strong></p>
<ul>
<li>아무것도 설정하지 않아도 Spring이 자동으로 500 에러 응답을 줌.</li>
</ul>
</li>
<li><p><strong>명시적으로 예외 처리를 하고 싶다면?</strong></p>
<ul>
<li>특정 컨트롤러에서만 예외를 처리하려면 <code>@ExceptionHandler</code></li>
<li>전역적으로 예외를 처리하려면 <code>@ControllerAdvice</code></li>
<li><code>@RestControllerAdvice</code>를 사용하면 JSON 응답을 쉽게 반환 가능</li>
</ul>
</li>
</ol>
<blockquote>
<p>스프링에서 기본적으로 처리하는 Interval Server Error는 예외를 명시적으로 식별하기 어려움
그래서 보통 ControllerAdvice로 예외 처리를 모아둔 클래스를 선언하고, 특정 예외별로 ExceptionHandler를 단 하위 핸들러 메서드들로 각 예외를 처리해서 명시적으로 예외를 처리할 수 있도록 함(status.code나 entity.body.message를 활용해서 프론트에 예외 메세지 던짐</p>
</blockquote>
<hr />
<h3 id="✅-component는-상위-개념이고">✅ <code>@Component</code>는 <strong>상위 개념</strong>이고</h3>
<h3 id="✅-controller는-component의-하위-개념이에요">✅ <code>@Controller</code>는 <code>@Component</code>의 <strong>하위 개념</strong>이에요.</h3>
<hr />
<h3 id="🔹-component">🔹 <code>@Component</code></h3>
<ul>
<li>스프링이 관리하는 <strong>빈(bean)</strong> 으로 등록하겠다는 뜻이에요.</li>
<li>범용적으로 사용되며, 주로 <strong>직접 만든 클래스</strong>를 빈으로 등록할 때 써요.</li>
</ul>
<h3 id="🔹-controller-service-repository-등">🔹 <code>@Controller</code>, <code>@Service</code>, <code>@Repository</code> 등</h3>
<ul>
<li>전부 <code>@Component</code>를 <strong>상속한 애들</strong>이에요.<br />그래서 이 애들도 스프링이 자동으로 빈으로 등록해줘요.</li>
<li>각각의 역할이 있어서 구분해서 쓰는 거예요.</li>
</ul>
<table>
<thead>
<tr>
<th>어노테이션</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>@Controller</code></td>
<td>웹 요청 처리용 클래스 (MVC의 C)</td>
</tr>
<tr>
<td><code>@Service</code></td>
<td>비즈니스 로직 처리용 클래스</td>
</tr>
<tr>
<td><code>@Repository</code></td>
<td>DB 처리용 DAO 클래스</td>
</tr>
<tr>
<td><code>@Component</code></td>
<td>그냥 스프링 빈 등록용 (특정 역할 없이 범용적으로)</td>
</tr>
</tbody></table>
<hr />
<h3 id="💡-요약">💡 요약</h3>
<p><code>@Controller</code>는 <code>@Component</code>에 포함된 스프링 어노테이션이고, 역할이 명확한 빈을 등록하기 위해 별도로 만든 거예요.</p>
<blockquote>
<p>위에 설명했듯이 @Componant는 @Controller의 구버전. 잘 안쓰지만
쓰는 경우도 있다 바로바로</p>
</blockquote>
<blockquote>
<p>Controller, Service, Repository를 제외한 다른 기능, 클래스들을 Spring bean으로 등록해서 관리하고 싶을 때, Componant 를 닮</p>
</blockquote>
<hr />
<h2 id="autowired">Autowired</h2>
<ul>
<li>Component 어노테이션 단 객체를 객체 생성 없이(new 없이) 대입할 수 있음?</li>
</ul>
<h2 id="✅-네가-말한-걸-정리하면">✅ 네가 말한 걸 정리하면:</h2>
<blockquote>
<p><code>new KakaoSender()</code>처럼 직접 new를 해버리면<br />→ 코드에 KakaoSender가 <strong>박혀버려서</strong><br />나중에 <code>EmailSender</code>, <code>SlackSender</code> 같은 걸 쓰고 싶어도<br />→ <strong>코드를 일일이 수정해야 함</strong> (하드코딩)</p>
</blockquote>
<hr />
<h2 id="✅-근데-autowired로-di를-쓰면">✅ 근데 <code>@Autowired</code>로 DI를 쓰면?</h2>
<blockquote>
<p>어떤 Sender를 쓸지는 <strong>스프링이 주입해주는 걸로 해결</strong><br />→ 호출하는 쪽은 <strong>어떤 구현체가 오든 신경 안 써도 됨</strong><br />→ 그러니까! <strong>다형성 + 느슨한 결합</strong>이 완성됨 🔥</p>
</blockquote>
<hr />
<h2 id="🎯-정확히-말하면-다형성--di의-조합">🎯 정확히 말하면: 다형성 + DI의 조합</h2>
<h3 id="다형성">다형성</h3>
<pre><code class="language-java">public interface NotificationSender {
    void send(String msg);
}

@Component
public class KakaoSender implements NotificationSender { ... }

@Component
public class EmailSender implements NotificationSender { ... }</code></pre>
<h3 id="서비스-쪽은-이렇게만-쓰면-됨">서비스 쪽은 이렇게만 쓰면 됨</h3>
<pre><code class="language-java">@Service
public class AlarmService {
    private final NotificationSender sender;

    public AlarmService(NotificationSender sender) {
        this.sender = sender;
    }

    public void alarm() {
        sender.send(&quot;알림!&quot;);
    }
}</code></pre>
<ul>
<li>어떤 구현체가 들어오든 <code>NotificationSender</code> 인터페이스만 지키면 돼</li>
<li>이게 <strong>다형성의 힘</strong>이고,</li>
<li>그 구현체를 <strong>스프링이 알아서 주입</strong>해주는 게 DI (<code>@Autowired</code>)야</li>
</ul>
<hr />
<h2 id="💬-네-요약--정답-✅">💬 네 요약 = 정답 ✅</h2>
<blockquote>
<p>❝ new로 박아버리면 유연성이 없고,<br />@Autowired로 주입받으면 어떤 구현체가 들어오든 상관없이 사용 가능 → 이게 다형성 느낌이다 ❞</p>
</blockquote>
<blockquote>
<p>ㅇㅎ 미리 new를 해놓으면 그 객체 (ex 카카오sender) 로만 new하게 되니까 개발자가 다른 sender로 보내고 싶으면 일일이 수정하는 하드코딩이 발생하는데
autrowired를 하면 호출하는 쪽에서 아무거나 넣어줘도 되니까 사용하기가 편한거다. 이거 맞아?
약간 다형성 느낌인가</p>
</blockquote>
<hr />
<h1 id="dto-vs-entity">DTO vs Entity</h1>
<h2 id="dto-entity-분리-이유">DTO, Entity 분리 이유</h2>
<table>
<thead>
<tr>
<th>이유</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>책임 분리</strong></td>
<td>DTO는 전달 역할, Entity는 도메인 역할 → 분리 유지</td>
</tr>
<tr>
<td><strong>유지보수성</strong></td>
<td>DTO 구조 바뀌어도 Entity에 영향 없음</td>
</tr>
<tr>
<td><strong>테스트 용이성</strong></td>
<td>불필요한 객체 생성 없이 Entity 테스트 가능</td>
</tr>
<tr>
<td><strong>의도 명확성</strong></td>
<td>어떤 값이 들어가는지 코드에서 명확히 보임</td>
</tr>
</tbody></table>
<h2 id="역할-마다-반환타입-정리">역할 마다 반환타입 정리</h2>
<table>
<thead>
<tr>
<th>레이어</th>
<th>기능</th>
<th>반환타입</th>
<th>DTO 처리</th>
</tr>
</thead>
<tbody><tr>
<td>Repository</td>
<td>DB 모방 (Map) 에서 Entity 조회</td>
<td><code>Memo</code></td>
<td>❌</td>
</tr>
<tr>
<td>Service</td>
<td>비즈니스 로직 + DTO 변환</td>
<td><code>MemoResponseDto</code></td>
<td>✅</td>
</tr>
<tr>
<td>Controller</td>
<td>클라이언트 요청 처리</td>
<td><code>MemoResponseDto</code></td>
<td>✅</td>
</tr>
</tbody></table>
<blockquote>
<p>또한 엔티티는 db용, dto는 외부 응답용이라 
엔티티엔 민감정보(비밀번호, 내부상태값) 등 외부에 노출되면 안되는 것들이 포함될 수 있기 때문에 직접 클라이언트에 반환하는 건 보안상 위험함</p>
</blockquote>
<blockquote>
<p>그래서 service, controller 등 외부에 응답하는 레이어들은 가공이 가능한 dto 에 담아서 반환</p>
</blockquote>