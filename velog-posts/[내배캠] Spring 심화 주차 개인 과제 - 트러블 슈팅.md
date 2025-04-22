<p>lv4에서 많이 헤맸기 때문에 
lv4 : Interceptor, AOP 로깅 구현 중 트러블슈팅에 대해 작성하겠습니다.</p>
<h1 id="filter-interceptor-aop-구조">Filter, Interceptor, AOP 구조</h1>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/887c61df-0295-4d2d-b82c-aa49dcb48405/image.png" /></p>
<br />

<hr />
<h1 id="interceptor">Interceptor</h1>
<p><code>preHandle()</code> </p>
<ul>
<li>핸들러가 수행되기 전에 실행됩니다.</li>
<li>return 값이 ture면 다음 인터셉터or컨트롤러 호출, false면 더이상 진행하지 않는다.</li>
</ul>
<p><code>postHandle()</code> </p>
<ul>
<li>핸들러가 수행된 뒤, 뷰가 아직 반환되지 않았을 때 실행됩니다. </li>
<li>컨트롤러에서 예외 발생 시 호출되지 않는다.</li>
</ul>
<p><code>afterCompletion()</code> </p>
<ul>
<li>요청에 대한 모든 작업이 끝난 뒤, 뷰까지 반환했을 때 실행됩니다.</li>
<li>컨트롤러에서 예외 발생하여도 호출된다.</li>
</ul>
<blockquote>
<p><a href="https://jddng.tistory.com/270">https://jddng.tistory.com/270</a>
<a href="https://dev-ws.tistory.com/58">https://dev-ws.tistory.com/58</a></p>
</blockquote>
<br />

<hr />
<br />

<h2 id="1-webconfig에-등록">1. WebConfig에 등록</h2>
<pre><code class="language-java">@Configuration
@RequiredArgsConstructor
public class WebConfig implements WebMvcConfigurer {

    // ArgumentResolver 등록
    @Override
    public void addArgumentResolvers(List&lt;HandlerMethodArgumentResolver&gt; resolvers) {
        resolvers.add(new AuthUserArgumentResolver());
    }

    //Interceptor 등록
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LogInterceptor())
                .addPathPatterns(&quot;/admin/**&quot;);
    }
}</code></pre>
<blockquote>
<p>인터셉터를 등록해준다!</p>
</blockquote>
<br />

<hr />
<br />

<h2 id="2-loginterceptor-클래스를-만든다">2. LogInterceptor 클래스를 만든다</h2>
<ol>
<li>실제 인터셉터를 구현할 클래스를 만들고 <code>HandlerInterceptor</code> 인터페이스를 상속받는다</li>
<li>그러면 <code>HandlerInterceptor</code> 내 메서드를 오버라이딩 할 수 있다</li>
</ol>
<p>앞서 설명했듯이</p>
<p><code>preHandle()</code> 
<code>postHandle()</code> 
<code>afterCompletion()</code> </p>
<p>등을 상속받을 수 있는데, 요구사항엔 요청전에만 log를 남기라 해서 
이번 과제의 인터셉터엔 <code>preHandle()</code>만 필요하다.</p>
<br />

<pre><code class="language-java">@Slf4j
public class LogInterceptor implements
    HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        String userRole = (String) request.getAttribute(&quot;userRole&quot;);
        String requestURL = request.getRequestURL().toString();

        if(!userRole.equals(UserRole.ADMIN.name())) {
            throw new AuthException(&quot;관리자만 접근할 수 있습니다.&quot;);
        }

        log.info(&quot;[관리자 인증 성공 : 시각 : {}, URL : {} ]&quot;, LocalDateTime.now(), requestURL);

        return HandlerInterceptor.super.preHandle(request, response, handler);
    }

}</code></pre>
<p>그래서 이와 같은 구현을 했다</p>
<blockquote>
<p>JwtFilter에서 set해준 request의 값들을 get으로 꺼내준다.
userRole의 값이 ADMIN하고 같지 않을경우엔 권한이 없기 때문에 예외를 날려 접근을 막고
ADMIN일 경우엔 로그를 남긴다</p>
</blockquote>
<br />

<hr />
<br />

<h2 id="트러블슈팅">트러블슈팅...</h2>
<p>postman으로 해당 인터셉터가 정상 작동하는 걸 확인했지만
log는 찍히지 않았다..............</p>
<p>계속 뻘짓을 하다가 어느 순간 갑자기 됐다....
아직 이유는 모른다...</p>
<p>캐시 문제였을 것으로 추측한다....
찜찜쓰..</p>
<br />

<hr />
<br />
<br />
<br />

<hr />
<h1 id="aop">AOP</h1>
<ul>
<li>요구사항은 사용자의 요청 전후로 요청데이터, 응답데이터를 로그에 표시해주는 거다</li>
</ul>
<blockquote>
<p>그래서 @Before, @After 말고 @Around를 써줌</p>
</blockquote>
<br />

<hr />
<h2 id="어노테이션-정리">어노테이션 정리</h2>
<p><code>Aspect</code></p>
<ul>
<li>여러 클래스들에 영향을 미치는 로직의 모듈화</li>
<li>로그, 트랜잭션 관리처럼 여러 클래스들에 미치는 로직을 공통화하여 분리한 것</li>
<li>이 클래스가 Aspect를 나타내는 클래스임을 명시</li>
</ul>
<p><code>@Pointcut(&quot;execution(* com.yata.backend..*Controller.*(..))&quot;)</code></p>
<ul>
<li>부가기능을 주입할 포인트컷을 com.yata.backend 패키지의 하위 패키지에 있는 모든 Controller를 대상으로 설정</li>
</ul>
<blockquote>
<p>@Pointcut(&quot;execution(* org.example.expert.domain.comment.controller.CommentAdminController.<em>(..)) || execution(</em> org.example.expert.domain.user.controller.UserAdminController.*(..))&quot;)</p>
</blockquote>
<p>난 이런 식으로 무식하게 만들긴 함.. 두 컨트롤러에서 쓰면 되기 때문에
근디 챗 지피티한테 물어보니까</p>
<p><code>@Pointcut(&quot;execution(* org.example.expert.domain..*AdminController.*(..))&quot;)</code></p>
<p>이런 식으로 써주면
sql의 like 문처럼 
컨트롤러 클래스명에 AdminController가 있으면 경로로 잡아준다
-&gt; controller like '%AdminController%' 요런 느낌</p>
<p><code>@Around(&quot;all()&quot;)</code></p>
<ul>
<li>메서드 호출 전/후, 예외 발생 시점에 해당 부가기능(Advice) 실행</li>
<li>인자로 PointCut 메서드 명을 넣어줌</li>
</ul>
<hr />
<h2 id="의존성-주입">의존성 주입</h2>
<pre><code class="language-java">    implementation 'org.springframework.boot:spring-boot-starter-aop'</code></pre>
<hr />
<h2 id="loggingaspect-클래스-생성">LoggingAspect 클래스 생성</h2>
<ul>
<li>AOP를 구현 할 클래스 생성</li>
</ul>
<pre><code class="language-java">
@Aspect
@Component
@Slf4j
@RequiredArgsConstructor
public class LoggingAspect {

    private final ObjectMapper objectMapper;

    @Pointcut(&quot;execution(* org.example.expert.domain.comment.controller.CommentAdminController.*(..)) || execution(* org.example.expert.domain.user.controller.UserAdminController.*(..))&quot;)
    private void cut() {}

    @Around(&quot;cut()&quot;)
    public Object aroundLong(ProceedingJoinPoint joinPoint) throws  Throwable {

        //request가져오기
        HttpServletRequest request = ((ServletRequestAttributes) RequestContextHolder.getRequestAttributes()).getRequest();

        Long userId  = (Long) request.getAttribute(&quot;userId&quot;); //요청자 아이디
        String url = (String) request.getRequestURL().toString();

        String requestBody = objectMapper.writeValueAsString(joinPoint.getArgs());

        log.info(&quot;[관리자 인증 성공] \n&quot; +
                &quot;           요청자 id : {} \n&quot; +
                &quot;           요청 시각 : {} \n&quot; +
                &quot;           요청 URL : {} \n&quot; +
                &quot;           요청 requestBody : {}&quot;,
                                    userId, LocalDateTime.now(), url, requestBody);

        Object result = joinPoint.proceed();

        String responseBody = objectMapper.writeValueAsString(result);

        log.info(&quot;[관리자 인증 성공] \n&quot; +
                        &quot;           요청자 id : {} \n&quot; +
                        &quot;           요청 시각 : {} \n&quot; +
                        &quot;           요청 URL : {} \n&quot; +
                        &quot;           응답 responseBody : {}&quot;,
                userId, LocalDateTime.now(), url, responseBody);

        return  result;
    }

}</code></pre>
<br />

<pre><code class="language-java">    private final ObjectMapper objectMapper;</code></pre>
<ul>
<li>ObjectMapper를 사용하기 위해 전역변수로 선언함.</li>
<li>json 형태인 요청,응답 정보를 log에 띄워야 하기 때문에</li>
</ul>
<br />

<pre><code class="language-java">    @Pointcut(&quot;execution(* org.example.expert.domain.comment.controller.CommentAdminController.*(..)) || execution(* org.example.expert.domain.user.controller.UserAdminController.*(..))&quot;)
    private void cut() {}</code></pre>
<ul>
<li>앞서 설명했던 Pointcut</li>
<li>구글링 하다보니 이런 방법을 사용하는 사람들이 많아서 사용함</li>
<li>Pointcut 어노테이션을 사용할 void 반환 메서드를 생성한 후 후에 @Around 등 aop 구현 메서드에서 어노테이션 경로로 사용</li>
</ul>
<br />

<pre><code class="language-java">    @Around(&quot;cut()&quot;)
    public Object aroundLong(ProceedingJoinPoint joinPoint) throws  Throwable {</code></pre>
<ul>
<li>이렇게 사용함</li>
</ul>
<p><code>ProceedJoinPoint</code></p>
<ul>
<li>이 aop의 대상이 되는 메서드, 이번 과제에선 <strong>컨트롤러</strong>의 정보를 담고 있는 객체임</li>
<li>여기서 객체(메서드-&gt;컨트롤러)를 실행(Arount에선:.proceed), 파라미터 정보 반환(getArgs) 등을 할 수 있음</li>
</ul>
<br />

<pre><code class="language-java">        //request가져오기
        HttpServletRequest request = ((ServletRequestAttributes) RequestContextHolder.getRequestAttributes()).getRequest();</code></pre>
<ul>
<li>log에 출력할 정보 때문에 reqeust가 필요하다. </li>
<li>구글링 하다가 이런 방법으로 선언함</li>
</ul>
<br />

<pre><code class="language-java">        Long userId  = (Long) request.getAttribute(&quot;userId&quot;); //요청자 아이디
        String url = (String) request.getRequestURL().toString();</code></pre>
<ul>
<li>request 에서 정보 가져오기</li>
</ul>
<br />

<pre><code class="language-java">        String requestBody = objectMapper.writeValueAsString(joinPoint.getArgs());</code></pre>
<ul>
<li>joinPoint.getArgs()는 메서드에 전달된 모든 인자들을 배열 형태로 반환함</li>
<li>이 배열을 ObjectMapper.writeValueAsString()으로 직렬화하면,</li>
<li>메서드 파라미터 전체를 JSON 문자열로 변환할 수 있음</li>
</ul>
<br />

<pre><code class="language-java">        log.info(&quot;[관리자 인증 성공] \n&quot; +
                &quot;           요청자 id : {} \n&quot; +
                &quot;           요청 시각 : {} \n&quot; +
                &quot;           요청 URL : {} \n&quot; +
                &quot;           요청 requestBody : {}&quot;,
                                    userId, LocalDateTime.now(), url, requestBody);</code></pre>
<ul>
<li>요청 정보를 로깅함</li>
<li>잘못 적었는데 requestBody를 로깅한게 아니라, 메서드(컨트롤러)의 요청 정보들(파라미터)을 다 로깅한 거임</li>
</ul>
<br />

<pre><code class="language-java">        Object result = joinPoint.proceed();</code></pre>
<ul>
<li>메서드를 실행함</li>
<li>@Around 어노테이션은 컨트롤러의 요청-응답에 관여하기 때문에 꼭 이렇게 메서드를 실행 시켜줘야 함</li>
<li>result엔 joinPoint(메서드,컨트롤러)의 response가 담김</li>
<li>void일 경우엔 null이 담김</li>
</ul>
<br />

<pre><code class="language-java">        String responseBody = objectMapper.writeValueAsString(result);</code></pre>
<ul>
<li>응답을 json 문자열로 변환</li>
</ul>
<br />

<pre><code class="language-java">        log.info(&quot;[관리자 인증 성공] \n&quot; +
                        &quot;           요청자 id : {} \n&quot; +
                        &quot;           요청 시각 : {} \n&quot; +
                        &quot;           요청 URL : {} \n&quot; +
                        &quot;           응답 responseBody : {}&quot;,
                userId, LocalDateTime.now(), url, responseBody);</code></pre>
<ul>
<li>응답 데이터 로깅</li>
</ul>
<br />

<pre><code class="language-java">    return  result;</code></pre>
<blockquote>
<p>이 부분이 좀 헷갈렸다</p>
</blockquote>
<p>🤔 Filter 같은 경우엔 마지막에 doFilter()를 다시 호출해서 다음 필터를 호출하던가, 아님 컨트롤러를 호출해서 <strong>컨트롤러에서 클라이언트에게 반환할 값을 전달</strong>하는데 AOP는 왜 result, 즉 joinPoint.proceed()를 다시 반환하는 걸까? </p>
<p>🤔 AOP를 사용하면 AOP가 클라이언트에게 반환할 값을 전달하는 걸까?</p>
<blockquote>
<p>정답입니다~~</p>
</blockquote>
<br />

<h4 id="filter-vs-aop-흐름-비교-정리">Filter vs AOP 흐름 비교 정리</h4>
<br />

<p><code>Filter</code></p>
<pre><code class="language-plaintext">클라이언트 요청
    ↓
[Filter] doFilter 실행
    ↓
chain.doFilter(request, response)
    ↓
컨트롤러 실행
    ↓
응답 만들어짐 (response에 직접 작성)
    ↓
[Filter] 이후 로직 (afterFilter)
    ↓
클라이언트 응답
</code></pre>
<br />

<p><code>AOP (Around)</code></p>
<pre><code class="language-plaintext">클라이언트 요청
    ↓
필터 통과 + 디스패처서블릿 진입
    ↓
[AOP] @Around 메서드 실행
    ↓
joinPoint.proceed() → 컨트롤러 메서드 실행
    ↓
리턴된 결과를 받아서 AOP에서 후처리
    ↓
AOP에서 result를 그대로 return
    ↓
DispatcherServlet이 응답 작성
    ↓
클라이언트 응답</code></pre>
<ul>
<li>AOP는 스프링 빈 내부 메서드의 실행 자체를 감싸는 거라서, 내가 return 해줘야 실행 흐름이 마무리 됨</li>
<li>Filter는 Servlet 흐름을 타고 들어오는 요청을 거르고 넘겨주는 거라서, 응답은 내부에서 처리되기만 하면 됨</li>
</ul>
<blockquote>
<p>🤔그럼 @Around가 아니라 @Before일 때도 똑같이 응답을 넘겨줘야하냐?</p>
</blockquote>
<blockquote>
<p>no!!!! 그건 아님
@Before는 타겟 메서드가 실행되기 &quot;직전&quot; 에 단순히 끼어들기만 하기 때문</p>
</blockquote>
<br />

<table>
<thead>
<tr>
<th>어노테이션</th>
<th>설명</th>
<th>타겟 메서드 실행 여부</th>
<th>결과값에 개입 가능?</th>
<th><code>return</code> 필요 여부</th>
</tr>
</thead>
<tbody><tr>
<td><code>@Before</code></td>
<td>메서드 실행 <strong>직전</strong> 동작</td>
<td>✅ 자동 실행됨</td>
<td>❌ 못 건드림</td>
<td>❌</td>
</tr>
<tr>
<td><code>@After</code></td>
<td>메서드 실행 <strong>후</strong> 항상 실행</td>
<td>✅ 자동 실행됨</td>
<td>❌ 못 건드림</td>
<td>❌</td>
</tr>
<tr>
<td><code>@AfterReturning</code></td>
<td><strong>정상적으로 실행 완료된 경우</strong> 후처리</td>
<td>✅ 자동 실행됨</td>
<td>✅ 결과값 접근만 가능</td>
<td>❌</td>
</tr>
<tr>
<td><code>@AfterThrowing</code></td>
<td><strong>예외 발생 시</strong> 실행됨</td>
<td>❌ (예외 발생 시 타겟 메서드는 실패함)</td>
<td>✅ 예외 객체 접근 가능</td>
<td>❌</td>
</tr>
<tr>
<td><code>@Around</code></td>
<td>메서드 실행 <strong>전후 모두</strong> 제어 가능</td>
<td>❌ 직접 <code>proceed()</code>로 호출해야 실행됨</td>
<td>✅ 호출 전/후 제어 가능</td>
<td>✅ <strong>반드시 <code>return joinPoint.proceed()</code> 해야 함</strong></td>
</tr>
</tbody></table>
<ul>
<li><code>@Before</code>, <code>@After</code>, <code>@AfterReturning</code> 등은 흐름에 <strong>끼어들기만 함</strong> → <code>return</code> 불필요</li>
<li><code>@Around</code>는 메서드 실행을 <strong>직접 제어함</strong> → <code>return joinPoint.proceed()</code> 필수!</li>
</ul>
<br />




<hr />
<br />
<br />
<br />

<hr />
<br />

<h1 id="과제-해설-aop-구현과는-다른-점">과제 해설 AOP 구현과는 다른 점</h1>
<hr />
<h2 id="aop-1">AOP</h2>
<pre><code class="language-java">@Slf4j
@Aspect
@Component
@RequiredArgsConstructor
public class AdminAccessLoggingAspect {

    private final HttpServletRequest request;
    private final ObjectMapper objectMapper;

    @Around(&quot;@annotation(org.example.expert.config.aop.annotation.Admin)&quot;)
    public Object logAdminApiAccess(ProceedingJoinPoint joinPoint) throws Throwable {
        Long userId = (Long) request.getAttribute(&quot;userId&quot;);</code></pre>
<blockquote>
<p>선생님은 이런 식으로 전역변수로 HttpServletRequest를 선언하심... 쏘 이지잖아...</p>
</blockquote>
<hr />
<pre><code class="language-java"> @Around(&quot;@annotation(org.example.expert.config.aop.annotation.Admin)&quot;)
     public Object logAdminApiAccess(ProceedingJoinPoint joinPoint) throws Throwable {</code></pre>
<blockquote>
<p>AOP 대상 메서드(컨트롤러)에 붙일 어노테이션을 직접 생성하시고
매우 쉽게 annotation으로 경로를 지정함..</p>
</blockquote>
<pre><code class="language-java">package org.example.expert.config.aop.annotation;

import java.lang.annotation.*;

@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Admin {
}</code></pre>
<blockquote>
<p>이렇게 이전에 argumentResolver 해설 코드에 적힌 @Auth 어노테이션처럼 
@Admin 어노테이션을 만들어서</p>
</blockquote>
<pre><code class="language-java">
@RestController
@RequiredArgsConstructor
public class UserAdminController {

    private final UserAdminService userAdminService;

    @Admin
    @PatchMapping(&quot;/admin/users/{userId}&quot;)
    public void changeUserRole(@PathVariable long userId, @RequestBody UserRoleChangeRequest userRoleChangeRequest) {
        userAdminService.changeUserRole(userId, userRoleChangeRequest);
    }
}</code></pre>
<blockquote>
<p>이렇게 대상이 되는 메서드 위에 @Admin어노테이션을 달아줌...
쏘이지잖아...... Pointcut 경로 짜느라 시간 안써도 되잖아...</p>
</blockquote>
<br />

<hr />
<br />

<h2 id="interceptor-1">Interceptor</h2>
<pre><code class="language-java">@Slf4j
public class AdminAccessInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        UserRole userRole = UserRole.of((String) request.getAttribute(&quot;userRole&quot;));
        if (!UserRole.ADMIN.equals(userRole)) {
            response.sendError(HttpServletResponse.SC_FORBIDDEN, &quot;관리자 권한이 필요합니다.&quot;);
            return false;
        }

        log.info(&quot;Interceptor - Admin API Access: Timestamp={}, URL={}&quot;, System.currentTimeMillis(), request.getRequestURI());
        return true;
    }
}</code></pre>
<blockquote>
<p>여기서 나는 예외 경우에 return false처리를 안해줬고, 
예외가 안나고 정상 처리엔 return HandlerInterceptor.super.preHandle(request, response, handler);
를 해줬는데 이는 선생님 방법을 따르는 게 나을 듯</p>
</blockquote>
<hr />
<blockquote>
<p>AOP에선 하나의 트러블이 있었는데 바로 ObjectMapper다...아직 json에 대한 개념이 부족하다는 생각이 들었다
해결은 못했고 결국 json으로 파싱하는 데서 끙끙대다가 과제 해설을 보고 참고했다.</p>
</blockquote>
<br />

<hr />
<br />

<h2 id="다음에-실천할-것">다음에 실천할 것</h2>
<p>AOP에서 request, response 데이터를 json문자열로 파싱할 때 </p>
<p>특히
컨트롤러의 여러 파라미터들 중 RequestBody만 출력할 수 있도록 하면 어케야 될지도 고민했었다.....결국 못했지만</p>
<p>예를 들어</p>
<br />

<hr />
<br />

<pre><code class="language-java">public void changeUserRole(@PathVariable long userId, 
                           @RequestBody UserRoleChangeRequest userRoleChangeRequest)</code></pre>
<p>컨트롤러의 파라미터에 @PathVariable, @RequestBody
이렇게 두 개가 있는데 여기서 @RequestBody만 로깅하고 싶을 땐 어케야 할까??</p>
<br />

<hr />
<pre><code class="language-java">MethodSignature signature = (MethodSignature) joinPoint.getSignature();
Method method = signature.getMethod();
Annotation[][] paramAnnotations = method.getParameterAnnotations();
Object[] args = joinPoint.getArgs();

for (int i = 0; i &lt; args.length; i++) {
    for (Annotation annotation : paramAnnotations[i]) {
        if (annotation instanceof RequestBody) {
            Object requestBody = args[i];
            String json = objectMapper.writeValueAsString(requestBody);
            log.info(&quot;RequestBody: {}&quot;, json);
        }
    }
}</code></pre>
<blockquote>
<p>이런 식으로 해야한다</p>
</blockquote>
<br />

<hr />
<pre><code class="language-java">MethodSignature signature = (MethodSignature) joinPoint.getSignature();
Method method = signature.getMethod(); // 이걸로 Method 가져옴</code></pre>
<blockquote>
<p>joinPoint에서 바로 Method(컨트롤러) 정보 객체를 못 꺼내기 때문에 
꼭 <code>MethodSignature</code>로 다운 캐스팅 후, <code>Method</code> 저오 객체를 가져온다.</p>
</blockquote>
<pre><code class="language-java">Annotation[][] paramAnnotations = method.getParameterAnnotations();</code></pre>
<blockquote>
<p>파라미터 어노테이션 정보를 담은 다차원 배열</p>
</blockquote>
<p>🤔 왜 다차원 배열이냐?</p>
<pre><code class="language-java">public void updateUser(
    @PathVariable Long id,
    @RequestBody UserDto dto,
    @Valid @RequestParam String name
) {}</code></pre>
<p>이렇게 하나의 파라미터에 여러 어노테이션이 붙을 수 있음 (Valid, RequestParam)</p>
<h4 id="🧠-구조-해석">🧠 구조 해석</h4>
<table>
<thead>
<tr>
<th>파라미터 인덱스</th>
<th>파라미터 타입</th>
<th>어노테이션들</th>
</tr>
</thead>
<tbody><tr>
<td><code>0</code></td>
<td><code>Long id</code></td>
<td><code>@PathVariable</code></td>
</tr>
<tr>
<td><code>1</code></td>
<td><code>UserDto dto</code></td>
<td><code>@RequestBody</code></td>
</tr>
<tr>
<td><code>2</code></td>
<td><code>String name</code></td>
<td><code>@Valid</code>, <code>@RequestParam</code></td>
</tr>
</tbody></table>
<hr />
<h4 id="✅-요약">✅ 요약</h4>
<table>
<thead>
<tr>
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>Annotation[][]</code></td>
<td><code>[파라미터 개수][해당 파라미터에 붙은 어노테이션 수]</code> 구조</td>
</tr>
<tr>
<td>이유</td>
<td>각 파라미터에 여러 개의 어노테이션이 붙을 수 있기 때문</td>
</tr>
<tr>
<td>활용</td>
<td>AOP에서 특정 어노테이션(<code>@RequestBody</code>, <code>@RequestParam</code> 등) 필터링에 사용</td>
</tr>
</tbody></table>
<h4 id="parameter의-정보는-어케-가져올까">Parameter의 정보는 어케 가져올까?</h4>
<pre><code class="language-java">MethodSignature signature = (MethodSignature) joinPoint.getSignature();
String[] paramNames = signature.getParameterNames(); // 파라미터 이름 배열
Class&lt;?&gt;[] paramTypes = method.getParameterTypes();</code></pre>
<blockquote>
<p>이런 식으로 가져오면 됨</p>
</blockquote>
<table>
<thead>
<tr>
<th>index</th>
<th>paramNames[i]</th>
<th>paramTypes[i]</th>
<th>paramAnnotations[i]</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td><code>&quot;userId&quot;</code></td>
<td><code>Long.class</code></td>
<td><code>[@PathVariable]</code></td>
</tr>
<tr>
<td>1</td>
<td><code>&quot;userRoleChangeRequest&quot;</code></td>
<td><code>UserRoleChangeRequest.class</code></td>
<td><code>[@RequestBody]</code></td>
</tr>
</tbody></table>
<br />

<hr />
<pre><code class="language-java">Object[] args = joinPoint.getArgs();</code></pre>
<blockquote>
<p>메서드(컨트롤러)의 파라미터 정보들을 담은 배열</p>
</blockquote>
<blockquote>
<p>파라미터의 값들도 다 담겨있음, 특히 객체는 key,value 형태로 필드명, 값이 모두 적혀있음</p>
</blockquote>
<br />

<hr />
<pre><code class="language-java">for (int i = 0; i &lt; args.length; i++) {
    for (Annotation annotation : paramAnnotations[i]) {
        if (annotation instanceof RequestBody) {
            Object requestBody = args[i];
            String json = objectMapper.writeValueAsString(requestBody);
            log.info(&quot;RequestBody: {}&quot;, json);
        }
    }
}</code></pre>
<blockquote>
<p>파라미터 어노테이션들을 for문 돌면서 @RequestBody인 걸 찾아냄
해당 파라미터의 정보(객체 정보)를 json으로 파싱하고 출력!!</p>
</blockquote>