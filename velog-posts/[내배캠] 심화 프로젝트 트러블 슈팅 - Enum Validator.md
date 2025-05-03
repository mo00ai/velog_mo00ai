<p>Category Enum을 검증하기 위해 만들었다.</p>
<p>처음엔 뭘 사용해야할지 모르고</p>
<p>@JsonValue랑 @JsonCreator를 사용했는데 이는 틀렸다 왜냐?</p>
<hr />
<p>✅ @JsonValue</p>
<ul>
<li>응답(JSON 만들 때) 어떤 값을 보낼지 지정 - 응답시 직렬화
– 응답을 “예쁘게” 보내고 싶을 때
❓ 서버 → 클라이언트 응답에서 enum name이 아닌, 사람이 읽기 쉬운 값을 보내고 싶을 때
응답을 &quot;KOREAN&quot; 말고 &quot;한식&quot;으로 보내고 싶을 때</li>
</ul>
<p>사용자 친화적인 JSON 만들고 싶을 때</p>
<pre><code class="language-java">@JsonValue
private final String value;</code></pre>
<p>Category.KOREAN → &quot;한식&quot; 으로 응답 보내짐
enum → JSON</p>
<br />

<p>✅ @JsonCreator(mode = DELEGATING)</p>
<ul>
<li>요청(JSON 받을 때) 어떤 방식으로 enum 만들지 지정 - 요청시 역직렬화</li>
<li>요청을 “유연하게” 받고 싶을 때
❓ 클라이언트 → 서버 요청에서 &quot;한식&quot; 같은 문자열을 enum으로 변환하고 싶을 때
요청에서 enum name() 대신 &quot;한식&quot; 같은 값이 들어올 때</li>
</ul>
<p>백엔드에서 커스텀 매핑이 필요할 때</p>
<pre><code class="language-java">@JsonCreator(mode = DELEGATING)
public static Category from(String value) { ... }</code></pre>
<p>&quot;한식&quot; → Category.KOREAN으로 매핑됨
JSON → enum</p>
<hr />
<p>🤔 사용자가 요청을 보낼 때 한글, 영어 모두 사용 하도록 해야하나?</p>
<p>&quot;프론트에서 '한식'이든 'KOREAN'이든 다 받아주는 게 유연해서 좋은가?&quot; 
vs
&quot;하나로 딱 정해서, 예: 'KOREAN'만 받게 하는 게 맞는가?&quot;</p>
<blockquote>
<p>실무에서는 무조건 하나로 통일하는게 맞음</p>
</blockquote>
<ol>
<li>명확한 계약(API명세)가 생김</li>
<li>API 문서화가 명확해짐</li>
<li>검증/변환 로직이 단순해짐 ( 둘 다 받으면 테스트도 늘고 버그 포인트도 많아짐)</li>
</ol>
<br />

<blockquote>
<p>그래서 나는 응답 값을 enum.value로 바꿔주는 jsonValue는 사용
요청할 때 value와 name을 모두 사용하게 하는 jsonCreator는 비사용하는 걸로 결정함</p>
</blockquote>
<p>❌ @JsonCreator → 쓸 이유 없음</p>
<ul>
<li>요청값이 enum name (KOREAN)이라서 Jackson이 기본으로 Category.valueOf(&quot;KOREAN&quot;) 써서 자동 변환함</li>
<li>우리가 커스텀 매핑(예: &quot;한식&quot; → KOREAN)을 할 이유가 없음</li>
<li>즉, @JsonCreator는 &quot;한식&quot; 받을 때 필요한 거니까 지금 구조엔 필요 ❌</li>
</ul>
<p>✅ @JsonValue → 필요함</p>
<ul>
<li>응답을 &quot;KOREAN&quot; 대신 &quot;한식&quot;으로 보내고 싶으면 꼭 필요</li>
<li>프론트에 사용자 친화적인 값 보여줄 수 있음</li>
</ul>
<hr />
<h1 id="enum-validator">Enum Validator</h1>
<h3 id="✅-enum-validator-쓸-땐-dto에-string으로-받는-게-좋은-이유">✅ Enum Validator 쓸 땐 DTO에 String으로 받는 게 좋은 이유</h3>
<p>🔹 Enum으로 받으면?</p>
<ul>
<li>JSON 요청에서 enum name(&quot;KOREAN&quot;)이 잘못 들어오면
  → Jackson이 먼저 예외 터뜨림 (스프링 내부에서 자동 Jackson 실행)
  → Validator까지 도달 못 함
  → 에러 메시지 커스터마이징 불가</li>
</ul>
<p>🔹 String으로 받으면?</p>
<ul>
<li>요청은 그냥 문자열로 받아짐
  → Validator에서 직접 검증 가능
  → 커스텀 메시지, 예외 처리 자유로움
  → 이후에 수동으로 Category.valueOf() 등으로 변환하면 됨</li>
</ul>
<hr />
<h2 id="enumcategory">EnumCategory</h2>
<pre><code class="language-java">package com.example.outsourcing.domain.store.enums;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

import jakarta.validation.Constraint;
import jakarta.validation.Payload;

@Documented
@Target({ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = EnumCategoryValidator.class)
public @interface EnumCategory {

    String message() default &quot;Enum에 없는 값입니다.&quot;;

    Class&lt;?&gt;[] groups() default {};

    Class&lt;? extends Payload&gt;[] payload() default {};

    Class&lt;? extends Enum&lt;?&gt;&gt; target();

}</code></pre>
<p> 커스텀 유효성 검사 어노테이션 제작하는 클래스
 Validator인 EnumCategoryValidator랑 세트로 작동</p>
 <br />


<pre><code class="language-java">@EnumCategory(target = Category.class)
private String category;</code></pre>
<p>이렇게 DTO에 붙이면,
&quot;category&quot;: &quot;KOREAN&quot;처럼 들어온 값이 실제 Category enum에 존재하는지 검증해줌.</p>
<br />

<hr />
<pre><code class="language-java">@Documented</code></pre>
<p>이 어노테이션을 붙이면, Javadoc에 표시됨
즉, Swagger나 JavaDoc에 이 유효성 검사 정보가 노출됨</p>
<hr />
<pre><code class="language-java">@Target({ElementType.FIELD})</code></pre>
<p>이 커스텀 어노테이션은 필드에만 사용 가능하다는 의미
즉, DTO의 필드에만 붙일 수 있음 (String category; 같은 데)</p>
<hr />
<pre><code class="language-java">@Retention(RetentionPolicy.RUNTIME)</code></pre>
<p>실행 중에도 이 어노테이션 정보를 리플렉션으로 읽을 수 있게 설정
Validator가 런타임에 이 정보를 읽어야 하기 때문에 꼭 필요함</p>
<hr />
<pre><code class="language-java">@Constraint(validatedBy = EnumCategoryValidator.class)</code></pre>
<p>이 어노테이션은 유효성 검사 기능을 가지며,
실제 검증 로직은 EnumCategoryValidator 클래스에 위임함</p>
<hr />
<pre><code class="language-java">public @interface EnumCategory {</code></pre>
<p>즉, @EnumCategory(...)라고 사용할 수 있게 해주는 사용자 정의 어노테이션</p>
<hr />
<pre><code class="language-java">String message() default &quot;Enum에 없는 값입니다.&quot;;</code></pre>
<p>유효성 검사 실패 시 나타날 기본 에러 메시지
❗️예: &quot;category&quot;: &quot;INVALID&quot; → 400 에러 + 이 메시지 노출됨</p>
<hr />
<pre><code class="language-java">Class&lt;?&gt;[] groups() default {};</code></pre>
<p>Bean Validation에서 사용하는 그룹 기능 (대부분 기본값으로 둠)</p>
<hr />
<pre><code class="language-java">Class&lt;? extends Payload&gt;[] payload() default {};</code></pre>
<p>역시 Bean Validation용, 예외 응답 외 메타데이터 처리용 (거의 안 씀)</p>
<hr />
<pre><code class="language-java">Class&lt;? extends Enum&lt;?&gt;&gt; target();</code></pre>
<p>이게 핵심!
검사할 대상 enum 클래스를 지정함</p>
<p>❗️사용 예:</p>
<pre><code class="language-java">@EnumCategory(target = Category.class)</code></pre>
<p>이 값을 validator 쪽에서 읽어서:</p>
<pre><code class="language-java">Object[] enumValues = this.annotation.target().getEnumConstants();</code></pre>
<p>이렇게 enum 목록을 가져올 수 있음</p>
<hr />
<h2 id="enumcategoryvalidator">EnumCategoryValidator</h2>
<ul>
<li>DTO에서 &quot;category&quot;: &quot;KOREAN&quot; 같은 요청이 들어올 때,</li>
<li>이 &quot;KOREAN&quot;이 Category enum에 실제로 있는지 확인해주는 검증기.</li>
</ul>
<br />

<pre><code class="language-java">public class EnumCategoryValidator implements ConstraintValidator&lt;EnumCategory, String&gt;</code></pre>
<ul>
<li>@EnumCategory 라는 커스텀 어노테이션을 처리하는 validator임</li>
<li>검사 대상은 String 타입 → DTO에서 category를 String으로 받는 경우에 작동</li>
</ul>
<hr />
<pre><code class="language-java">private EnumCategory annotation;</code></pre>
<p>어노테이션에 설정된 target 정보를 담기 위한 필드</p>
<hr />
<pre><code class="language-java">public void initialize(EnumCategory constraintAnnotation) {
    this.annotation = constraintAnnotation;
}</code></pre>
<p>@EnumCategory(target = Category.class) 이 정보를 여기서 저장해둠
어노테이션에 작성된 설정값(target = Category.class)을 validator 내부에서 쓸 수 있게 저장해두는 메서드</p>
<ul>
<li>유효성 검사가 시작되기 전에,</li>
<li>스프링이 @EnumCategory 어노테이션 안의 속성들을 넘겨줌</li>
<li>그걸 this.annotation에 저장해두는 거</li>
</ul>
<p>✅ 꼭 필요한 이유?</p>
<ul>
<li>isValid()는 인자로 value랑 context만 받음</li>
<li>근데 우리가 검사하려는 enum 클래스 정보는 어노테이션에 있으니까,</li>
<li>그걸 initialize()에서 미리 저장해둬야 나중에 쓸 수 있어</li>
</ul>
<blockquote>
<p>🔧 initialize()는 어노테이션의 설정값을 validator가 사용할 수 있게 준비하는 메서드다.
실행은 자동으로 호출되니까 걍 아묻따 &quot;시작 준비&quot;라고 보면 됨.</p>
</blockquote>
<hr />
<pre><code class="language-java">public boolean isValid(String value, ConstraintValidatorContext context) {</code></pre>
<p>실제 유효성 검사 메서드</p>
<hr />
<p>🤔매개변수 파라미터 2개는 뭘까?</p>
<p>**String value++
👉 검사 대상 값 (사용자가 dto에 입력한 값)
즉, DTO에서 해당 필드에 실제 들어온 요청 값이 여기에 들어감</p>
<pre><code class="language-java">{
  &quot;category&quot;: &quot;KOREAN&quot;
}

@EnumCategory(target = Category.class)
private String category;</code></pre>
<p>이러면 → &quot;KOREAN&quot; 이 value에 들어와서 유효한 enum 값인지 검사하는 거</p>
<br />

<p><strong>ConstraintValidatorContext context</strong></p>
<p>👉 유효성 검사 도중에 오류 메시지 등을 커스터마이징할 수 있는 도구
기본적으로는 잘 안 건드리고 그냥 넘어가도 됨
하지만 커스텀 메시지 만들거나, 다국어 처리할 때 필요함</p>
<pre><code class="language-java">context.disableDefaultConstraintViolation();
context.buildConstraintViolationWithTemplate(&quot;카테고리 값이 유효하지 않음&quot;)
       .addConstraintViolation();</code></pre>
<p>이렇게 하면 기본 메시지 무시하고, 새 메시지 던질 수 있음</p>
<hr />
<pre><code class="language-java">if (value == null || value.isBlank()) {
    return true;
}</code></pre>
<p>빈 값(null 또는 &quot;&quot;)은 통과시킴 → 비워도 허용하려면 이렇게
-&gt; 후에 필드에 @Notblank validator로 잡아줌</p>
<hr />
<pre><code class="language-java">Object[] enumValues = this.annotation.target().getEnumConstants();</code></pre>
<p>전달받은 enum 클래스에서 모든 enum 값 가져옴
(예: Category.values()랑 같음)</p>
<hr />
<pre><code class="language-java">for (Object enumValue : enumValues) {
    if (value.equals(enumValue.toString())) {
        return true;
    }
}</code></pre>
<p>value가 enum의 name()과 일치하면 → 유효함
(toString()은 기본적으로 name()과 동일)
-&gt; 데이터가 dto 필드에 잘 담김</p>
<hr />
<pre><code class="language-java">return false;</code></pre>
<p>위에서 하나도 안 맞으면 유효하지 않음 → 검증 실패
-&gt; 예외 터짐</p>