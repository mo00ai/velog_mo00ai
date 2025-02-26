<h3 id="static">Static</h3>
<ul>
<li><p><code>static</code> 키워드는 모든 객체가 함께 사용하는 <code>변수</code>나 <code>메서드</code>를 만들때 사용됩니다.</p>
</li>
<li><p><code>객체(인스턴스)</code>를 만들지 않아도 클래스 이름만으로 바로 사용할 수 있습니다.</p>
</li>
<li><p>모든 객체가 같은 값을 공유합니다.</p>
<p>  → <strong>공용 게시판</strong>이라고 생각하시면 이해하기 쉽습니다.</p>
</li>
<li><p><code>static</code> 변수와 메서드는 한 번만 생성되고 <code>Method Area(메서드영역)</code> 에 저장됩니다.</p>
</li>
<li><p><code>static</code> 키워드는 변수, 메서드에 붙일 수 있습니다.</p>
</li>
<li><p><strong><code>static</code> 키워드로 선언된 변수와 메서드는 MethodArea 에 저장</strong>됩니다.</p>
</li>
<li><p>각 <strong>객체(인스턴스)</strong>는 클래스영역에 저장된 데이터를 활용할 수 있습니다</p>
</li>
</ul>
<br />
<br />

<p>인스턴스 멤버</p>
<ul>
<li>객체를 만들때 마다 생성되는 <code>변수</code>와 <code>메서드</code> 입니다.</li>
<li>객체(인스턴스)를 생성한 후에만 사용할 수 있습니다.</li>
<li>각 객체가 개별적으로 값을 가집니다. (공유되지 않음)</li>
<li>인스턴스는 <code>Heap</code> 영역에 위치합니다.</li>
</ul>
<p>인스턴스 변수</p>
<ul>
<li>객체가 생성될 때마다 따로 만들어지는 변수입니다.</li>
<li>객체를 생성한 후 접근할 수 있습니다.</li>
<li><code>name</code> 변수는 각 객체마다 별도로 저장됩니다.</li>
</ul>
<pre><code>class Person {
        String name; // ✅ 인스턴스 변수
}</code></pre><p>인스턴스 메서드</p>
<ul>
<li>객체의 속성을 활용하는 메서드입니다.</li>
<li>객체가 생성된 후에만 사용할 수 있습니다.</li>
</ul>
<pre><code>class Person {
        String name;

        void printName() { // ✅ 인스턴스 메서드
                System.out.println(&quot;나의 이름은 &quot; + this.name + &quot;입니다.&quot;);
        }
}</code></pre><br />

<p>클래스 멤버</p>
<ul>
<li>클래스 자체에 속하는 <code>변수</code>와 <code>메서드</code>를 의미합니다.</li>
<li><code>static</code> 키워드를 사용해서 선언합니다.</li>
<li>해당 클래스로 만들어진 객체가 공유해서 사용할 수 있습니다.</li>
<li>클래스가 로드될때 <code>Method Area</code> 에 적재됩니다.</li>
<li>객체 생성 없이 사용 가능합니다.</li>
</ul>
<p>클래스 변수</p>
<ul>
<li><p>클래스가 로드될 때 한 번만 생성됩니다.</p>
</li>
<li><p>모든 객체가 <strong><em>공유</em></strong>하는 변수입니다.</p>
</li>
<li><p><code>Heap</code> 이 아니라 <code>Method Area</code> 에 저장됩니다.</p>
</li>
<li><p>객체를 만들지 않아도 <code>클래스명.변수명</code>으로 접근가능합니다.</p>
<pre><code>class Person {
      static int population = 0; // ✅ 클래스 변수
}</code></pre><pre><code>public class Main {
  public static void main(String[] args) {

      // ✅ 객체 생성 전에도 클래스 레벨에서 직접 접근가능
      System.out.println(&quot;현재 인구 수: &quot; + Person.population);

      Person p1 = new Person();
      Person p2 = new Person();

      // ✅ 모든 객체가 하나의 값을 공유
      System.out.println(&quot;현재 인구 수: &quot; + Person.population);
  }
}</code></pre></li>
</ul>
<p>클래스 메서드를 알아봅시다</p>
<ul>
<li><p>클래스에 속하는 메서드입니다.</p>
</li>
<li><p>객체 없이 사용할 수 있습니다.</p>
</li>
<li><p>클래스 변수만 사용할 수 있고 인스턴스 변수는 사용할 수 없습니다.</p>
<pre><code>class Person {
      static int population = 0;

      public Person(String name) {
              this.name = name;
              population++; // 생성자 호출시 populataion 1 증가
      }

      static void printPopulation() {
              System.out.println(&quot;현재 인구 수: &quot; + population); // ✅ 클래스 메서드
      }
}</code></pre></li>
</ul>
<br />
<br />

<p>주의!!</p>
<ul>
<li><p>static은 공유가 필요한 곳에 사용해야 됨</p>
</li>
<li><p>멤버변수에 무턱대고 쓰면 안되겠지</p>
<pre><code>public class Student {
  static String name; // ⚠️ 모든 객체가 동일한 name을 공유 (위험)

  public Student(String name) {
      this.name = name;
  }

  public void printName() {
      System.out.println(&quot;이름: &quot; + name);
  }

</code></pre></li>
</ul>
<p>}</p>
<pre><code>-</code></pre><p>public class Main {</p>
<pre><code>public static void main(String[] args) {
    Student s1 = new Student(&quot;gygim&quot;);
    Student s2 = new Student(&quot;Steve&quot;);

    s1.printName();  // ⚠️ &quot;이름: Steve&quot;
    s2.printName();  // ⚠️ &quot;이름: Steve&quot;
}</code></pre><p>}</p>
<pre><code>
&lt;br&gt;

Static메서드에서 인스턴스 변수에 접근할 수 없음
- 일반 멤버변수에 접근할 수 없다는 거임</code></pre><p>public class Person {
    String name;</p>
<pre><code>public static void staticMethod() {
    System.out.println(this.name);  // ⚠️ 오류 발생
}</code></pre><p>}</p>
<pre><code>
&lt;br&gt;

#### static 은 꼭 필요할 때만 사용해야 합니다.

&lt;aside&gt;
⚠️

`static` 변수와 메모리는 프로그램이 종료될 때까지 메모리에 유지됩니다.

- 너무 많은 `static`  남용하면 메모리 낭비로 이어집니다.
&lt;/aside&gt;


&lt;br&gt;
&lt;br&gt;

---

&lt;br&gt;
&lt;br&gt;

### Final
- 변수는 변경이 불가능하게
- 클래스는 상속할 수 없게
- 메서드는 수정할 수 없게(오버라이딩 불가능)

&lt;br&gt;
&lt;br&gt;


상수(constant)
- `상수`는 변하지 않고 항상 일정한 값을 갖는 수 입니다.
- Java에서 상수는 **대문자로 표현하는 것이 관례**입니다.
- 프로그램 실행중에 절대 변경되서는 안되기 때문에 `static final` 키워드를 사용해 선언합니다.
- `static` 으로 선언된 변수는 프로그램 시작시 한 번만 초기화되고 모든 인스턴스에서 같은 값을 공유합니다.</code></pre><p>public class Circle {</p>
<pre><code>final static double PI = 3.14159; // ✅ 상수 선언</code></pre><p>}</p>
<pre><code>
&lt;br&gt;

static 으로 선언하는 이유(복습)
- 보통 상수는 여러 곳에서 값을 공유해 쓰일 목적으로 활용됩니다.
- 인스턴스 변수를 `static` 없이 선언할 경우 인스턴스마다 `PI` 값이 중복 저장됩니다.

&lt;br&gt;

불변객체(Immutable Object)
- `불변객체`는 내부 상태를 변경할 수 없는 객체입니다.
- `final` 을 속성(property, field) 에 활용합니다.
- 세터(setter) 없이 설계 합니다.
- 변경이 필요할 경우 새로운 객체를 만들어야 합니다.
- 예) `String` , `Integer` , `래퍼클래스` 등</code></pre><p>public final class Circle {</p>
<pre><code>final static double PI = 3.14159; 
final double radius; // ✅ final 로 선언해서 값이 변경되지 않도록 합니다.

Circle(double radius)  {
    this.radius = radius;
}</code></pre><p>}</p>
<pre><code>
&lt;br&gt;

불변 객체의 값이 변경이 필요한 경우
- 불변성을 유지하면서 값을 변경하는 효과를 얻을 때 활용합니다.
- **기존 객체의 상태를 직접 변경할 수 없기 때문에 새로운 객체를 생성**합니다.
- 생성자를 새로 호출하거나 아래의 기능을 활용할 수 있습니다.</code></pre><p>public final class Circle {
    public static final double PI = 3.14159;
    private final double radius;</p>
<pre><code>public Circle(double radius) {
    this.radius = radius;
}

// ✅ 반지름이 다른 새로운 Circle 생성 (불변 객체 유지)
public Circle changeRadius(double newRadius) {
    return new Circle(newRadius); // 생성자 호출: 기존 객체 변경 X, 새 객체 생성
}</code></pre><p>}
```</p>