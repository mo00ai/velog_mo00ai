<p>기본적으로 스프링이 다 예외잡아줌! But 문제 </p>
<ul>
<li>스프링 기본 에러처리는 식별이 힘듦</li>
<li>Interval 뭐시기 에러가 뜨는게 이게 아주 긺. 서버에서 확인하기 예외 확인이 어려움</li>
<li>클라이언트 쪽에서도 식별이 어려움 </li>
<li><blockquote>
<p>이 문제를 해결하기 위해 나온 방법</p>
</blockquote>
</li>
</ul>
<hr />
<p>예외처리 클래스를 직접 만들어서 거기서 해결하고 메세지를 지정하자~
-&gt; 근데 이것도 스프링부트가 어노테이션으로 다 제공한단다^^</p>
<blockquote>
<p>@ExceptionHandler, @ControllerAdvice</p>
</blockquote>
<hr />
<h2 id="예외-처리-핸들러클래스에-적용">예외 처리 핸들러(클래스에 적용)</h2>
<pre><code class="language-java">// 예외 처리 핸들러
@ControllerAdvice
class MyExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity&lt;String&gt; handleGeneralException(Exception ex) {
        return new ResponseEntity&lt;&gt;(&quot;An error occurred: &quot; + ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }

    @ExceptionHandler(CustomException.class)
    public ResponseEntity&lt;String&gt; handleCustomException(CustomException ex) {
        return new ResponseEntity&lt;&gt;(ex.getMessage(), HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(ConstraintViolationException.class)
    public ResponseEntity&lt;String&gt; handleConstraintViolationException(ConstraintViolationException ex) {
        return new ResponseEntity&lt;&gt;(&quot;@Validated failed: &quot; + ex.getMessage(), HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity&lt;String&gt; handleValidationException(MethodArgumentNotValidException ex) {
        return new ResponseEntity&lt;&gt;(&quot;@Valid failed: &quot; + ex.getBindingResult().getFieldError().getDefaultMessage(), HttpStatus.BAD_REQUEST);
    }

}</code></pre>
<p><code>@ControllerAdvice</code></p>
<ul>
<li>클래스에 적용</li>
<li>이 클래스는 이제 예외처리 핸들러다 명시</li>
</ul>
<p><code>@ExceptionHandler</code></p>
<ul>
<li>직접 에러 메시지와 http 상태 코드를 반환하는 메서드에 적용</li>
<li>실제 구현</li>
</ul>
<p><code>Exception.class</code></p>
<ul>
<li>어떤 에러인지</li>
<li>뒤에 class는 걍 Exception이라고 적혀있으면 스프링이 인식 못해서 이거 예외 클래스 Exception이야~하고 알려주려고 닮</li>
</ul>
<p><code>ResponseEntity&lt;String&gt;</code></p>
<ul>
<li>ResponseEntity는 http상태코드와 여러가지(까묵)를 같이 반환할 수 있음</li>
<li>상태코드 반환? 어떤 예외가 처리됐는지 알려주기에 적합하잖아<del>~</del> </li>
<li><blockquote>
<p>그래서 ResponseEntity 사용^^</p>
</blockquote>
</li>
</ul>
<p><code>ex.getMessage</code></p>
<ul>
<li>예외 던진 쪽(throw)에서 보낸 에러메세지 받아서 출력</li>
</ul>
<blockquote>
<p>그리고 throw하지 않아도 발생한 예외(에러)가 예외처리 핸들러 종류와 일치하면
예외 처리가 잡아서 알아서 처리해줌 굳굳~</p>
</blockquote>
<blockquote>
<p>그래서 우리가 실제 스프링부트 컨트롤러 만들 때도 </p>
</blockquote>
<hr />
<h2 id="customexception">CustomException</h2>
<ul>
<li>개발하다가 어? 이거 예외핸들러로 빼야겠다 싶은 것들이 있을거임</li>
<li>RuntimeException이나 Exception 상속받지 않는 새로운 예외처리들 내가 만든 것들</li>
<li>ex) 회원가입 인원 10명 초과되면 예외처리 등</li>
</ul>
<h3 id="customexception-클래스-생성">CustomException 클래스 생성</h3>
<pre><code class="language-java">public class CustomException extends RuntimeException {
    public CustomException(String message) {
        super(message);
    }
}</code></pre>
<p><code>extends RuntimeException</code></p>
<ul>
<li>Exception을 상속받아야 message를 직접 보낼 수 있고 예외로써 작용함</li>
<li>암튼 이렇게 클래스 만드삼!</li>
</ul>
<blockquote>
<p>근데?? 이름을 명시해야함. 
ex) 회원가입 인원 10명 초과되면 예외처리
-&gt; TooManyMemberException 이런 식으로!</p>
</blockquote>
<blockquote>
<p>그리고 exception 패키지에 정리 ㅇㅇ
예외는 만들어야겠다 생각하면 걍 아묻따 만드셈 문제 없음</p>
</blockquote>
<h3 id="customexception-예외-발생-예시">CustomException 예외 발생 예시</h3>
<pre><code class="language-java">    @GetMapping(&quot;/customException&quot;)
    public String customException() {
        throw new CustomException(&quot;custom exception occur !&quot;);
    }</code></pre>
<blockquote>
<p>컨트롤러에서 발생한 예시 사례
-&gt; throw해서 예외 던지고 생성자 란에 message 적으면 됨~</p>
</blockquote>
<h3 id="customeexcpeiton-exceptionhandler-예시">CustomeExcpeiton @ExceptionHandler 예시</h3>
<pre><code class="language-java">    @ExceptionHandler(CustomException.class)
    public ResponseEntity&lt;String&gt; handleCustomException(CustomException ex) {
        return new ResponseEntity&lt;&gt;(ex.getMessage(), HttpStatus.BAD_REQUEST);
    }</code></pre>
<blockquote>
<p>위에서 충분히 설명함</p>
</blockquote>
<br />
<br />

<hr />
<br />

<hr />
<h2 id="valid">Valid</h2>
<ul>
<li>데이터를 검증하기 위한 어노테이션</li>
<li>주로 Controller의 dto 앞에 적용시키고 dto내엔 하위 어노테이션(Min) 등 사용</li>
</ul>
<pre><code class="language-java">@RestController
public class UserController {
  @PostMapping(&quot;/user&quot;)
  public ResponseEntity&lt;String&gt; createUser(@RequestBody @Valid UserDto userDto){
        return ResponseEntity.ok(&quot;User is valid!&quot;);
  }
}

@Getter
public class UserDto {
    private Long id;
    @Min(20)
    private Long age;

    @Override
    public String toString() {
        return &quot;UserDto{id=&quot; + id + &quot;, age=&quot; + age + '}';
    }
}</code></pre>
<ul>
<li>컨트롤러 RequestBody에 <code>@Valid</code> 적용</li>
<li>dto 필드에 하위 어노테이션 적용</li>
</ul>
<blockquote>
<p>왜 사용 할까?</p>
</blockquote>
<ul>
<li>식별 쉬움! 코드 간단해짐</li>
<li>우리 프로젝트에 깊이 들어오지 않고 딱 처음 dto 만나자마자 검사 당해버려서</li>
<li>프로젝트 내 쓰레드 풀을 절약할 수 있음!</li>
</ul>
<blockquote>
<p>만약 Valid를 안썼다면 거의 Service, Repository까지 쓸데없는 값 들고가서 유효성 검사하고
튕겨나갈텐데 거기에 사용된 쓰레드풀이 아깝단 말임</p>
</blockquote>
<br />
<br />


<h3 id="유효성-검사-어노테이션-종류">@유효성 검사 어노테이션 종류</h3>
<table>
<thead>
<tr>
<th>어노테이션</th>
<th>종류</th>
<th>설명</th>
<th>예시</th>
</tr>
</thead>
<tbody><tr>
<td><code>@NotBlank</code></td>
<td>String</td>
<td>null이 아니며 공백이 아닌 문자를 하나 이상 포함한다.</td>
<td></td>
</tr>
<tr>
<td><code>@NotEmpty</code></td>
<td>String</td>
<td>null 이거나 빈 문자열이 아니어야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@NotNull</code></td>
<td>모두</td>
<td>null이 아닌 값이다.</td>
<td></td>
</tr>
<tr>
<td><code>@Null</code></td>
<td>모두</td>
<td>null값이다.</td>
<td></td>
</tr>
<tr>
<td><code>@Max</code></td>
<td>int</td>
<td>해당값보다 작거나 같아야 한다.</td>
<td><code>@Max(value = 100)</code></td>
</tr>
<tr>
<td><code>@Min</code></td>
<td>int</td>
<td>해당값보다 크거나 같아야 한다.</td>
<td><code>@Min(value = 1)</code></td>
</tr>
<tr>
<td><code>@DecimalMax</code></td>
<td>String</td>
<td>해당값보다 작거나 같아야 한다.</td>
<td><code>@DecimalMax(&quot;100&quot;)</code></td>
</tr>
<tr>
<td><code>@DecimalMin</code></td>
<td>String</td>
<td>해당값보다 크거나 같아야 한다.</td>
<td><code>@DecimalMin(&quot;1&quot;)</code></td>
</tr>
<tr>
<td><code>@Positive</code></td>
<td>int</td>
<td>양수인 값이다.</td>
<td></td>
</tr>
<tr>
<td><code>@PositiveOrZero</code></td>
<td>int</td>
<td>0이거나 양수인 값이다.</td>
<td></td>
</tr>
<tr>
<td><code>@Negative</code></td>
<td>int</td>
<td>음수인 값이다.</td>
<td></td>
</tr>
<tr>
<td><code>@NegativeOrZero</code></td>
<td>int</td>
<td>0이거나 음수인 값이다.</td>
<td></td>
</tr>
<tr>
<td><code>@Email</code></td>
<td>String</td>
<td>올바른 형식의 이메일 주소여야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@Future</code></td>
<td>Date</td>
<td>현재보다 미래의 날짜, 시간이어야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@FutureOrPresent</code></td>
<td>Date</td>
<td>현재거나 미래의 날짜, 시간이어야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@Past</code></td>
<td>Date</td>
<td>현재보다 과거의 날짜, 시간이어야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@PastOrPresent</code></td>
<td>Date</td>
<td>현재거나 과거의 날짜, 시간이어야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@AssertTrue</code></td>
<td>boolean</td>
<td>값이 항상 <code>true</code>여야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@AssertFalse</code></td>
<td>boolean</td>
<td>값이 항상 <code>false</code>여야 한다.</td>
<td></td>
</tr>
<tr>
<td><code>@Size</code></td>
<td>int</td>
<td>값이 min과 max 사이에 있어야 한다.</td>
<td><code>@Size(min = 1, max = 10)</code></td>
</tr>
</tbody></table>
<blockquote>
<p>출처 : <a href="https://suyeonme.tistory.com/90">https://suyeonme.tistory.com/90</a></p>
</blockquote>
<blockquote>
<p>@NOTNULL(message =&quot;&quot;) 로 에러메세지 보낼 수 있음 
@Size(max=1, message = &quot;&quot;) </p>
</blockquote>
<br />

<hr />
<h2 id="validated">Validated</h2>
<pre><code class="language-java">@Validated
@RestController
public class ValidatedController {
    @PostMapping(&quot;/test-validated/number&quot;)
    public String testValid(@Min(10) Integer number, @RequestBody @Valid UserDto userDto) {
        return number + &quot; : &quot; + userDto.toString();
    }
}

@Getter
public class UserDto {
    private Long id;
    @Min(20)
    private Long age;

    @Override
    public String toString() {
        return &quot;UserDto{id=&quot; + id + &quot;, age=&quot; + age + '}';
    }
}</code></pre>
<blockquote>
<p>@Requestbody가 아닌 requestParam, @PathVariable같은 거에 쓸 수 있음</p>
</blockquote>
<p>단!!</p>
<ul>
<li>클래스에 @Validated 달고</li>
<li>requestParam 이나 PathVariable에 직접 유효성 검사 어노테이션 달면 됨</li>
</ul>
<hr />
<h2 id="valid-validated-예외-처리-핸들러-양식">Valid, Validated 예외 처리 핸들러 양식</h2>
<pre><code class="language-java">
    @ExceptionHandler(ConstraintViolationException.class)
    public ResponseEntity&lt;String&gt; handleConstraintViolationException(ConstraintViolationException ex) {
        return new ResponseEntity&lt;&gt;(&quot;@Validated failed: &quot; + ex.getMessage(), HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity&lt;String&gt; handleValidationException(MethodArgumentNotValidException ex) {
        return new ResponseEntity&lt;&gt;(&quot;@Valid failed: &quot; + ex.getBindingResult().getFieldError().getDefaultMessage(), HttpStatus.BAD_REQUEST);
    }</code></pre>
<p><code>ConstraintViolationException</code></p>
<ul>
<li><code>@Validated</code> 전용 예외</li>
</ul>
<p><code>MethodArgumentNotValidException</code></p>
<ul>
<li><code>@Valid</code> 전용 예외</li>
<li>여러 필드 중 가장 첫 번째 오류 메시지만 가져옴</li>
<li>에러 메시지가 너무 많거나 복잡하면 사용자에게 부담됨</li>
<li>에러 메시지가 이상하거나 길게 떠서 식별하기 어려우니까 추가적으로 작업함</li>
</ul>