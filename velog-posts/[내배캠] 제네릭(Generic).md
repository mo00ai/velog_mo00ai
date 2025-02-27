<h3 id="제네릭">제네릭</h3>
<ul>
<li>제네릭은 클래스, 메서드 등에 사용되는 <code>&lt;T&gt;**타입 매개변수**</code>를 의미합니다.</li>
<li>타입을 미리 지정하지 않고 사용 시점에 유연하게 결정할 수 있는 문법입니다.</li>
<li>제네릭을 활용하면 <code>코드 재사용성</code>과 <code>타입 안정성</code>을 보장받을 수 있습니다.</li>
<li>하지만 과도하게 사용하면 오히려 복잡해질 수 있으므로 주의해야 합니다.</li>
</ul>
<br />

<p><strong><em>얻는 효과</em></strong></p>
<p><code>코드 재사용성</code></p>
<ul>
<li>다양한 타입에서 동일한 코드로 재사용이 가능합니다.</li>
</ul>
<p><code>타입 안정성</code></p>
<ul>
<li>잘못된 타입 사용을 컴파일 시점에 방지합니다.</li>
</ul>
<br />
<br />

<hr />
<br />

<h4 id="제네릭이-없는-경우">제네릭이 없는 경우</h4>
<p><strong>1. 제네릭이 없는 Box 클래스 - 재사용 불가</strong></p>
<ul>
<li><p>이 클래스는 특정 타입(<code>Integer</code>)으로 고정 되어 있어 재사용이 어렵습니다.</p>
<ul>
<li><code>String</code> 타입 전용 박스가 필요하다면 다시 만들어야 합니다.</li>
</ul>
</li>
<li><p>다시 사용하려면 다른 클래스를 만들어야 합니다.(낮은 유연성)</p>
<pre><code class="language-java">public class Box {
  private Integer item; // ⚠️ Integer 타입으로 고정

  public Box(Integer item) { // ⚠️ Integer 타입으로 고정
      this.item = item;
  }

  public Integer getItem() {
      return this.item;
  }
}

</code></pre>
</li>
</ul>
<p>public class Main {
    public static void main(String[] args) {
        // ✅ Integer 타입 박스
        Box box1 = new Box(100);</p>
<pre><code>    // ❌ String 타입을 저장하려면 새로운 클래스를 만들어야 함
    Box box2 = new Box(&quot;ABC&quot;); 

}</code></pre><p>}</p>
<pre><code>
&lt;br&gt;

***2. 제네릭이 없는 Box 클래스 - 낮은 타입 안정성 ***
- 다형성을 활용하면 다양한 타입을 저장 가능하지만 실행 중 오류가 발생할 가능성이 높습니다.
- 사용 시 형 변환이 필요하고 실수로 잘못된 타입을 사용하면 런타임 오류가 발생합니다.
     →  잘못된 다운케스팅 활용 시: `ClassCastException`

```java
public class ObjectBox {
    private Object item; // ⚠️ 다형성: 모든 타입 저장 가능 (하지만 안전하지 않음)

    public ObjectBox(Object item) {
        this.item = item;
    }

    public Object getItem() {
        return this.item;
    }
}


public class Main {
    public static void main(String[] args) {
        // ✅ ObjectBox 사용
        ObjectBox objBox = new ObjectBox(&quot;Hello&quot;);
        String str = (String) objBox.getItem(); // 형변환 필요
        System.out.println(&quot;objBox 내용: &quot; + str); // Hello

        // ⚠️ 실행 중 오류 발생 (잘못된 다운 캐스팅: ClassCastException)
        objBox = new ObjectBox(100); // 정수 저장
        String error = (String) objBox.getItem(); // ❌ 오류: Integer -&gt; String 
        System.out.println(&quot;잘못된 변환: &quot; + error);
    }
}</code></pre><p>다형성이라 한 이유</p>
<ul>
<li><code>Object</code> 클래스 내에 <code>레퍼 클래스</code>들(Integer,String...etc) 등이 존재</li>
</ul>
<br />
<br />

<hr />
<br />

<h4 id="제네릭-활용재사용성--타입안정성">제네릭 활용(재사용성 + 타입안정성)</h4>
<p>제네릭 <code>&lt;T&gt;</code>(타입매개변수)</p>
<ul>
<li><code>&lt;T&gt;</code>(타입매개변수) 는 제네릭에서 <strong>타입을 의미하는 자리</strong>입니다.</li>
<li>실제 데이터 타입으로 대체되어 활용 됩니다.</li>
<li>타입 : 자료형</li>
</ul>
<p>클래스에 제네릭을 활용해 재사용성과 타입안정성을 보장받을 수 있습니다.</p>
<ul>
<li><code>제네릭 클래스</code>는 클래스 선언부에 <code>&lt;T&gt;</code> 가 선언된 클래스입니다.</li>
<li><code>제네릭 클래스</code>는 클래스 선언시 타입 매개변수를 사용해 다양한  데이터 타입을 안전하게 처리할 수 있는 구조입니다.</li>
<li><code>GenericBox&lt;T&gt;</code> 를 활용해서 <code>String</code>, <code>Integer</code>, <code>Double</code> 등 다양한 타입 저장 가능 합니다.</li>
</ul>
<pre><code class="language-java">public class GenericBox&lt;T&gt; { // ✅ 제네릭 클래스
    private T item;

    public GenericBox(T item) {
        this.item = item;
    }

    public T getItem() {
        return this.item;
    }
}</code></pre>
<br />

<p><strong>`타입소거(</strong>Erasure<strong>)`</strong> </p>
<ul>
<li>타입 소거는 컴파일 시점에 제네릭 타입 정보를 제거하는 과정입니다.<ul>
<li><code>&lt;T&gt;</code> 타입 매개변수 부분은 <code>Object</code> 로 대체됩니다.</li>
<li>필요한 경우 컴파일러가 <strong><em>자동으로 강제 다운 캐스팅(cast) 코드를 삽입하여 타입 안전성을 보장</em></strong>합니다.</li>
</ul>
</li>
</ul>
<pre><code class="language-java">```java
public class GenericBox&lt;Object&gt; { // ✅ 제네릭 클래스
    private Object item;

    public GenericBox(Object item) {
        this.item = item;
    }

    public Ojbect getItem() {
        return this.item;
    }
}</code></pre>
<br />

<p>main에서 제네릭 활용</p>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {

        // 1. ✅ 재사용 가능(컴파일시 타입소거: T -&gt; Object)
        GenericBox&lt;String&gt; strGBox = new GenericBox&lt;&gt;(&quot;ABC&quot;);
        GenericBox&lt;Integer&gt; intGBox = new GenericBox&lt;&gt;(100);
        GenericBox&lt;Double&gt; doubleGBox = new GenericBox&lt;&gt;(0.1);

        // 2. ✅ 타입 안정성 보장(컴파일시 타입소거: 자동으로 다운캐스팅)
        String strGBoxItem = strGBox.getItem();
        Integer intGBoxItem = intGBox.getItem();
        Double doubleGBoxItem = doubleGBox.getItem();
        System.out.println(&quot;strGBoxItem = &quot; + strGBoxItem);
        System.out.println(&quot;intGBoxItem = &quot; + intGBoxItem);
        System.out.println(&quot;doubleGBoxItem = &quot; + doubleGBoxItem);
    }
}</code></pre>
<p><code>컴파일시 타입소거: 자동으로 다운캐스팅</code></p>
<pre><code class="language-java">       String strGBoxItem = (String) strGBox.getItem();
       Integer intGBoxItem = (Integer) intGBox.getItem();
       Double doubleGBoxItem = (Double) doubleGBox.getItem();</code></pre>
<ul>
<li>이 과정을 자동으로 해준다는 거 </li>
<li>왜? 타입 소거할 때 자동으로 T가 Object로 변환했으니까 다운캐스팅 해드려야지</li>
</ul>
<br />
<br />

<hr />
<br />

<h4 id="제네릭-메서드generic-method">제네릭 메서드(Generic Method)</h4>
<p><strong><code>제네릭 메서드</code> 는 메서드 내부에서 사용할 타입을 유연하게 지정하는 기능입니다.</strong></p>
<ul>
<li>제네릭 메서드는 메서드 선언부에 <code>&lt;T&gt;</code> 가 선언된 메서드입니다.</li>
<li>제네릭 메서드는 클래스 제네릭 타입과 별개로 <strong><em>독립적인 타입 매개변수</em></strong>를 가집니다.
  → 타입 소거 과정을 생각해 보세요.</li>
</ul>
<pre><code class="language-java">public class GenericBox&lt;T&gt; {

    // 속성
    private T item;

    // 생성자
    public GenericBox(T item) {
        this.item = item;
    }

    // 기능
    public T getItem() {
        return this.item;
    }

        // ⚠️ 일반 메서드 T item 는 클래스의 &lt;T&gt; 를 따라갑니다.
    public void printItem(T item) {
        System.out.println(item);
    }

    // ✅ 제네릭 메서드 &lt;S&gt; 는 &lt;T&gt; 와 별개로 독립적이다.
    public &lt;S&gt; void printBoxItem(S item) { 
        System.out.println(item);
    }
}


public class Main {

    public static void main(String[] args) {
        GenericBox&lt;String&gt; strGBox = new GenericBox&lt;&gt;(&quot;ABC&quot;);
        GenericBox&lt;Integer&gt; intGBox = new GenericBox&lt;&gt;(100);

        // ⚠️ 일반메서드: 클래스 타입 매개변수를 따라갑니다.
        // String 데이터 타입 기반으로 타입소거가 발생.
        // String 타입의 다운캐스팅 코드 삽입!
        strGBox.printItem(&quot;ABC&quot;); // ✅ String 만 사용가능
        strGBox.printItem(100);   // ❌ 에러 발생 

        // ✅ 제네릭 메서드: 독립적인 타입 매개변수를 가집니다.
        // String 타입 정보가 제네릭 메서드에 아무런 영향을 주지 못함.
        // 다운캐스팅 코드 삽입되지 않음.
        strGBox.printBoxItem(&quot;ABC&quot;); //✅ 모든 데이터 타입 활용 가능
        strGBox.printBoxItem(100);   //✅ 모든 데이터 타입 활용 가능
        strGBox.printBoxItem(0.1);   //✅ 모든 데이터 타입 활용 가능
    }
}</code></pre>
<br />
<br />

<hr />
<br />

<h4 id="제네릭-메서드를-사용하는-구체적인-상황-예시">제네릭 메서드를 사용하는 구체적인 상황 예시</h4>
<br />

<p><strong><em>1. 코드의 중복을 줄이고 싶을 때</em></strong></p>
<ul>
<li>여러 데이터 타입에 대해 같은 로직을 수행하는 메서드를 각각의 데이터 타입별로 여러 번 작성하면 코드가 중복되겠지? 제네릭을 사용하면 하나의 메서드로 다양한 데이터 타입을 처리할 수 있어 중복을 피할 수 있어.</li>
</ul>
<p><strong><em>예시 상황</em></strong></p>
<ul>
<li>숫자, 문자 등 다양한 데이터 타입을 배열에서 찾고 싶을 때:</li>
</ul>
<pre><code class="language-java">public class Main {
    // 제네릭 메서드
    public static &lt;T&gt; boolean contains(T[] array, T element) {
        for (T item : array) {
            if (item.equals(element)) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        Integer[] numbers = {1, 2, 3};
        String[] words = {&quot;Hello&quot;, &quot;Java&quot;};

        System.out.println(contains(numbers, 2));    // true
        System.out.println(contains(words, &quot;Java&quot;)); // true
    }
}</code></pre>
<p>위의 메서드로 정수, 문자, 객체 등 모든 타입의 배열에 대응 가능해져.</p>
<br />
<br />

<p><strong><em>2. 타입 안정성(Type Safety)을 높이고 싶을 때</em></strong></p>
<ul>
<li>Object 타입으로 모든 데이터를 받으면 컴파일 단계에서 타입 체크가 어렵고 런타임에서 오류가 발생하기 쉬워. 제네릭을 사용하면 컴파일 타임에 미리 타입 오류를 확인할 수 있어서 안전해져.</li>
</ul>
<p><strong><em>예시 상황</em></strong></p>
<ul>
<li>타입 체크 없이 Object로 데이터를 받을 때:<pre><code class="language-java">import java.util.*;
</code></pre>
</li>
</ul>
<p>public class Main {
    // 제네릭을 사용하지 않고 Object를 반환하는 메서드
    public static Object getFirstElement(List list) {
        return list.get(0);
    }</p>
<pre><code>public static void main(String[] args) {
    List list = new ArrayList();

    list.add(&quot;Hello&quot;);    // String 타입
    list.add(123);        // Integer 타입

    // 첫 번째 요소 가져와서 String으로 캐스팅 (정상 작동)
    String firstElement = (String) getFirstElement(list);
    System.out.println(&quot;첫 번째 요소: &quot; + firstElement);

    // 두 번째 요소 가져와서 String으로 캐스팅 시도 (런타임 에러 발생!)
    String secondElement = (String) list.get(1);
    System.out.println(&quot;두 번째 요소: &quot; + secondElement);
}</code></pre><p>}</p>
<pre><code>
&lt;br&gt;

- 제네릭을 활용해 타입 체크를 강화했을 때:
```java
import java.util.*;

public class Main {
    // 제네릭을 활용한 메서드
    public static &lt;T&gt; T getFirstElement(List&lt;T&gt; list) {
        return list.get(0);
    }

    public static void main(String[] args) {
        List&lt;String&gt; list = new ArrayList&lt;&gt;();

        list.add(&quot;Hello&quot;);  // 정상
        // list.add(123);   // 컴파일 에러! Integer 타입은 추가 불가능

        String firstElement = getFirstElement(list);
        System.out.println(&quot;첫 번째 요소: &quot; + firstElement);
    }</code></pre><blockquote>
<p>타입 체크 없이 Object로 받는다면 -&gt; 들어가있는게 String인지 int인지 나중에 호출할 때 뭐가 뭔지 모르겠다는 거임 int 들어가있는데 String으로 호출할 수도 있음</p>
</blockquote>
<blockquote>
<p>but 제네릭을 쓰면 어떤 타입을 썼는지 눈에 확연히 볼 수 있으니 </p>
</blockquote>
<br />
<br />

<p><strong><em>3. 라이브러리나 프레임워크를 만들 때</em></strong></p>
<ul>
<li>특정 데이터 타입에 종속되지 않고, 다양한 사용자가 여러 타입을 이용할 수 있도록 API를 제공하려면 제네릭 메서드를 활용해 범용성을 높일 수 있어.</li>
</ul>
<p><strong><em>예시 상황:</em></strong></p>
<ul>
<li>자바의 컬렉션 프레임워크(List&lt;제네릭&gt;, Map&lt;K,V&gt; 등)는 모두 제네릭으로 구현되어 있어서 사용자가 원하는 데이터 타입으로 활용 가능해.</li>
</ul>
<br />

<p><strong><em>4. 다양한 타입을 유연하게 처리하고 싶을 때</em></strong></p>
<ul>
<li>특정 타입을 미리 알 수 없는 상황에서 유연하게 타입을 받아 처리해야 할 때 제네릭 메서드를 쓰면 좋지.</li>
</ul>
<p><strong><em>예시 상황</em></strong></p>
<ul>
<li>JSON이나 데이터 직렬화 과정에서, 다양한 형태의 데이터를 범용적으로 처리할 때:</li>
</ul>
<p><strong><em>💡 구체적인 상황 설명</em></strong>
제네릭 메서드가 특히 유용한 순간은 코드를 작성할 당시에는 어떤 타입을 처리할지 정확히 모를 때야.
예를 들어, 데이터를 외부에서 받아와서 처리할 때를 생각해 봐.
웹 서버로 들어오는 JSON 데이터나 파일에서 읽어오는 데이터는 매번 형태가 다를 수 있지.
이럴 때 타입을 미리 특정할 수 없기 때문에 유연하게 처리할 방법이 필요한 거야.</p>
<blockquote>
<p>이제부터 JSON 때문에 제네릭을 사용하는 예시를 들건데 진짜 대박 어려움 
하지만 플젝 할 때 꼭 쓰일테니까 완전 정리하겠음</p>
</blockquote>
<br />
<br />
<br />

<hr />
<br />
<br />

<h3 id="제네릭을-사용해서-json-데이터를-다양한-객체로-변환하자">제네릭을 사용해서 JSON 데이터를 다양한 객체로 변환하자</h3>
<br />

<p>제네릭 메서드가 특히 유용한 순간은 코드를 작성할 당시에는 어떤 타입을 처리할지 정확히 모를 때야.
예를 들어, 데이터를 외부에서 받아와서 처리할 때를 생각해 봐.
<strong><em>웹 서버로 들어오는 JSON 데이터</em></strong>나 <strong><em>파일에서 읽어오는 데이터</em></strong>는 매번 형태가 다를 수 있지.
이럴 때 타입을 미리 특정할 수 없기 때문에 <strong><em>유연하게 처리</em></strong>할 방법이 필요한 거야.</p>
<br />
<br />

<h4 id="실제-상황-예시">실제 상황 예시</h4>
<br />

<p>json 데이터 예시</p>
<pre><code class="language-java">// 사람 데이터 (Person 객체로 변환)
{
  &quot;name&quot;: &quot;홍길동&quot;,
  &quot;age&quot;: 27
}

// 상품 데이터 (Product 객체로 변환)
{
  &quot;productName&quot;: &quot;노트북&quot;,
  &quot;price&quot;: 1500000
}</code></pre>
<p>위처럼 서로 다른 구조의 데이터를 처리하려면, 아래와 같은 제네릭 메서드를 사용해서 서로 다른 객체로 처리함</p>
<br />

<h4 id="제네릭을-활용한-json-파싱-메서드">제네릭을 활용한 JSON 파싱 메서드</h4>
<pre><code class="language-java">import com.google.gson.Gson;

public class JsonUtil {

    // JSON 문자열을 원하는 객체 타입으로 변환해주는 제네릭 메서드
    public static &lt;T&gt; T parseJson(String json, Class&lt;T&gt; clazz) {
        Gson gson = new Gson();
        return gson.fromJson(json, clazz);
    }

    public static void main(String[] args) {
        String personJson = &quot;{\&quot;name\&quot;: \&quot;홍길동\&quot;, \&quot;age\&quot;: 27}&quot;;
        String productJson = &quot;{\&quot;productName\&quot;: \&quot;노트북\&quot;, \&quot;price\&quot;: 1500000}&quot;;

        // 사람 객체로 변환
        Person person = parseJson(personJson, Person.class);
        System.out.println(&quot;이름: &quot; + person.name + &quot;, 나이: &quot; + person.age);

        // 상품 객체로 변환
        Product product = parseJson(productJson, Product.class);
        System.out.println(&quot;상품명: &quot; + product.productName + &quot;, 가격: &quot; + product.price);
    }
}

// 데이터 클래스 정의
class Person {
    String name;
    int age;
}

class Product {
    String productName;
    int price;
}</code></pre>
<blockquote>
<p>제네릭 메서드를 사용해서 외부에서 받아온 JSON 데이터를 자바 객체로 만드는 예시임
근데 실제로 프로젝트 할 때는 Gson 라이브러리 내부에 똑같은 제네릭 메서드가 내장되어있으니 손 쉽게 그걸 사용하면 됨!! 밑에 설명할거임 일단 간단하게 메서드에 대해 설명하자면</p>
</blockquote>
<pre><code class="language-java">public static ❓&lt;T&gt;❓ ❗T❗ parseJson(String json, Class❓&lt;T&gt;❓ clazz) {</code></pre>
<blockquote>
<p><code>❓&lt;T&gt;❓</code> : &quot;T라는 임의의 타입을 이제부터 쓰겠다!&quot; 선언.
<code>❗T❗</code> :   &quot;메서드의 반환값은 T라는 타입이고, 사용자가 입력한 타입에 따라 달라진다.&quot;</p>
</blockquote>
<blockquote>
<p>이로써 
<code>❓&lt;T&gt;❓</code>를 사용해서 어떤 타입이든 매개변수로 받을 수 있고
<code>❗T❗</code>를 사용해서 어떤 타입이로든 메서드 반환이 가능하단거임.</p>
</blockquote>
<p>그래서</p>
<pre><code class="language-java">        // 사람 객체로 변환
        ❗Person person❗ = parseJson(personJson, ❓Person.class❓);
        System.out.println(&quot;이름: &quot; + person.name + &quot;, 나이: &quot; + person.age);

        // 상품 객체로 변환
        ❗Product product❗ = parseJson(productJson, ❓Product.class❓);
        System.out.println(&quot;상품명: &quot; + product.productName + &quot;, 가격: &quot; + product.price);</code></pre>
<blockquote>
<p>❓: <code>&lt;T&gt;</code>, 어떤 타입으로든 매개변수 넣을 수 있음
❗: <code>T</code>, 어떤 타입으로든 반환 가능</p>
</blockquote>
<br />
<br />
<br />

<h4 id="gson이-뭔데">Gson이 뭔데?</h4>
<ul>
<li>Gson(지슨)은 구글에서 만든 <strong><em>자바용 JSON 직렬화/역직렬화 라이브러리</em></strong>야.</li>
<li>즉, <strong><em>자바 객체를 JSON 문자열로 변환</em></strong>하거나, 반대로 <strong><em>JSON 문자열을 자바 객체로 변환</em></strong>할 때 사용하지.</li>
</ul>
<p><strong><em>Gson이 필요한 이유</em></strong></p>
<ul>
<li>자바에서 JSON 데이터를 직접 다루려면 복잡한 처리가 필요해.</li>
<li>Gson은 이 과정을 아주 쉽게 만들어주는 역할을 해.</li>
</ul>
<br />

<p><strong><em>Gson 사용법</em></strong></p>
<p><strong><em>1. 객체를 JSON으로 변환(직렬화)</em></strong></p>
<pre><code class="language-java">import com.google.gson.Gson;

class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person(&quot;홍길동&quot;, 27);

        Gson gson = new Gson();
        String json = gson.toJson(person);

        System.out.println(json);
    }
}


출력(json)
{&quot;name&quot;:&quot;홍길동&quot;,&quot;age&quot;:27}</code></pre>
<br />

<p><strong><em>2. JSON을 객체로 변환 (역직렬화)</em></strong></p>
<pre><code class="language-java">import com.google.gson.Gson;

class Person {
    String name;
    int age;
}

public class Main {
    public static void main(String[] args) {
        String json = &quot;{\&quot;name\&quot;:\&quot;홍길동\&quot;,\&quot;age\&quot;:27}&quot;;

        Gson gson = new Gson();
        Person person = gson.fromJson(json, Person.class);

        System.out.println(&quot;이름: &quot; + person.name + &quot;, 나이: &quot; + person.age);
    }
}


출력(객체)
이름: 홍길동, 나이: 27</code></pre>
<br />
<br />

<p><strong><em>Gson 사용법 요약</em></strong></p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
<th>사용 예시</th>
</tr>
</thead>
<tbody><tr>
<td><code>toJson()</code></td>
<td>객체 → JSON 변환 (직렬화)</td>
<td><code>String json = gson.toJson(객체);</code></td>
</tr>
<tr>
<td><code>fromJson()</code></td>
<td>JSON → 객체 변환 (역직렬화)</td>
<td><code>객체 = gson.fromJson(json, 클래스명.class);</code></td>
</tr>
</tbody></table>
<br />

<p><strong><em>JavsScript vs Javs JSON 처리 비교표</em></strong></p>
<table>
<thead>
<tr>
<th>구분</th>
<th>JavaScript</th>
<th>Java</th>
</tr>
</thead>
<tbody><tr>
<td><strong>타입 방식</strong></td>
<td>동적 타입</td>
<td>정적 타입</td>
</tr>
<tr>
<td><strong>JSON 처리 방식</strong></td>
<td>내장 메서드 (<code>JSON.parse()</code>) 사용</td>
<td>외부 라이브러리(Gson, Jackson) 필요</td>
</tr>
<tr>
<td><strong>객체로 변환 시 타입 정의</strong></td>
<td>불필요</td>
<td>필수</td>
</tr>
<tr>
<td><strong>객체의 필드 접근</strong></td>
<td>자유롭게 접근 가능</td>
<td>미리 정의된 필드만 접근 가능</td>
</tr>
</tbody></table>
<br />
<br />
<br />

<blockquote>
<p>그동안 제일 헷갈렸던 json을 변환하는 법...을 배웠다
제네릭에 대한 이해도도 부족해서 코드를 읽는 법도 많이 부족했는데
제네릭 강의를 통해 이해력이 좋아진 거 같아 기분 째진다!!!!!!!!속이 다 시원하다</p>
</blockquote>