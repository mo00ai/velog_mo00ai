<h3 id="익명-클래스">익명 클래스</h3>
<ul>
<li><code>익명 클래스</code>는 이름이 없는 클래스를 익명 클래스라고 합니다.</li>
<li>별도의 클래스 파일을 만들지 않고 코드 내에서 일회성으로 정의해 사용하기 때문에 이름이 없다고 부릅니다.</li>
<li><code>인터페이스</code>, <code>클래스(일반, 추상)</code>의 구현과 상속을 활용해 익명 클래스를 구현할 수 있습니다.
→ 람다에서는 인터페이스를 사용한 익명 클래스가 활용됩니다.</li>
</ul>
<br />

<h4 id="인터페이스를-활용한-익명-클래스-예제">인터페이스를 활용한 익명 클래스 예제</h4>
<p>익명 클래스를 코드내에서 직접 구현하기 때문에 클래스 파일을 만들 필요가 없습니다.
→ 하지만 코드가 길어집니다.</p>
<pre><code class="language-java">public interface Calculator {

    int sum(int a, int b);
}


public class Main {

    public static void main(String[] args) {

            // ✅ 익명 클래스 활용
        Calculator calculator1 = new Calculator() {
            @Override
            public int sum(int a, int b) {
                return a + b;
            }
        };

        int ret1 = calculator1.sum(1, 1);
        System.out.println(&quot;ret1 = &quot; + ret1);
    }
}</code></pre>
<br />
<br />

<hr />
<br />

<h3 id="람다-lamb람다lambda가-무엇인지-학습해-봅시다">람다 (Lamb<strong>람다(Lambda)가 무엇인지 학습해 봅시다.</strong></h3>
<ul>
<li>람다는 익명 클래스를 더 간결하게 표현하는 문법입니다.</li>
<li><code>함수형 인터페이스</code> 를 통해서 구현하는 것을 권장합니다.
→ 하나의 추상 메서드만 가져야하기 때문입니다.
→ 하지만, 하나의 추상 메서드를 가진 일반 인터페이스를 통해서도 사용 가능합니다.</li>
</ul>
<br />

<h4 id="람다식을-활용한-익명-클래스-변환-방법">람다식을 활용한 익명 클래스 변환 방법</h4>
<ul>
<li>컴파일 시점에 컴파일러가 <code>(a, b) -&gt; a + b</code> 람다 표현식을 보고 <code>sum()</code> 메서드를 가진 익명 클래스를 구현합니다.</li>
<li><code>Calculator</code> 인터페이스에 추상 메서드가 하나뿐이기 때문에 컴파일러는 <code>(a, b) -&gt; a + b</code> 람다 표현식이<code>sum()</code> 메서드라고 추론 가능하기 때문입니다</li>
</ul>
<pre><code class="language-java">// 람다 표현식
Calculator calculator1 = (a, b) -&gt; a + b;

// 익명클래스
Calculator calculator1 = new Calculator() {
        @Override
        public int sum(int a, int b) {
                return a + b;
        }
};


@FunctionalInterface // ✅ 함수형 인터페이스 선언 어노테이션
public interface Calculator {

    int sum(int a, int b); // ✅ 오직 하나의 추상 메서드만 선언해야합니다.
}


public class Main {

    public static void main(String[] args) {

            ...

        // ✅ 람다식 활용
        Calculator calculator2 = (a, b) -&gt; a + b;
        int ret2 = calculator2.sum(2, 2);
        System.out.println(&quot;ret2 = &quot; + ret2);
    }
}</code></pre>
<blockquote>
<p>@FunctionalInterface
함수형 인터페이스 선언 어노테이션
-&gt; 한 인터페이스에 하나의 추상 메서드만 사용하게끔 제약 걸어줌
-&gt; 이렇게 제약을 안 걸면 프로그램이 여러 추상 메서드 중 어떤 걸 골라서 람다식을 실행할지 판단 못하니까.</p>
</blockquote>
<br />
<br />

<h4 id="람다-사용시-주의사항">람다 사용시 주의사항</h4>
<ul>
<li><p>람다식을 활용할때는 꼭 <code>함수형 인터페이스</code>를 활용합시다.</p>
</li>
<li><p><code>함수형 인터페이스</code>는 단 하나의 추상 메서드만 가지도록 강제하는 어노테이션입니다.</p>
</li>
<li><p>람다식에서는 함수형 인터페이스가 활용됩니다.</p>
</li>
<li><p>인터페이스에 두 개 이상의 추상 메서드가 존재하면 컴파일러가 어떤  메서드를 구현하는지 모호해지기 때문입니다.</p>
</li>
<li><p>예를 들어 <strong><code>오버로딩(Overloading)</code></strong> 기능을 통해 같은 이름의 <code>sum()</code> 메서드를 여러 형태로 정의한다면 람다 표현식이 어떤 메서드를 구현하는 것인지 명확하지 않아 모호성이 발생할 수 있습니다.</p>
</li>
</ul>
<pre><code class="language-java">public interface Calculator {
    int sum(int a, int b);        // ✅ 선언 가능
    int sum(int a, int b, int c); // ⚠️ 오버로딩으로 선언 가능 모호성 발생!
}


@FunctionalInterface // ✅ 함수형 인터페이스 선언
public interface Calculator {
    int sum(int a, int b); // ✅ 오직 하나의 추상 메서드만 선언해야합니다.
    int sum(int a, int b, int c); // ❌ 선언 불가 에러발생!
}</code></pre>
<br />

<p><strong><code>오버로딩(Overloading)</code> vs <code>오버라이딩(Overriding)</code></strong> </p>
<ul>
<li><strong><code>오버로딩</code></strong>은 같은 클래스나 인터페이스 내에서 <strong>동일한 메서드 이름</strong>을 사용해서 선언하는 기능입니다.
→  매개변수의 개수나 타입, 순서는 다르게 선언해야 합니다.</li>
<li><strong><code>오버라이딩</code></strong>은 부모 클래스에 정의된 메서드를 자식 클래스에서 재정의하는 것을 의미합니다.</li>
</ul>
<br />
<br />
<br />


<h4 id="람다식을-매개변수로-전달하는-방법">람다식을 매개변수로 전달하는 방법</h4>
<br />

<p><strong><em>익명 클래스를 변수에 담아 전달</em></strong></p>
<ul>
<li><p>람다식 없이 직접 객체를 생성해서 전달하는 방식입니다.</p>
</li>
<li><p>클래스의 익명 객체를 만든 다음에 매개변수로 전달합니다.</p>
<pre><code class="language-java">public class Main {
  public static int calculate(int a, int b, Calculator calculator) {
      return calculator.sum(a, b);
  }

  public static void main(String[] args) {

      Calculator cal1 = new Calculator() {
          @Override
          public int sum(int a, int b) {
              return a + b;
          }
      };

      // ✅ 익명 클래스를 변수에 담아 전달
      int ret3 = calculate(3, 3, cal1);
      System.out.println(&quot;ret3 = &quot; + ret3); // 출력: ret3 = 6
  }
}</code></pre>
</li>
</ul>
<br />


<p><strong><em>람다식을 변수에 담아 전달</em></strong></p>
<ul>
<li>람다식을 변수에 담아 매개변수로 전달하는 방식입니다.</li>
<li>람다식을 전달하면 <code>calculate()</code> 메서드의  매개변수의 타입으로 <code>Calculator</code> 인터페이스를 구현했는지 추론되기 때문에 람다식을 전달 가능합니다.</li>
</ul>
<pre><code class="language-java">public class Main {

    public static int calculate(int a, int b, Calculator calculator) {
        return calculator.sum(a, b);
    }

    public static void main(String[] args) {
        Calculator cal2 = (a, b) -&gt; a + b;

        // ✅ 람다식을 변수에 담아 전달
        int ret4 = calculate(4, 4, cal2);
        System.out.println(&quot;ret4 = &quot; + ret4); // 출력: ret4 = 8
    }
}</code></pre>
<br />

<p><strong><em>람다식을 직접 전달</em></strong></p>
<ul>
<li>람다식을 직접 전달합니다.</li>
<li>마찬가지로 <code>calculate()</code> 메서드의  매개변수의 타입으로 <code>Calculator</code> 인터페이스를 구현했는지 추론됩니다.</li>
</ul>
<pre><code class="language-java">public class Main {

    public static int calculate(int a, int b, Calculator calculator) {
        return calculator.sum(a, b);
    }

    public static void main(String[] args) {
        // ✅ 람다식을 직접 매개변수로 전달
        int ret5 = calculate(5, 5, (a, b) -&gt; a + b);
        System.out.println(&quot;ret5 = &quot; + ret5); // 출력: ret5 = 10
    }
}</code></pre>