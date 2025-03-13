<p>코드카타 풀 때마다 막히는 정렬에 대해 정리해보고자 한다...........
ㅜ ㅁ ㅜ
ㄱㄱ</p>
<hr />
<h2 id="comparable과-comparator">Comparable과 Comparator</h2>
<h3 id="📚-java-comparable과-comparator-차이점-정리">📚 Java <code>Comparable</code>과 <code>Comparator</code> 차이점 정리</h3>
<table>
<thead>
<tr>
<th>항목</th>
<th>Comparable</th>
<th>Comparator</th>
</tr>
</thead>
<tbody><tr>
<td>패키지</td>
<td><code>java.lang</code></td>
<td><code>java.util</code></td>
</tr>
<tr>
<td>구현 방법</td>
<td>객체 자체에 비교 기준을 정의</td>
<td>외부에서 비교 기준을 별도로 정의</td>
</tr>
<tr>
<td>정렬 기준</td>
<td>기본 정렬 기준</td>
<td>여러 정렬 기준을 정의 가능</td>
</tr>
<tr>
<td>구현 방식</td>
<td><code>compareTo()</code> 메서드 오버라이딩</td>
<td><code>compare()</code> 메서드 오버라이딩</td>
</tr>
<tr>
<td>사용 예시</td>
<td>Collections.sort(list); Arrays.sort(array);</td>
<td>Collections.sort(list, comparator); Arrays.sort(array, comparator);</td>
</tr>
</tbody></table>
<hr />
<h3 id="✅-comparable-예시">✅ <code>Comparable</code> 예시</h3>
<pre><code class="language-java">class Person implements Comparable사람 {
    int age;

    public Person(int age) {
        this.age = age;
    }

    @Override
    public int compareTo(Person o) {
        return this.age - o.age;
    }
}

List사람 list = new ArrayList&lt;&gt;();
list.add(new Person(25));
list.add(new Person(20));
Collections.sort(list);</code></pre>
<hr />
<h3 id="✅-comparator-예시">✅ <code>Comparator</code> 예시</h3>
<pre><code class="language-java">class Person {
    int age;

    public Person(int age) {
        this.age = age;
    }
}

Comparator사람 comparator = (p1, p2) -&gt; p1.age - p2.age;

List사람 list = new ArrayList사람();
list.add(new Person(25));
list.add(new Person(20));
Collections.sort(list, comparator);</code></pre>
<hr />
<h3 id="⚠️-사용-시-주의사항">⚠️ 사용 시 주의사항</h3>
<ul>
<li><code>Comparable</code>은 <strong>객체 자체에 비교 기준</strong>을 두므로, <strong>한 가지 기준만</strong> 정의 가능.  </li>
<li><code>Comparator</code>는 <strong>외부에서 여러 비교 기준을 정의</strong>할 수 있어 유연성이 높음.  </li>
<li><code>Comparator</code>를 사용하면 <strong>람다식</strong>으로 간단하게 비교 기준을 작성할 수 있음.</li>
</ul>
<hr />
<h3 id="정리">정리</h3>
<ul>
<li><code>Comparable</code>은 클래스에 comparable인터페이스를 구현한 후 compareTo() 메서드를 오버라이딩해서 정렬 기준을 작성함<ul>
<li>매우 귀찮</li>
<li>한 가지의 정렬 기준</li>
</ul>
</li>
<li><code>Comparator</code>은 클래스에 Comparator를 구현하지 않아도 되고, 람다식이나 익명 클래스로 정렬 기준을 작성함<ul>
<li>안귀찮, 그래서 상용됨.</li>
<li>정렬 시 Collections.sort()나 Arrays.sort()에 Comparator를 함께 전달해야 함.</li>
<li>여러 개의 정렬 기준 사용 가능</li>
</ul>
</li>
</ul>
<hr />
<br />
<br />

<hr />
<h2 id="comparator">Comparator</h2>
<ul>
<li>Comparator는 Java에서 객체를 커스텀 기준으로 정렬할 때 사용하는 인터페이스입니다.</li>
<li>Comparable은 객체 자체에 정렬 기준을 정의하는 반면, Comparator는 외부에서 정렬 기준을 정의합니다.</li>
<li>즉, Comparator는 객체에 종속되지 않고, 다양한 기준으로 정렬할 수 있어 유연성이 매우 높습니다.</li>
</ul>
<hr />
<h3 id="✅-comparator의-기본-구조">✅ Comparator의 기본 구조</h3>
<ul>
<li>Comparator는 compare() 메서드를 오버라이딩하여 정렬 기준을 정의합니다.<pre><code class="language-java">복사
편집
public interface Comparator&lt;T&gt; {
  int compare(T o1, T o2);
}</code></pre>
<pre><code class="language-java">반환값 의미:
음수: o1이 o2보다 먼저 온다.
0: 두 객체의 순서가 같다.
양수: o1이 o2보다 나중에 온다.</code></pre>
</li>
</ul>
<hr />
<h3 id="✅-comparator-기본-사용법-익명-클래스">✅ Comparator 기본 사용법 (익명 클래스)</h3>
<pre><code class="language-java">import java.util.*;

class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class Main {
    public static void main(String[] args) {
        List&lt;Person&gt; people = Arrays.asList(
            new Person(&quot;Alice&quot;, 25),
            new Person(&quot;Bob&quot;, 20),
            new Person(&quot;Charlie&quot;, 30)
        );

        // 나이 기준 오름차순 정렬
        Collections.sort(people, new Comparator&lt;Person&gt;() {
            @Override
            public int compare(Person p1, Person p2) {
                return p1.age - p2.age;
            }
        });

        for (Person p : people) {
            System.out.println(p.name + &quot;: &quot; + p.age);
        }
    }
}

Bob: 20
Alice: 25
Charlie: 30</code></pre>
<hr />
<h3 id="✅-comparator--람다식-더-간단한-방법">✅ Comparator + 람다식 (더 간단한 방법)</h3>
<ul>
<li>Java 8 이후부터는 람다식을 사용해 Comparator를 더 간결하게 작성할 수 있습니다.<pre><code class="language-java">Collections.sort(people, (p1, p2) -&gt; p1.age - p2.age);
</code></pre>
</li>
</ul>
<p>//List.sort() 로 더 간단하게
people.sort((p1, p2) -&gt; p1.age - p2.age);</p>
<pre><code>
---

### ✅ Comparator.comparing() 사용하기 (가장 추천하는 방법)
```java
people.sort(Comparator.comparing(person -&gt; person.age));

//또는 메서드 참조 사용
people.sort(Comparator.comparing(Person::getAge));</code></pre><hr />
<h3 id="✅-내림차순-정렬-reverseorder">✅ 내림차순 정렬 (reverseOrder)</h3>
<pre><code class="language-java">people.sort(Comparator.comparingInt(person -&gt; person.age).reversed());</code></pre>
<hr />
<h3 id="✅-여러-기준으로-정렬-thencomparing">✅ 여러 기준으로 정렬 (thenComparing)</h3>
<pre><code class="language-java">people.sort(Comparator.comparingInt((Person p) -&gt; p.age)
                      .thenComparing(p -&gt; p.name));</code></pre>
<ul>
<li><strong>thenComparing()</strong>을 사용하면 1차, 2차 정렬을 쉽게 설정할 수 있습니다.</li>
</ul>
<hr />
<h3 id="✅-comparator의-주요-메서드">✅ Comparator의 주요 메서드</h3>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
<th>사용 예시</th>
</tr>
</thead>
<tbody><tr>
<td><code>compare()</code></td>
<td>두 객체를 비교하여 정렬 순서를 결정</td>
<td><code>Comparator&lt;Person&gt; comparator = (p1, p2) -&gt; p1.age - p2.age;</code></td>
</tr>
<tr>
<td><code>comparing()</code></td>
<td>특정 필드를 기준으로 정렬</td>
<td><code>people.sort(Comparator.comparing(Person::getAge));</code></td>
</tr>
<tr>
<td><code>comparingInt()</code></td>
<td><code>int</code> 타입 필드를 기준으로 정렬</td>
<td><code>people.sort(Comparator.comparingInt(Person::getAge));</code></td>
</tr>
<tr>
<td><code>comparingDouble()</code></td>
<td><code>double</code> 타입 필드를 기준으로 정렬</td>
<td><code>list.sort(Comparator.comparingDouble(Product::getPrice));</code></td>
</tr>
<tr>
<td><code>reversed()</code></td>
<td>정렬 순서를 반대로 변경</td>
<td><code>people.sort(Comparator.comparing(Person::getAge).reversed());</code></td>
</tr>
<tr>
<td><code>thenComparing()</code></td>
<td>1차 정렬 기준이 같을 때 2차 기준을 적용</td>
<td><code>people.sort(Comparator.comparing(Person::getAge).thenComparing(Person::getName));</code></td>
</tr>
<tr>
<td><code>thenComparingInt()</code></td>
<td>2차 정렬 기준으로 <code>int</code> 타입 필드 사용</td>
<td><code>people.sort(Comparator.comparing(Person::getName).thenComparingInt(Person::getAge));</code></td>
</tr>
<tr>
<td><code>naturalOrder()</code></td>
<td>기본 정렬 순서(오름차순)를 적용</td>
<td><code>list.sort(Comparator.naturalOrder());</code></td>
</tr>
<tr>
<td><code>reverseOrder()</code></td>
<td>기본 정렬 순서의 반대(내림차순)를 적용</td>
<td><code>list.sort(Comparator.reverseOrder());</code></td>
</tr>
<tr>
<td><code>nullsFirst()</code></td>
<td><code>null</code> 값을 먼저 정렬</td>
<td><code>list.sort(Comparator.nullsFirst(Comparator.naturalOrder()));</code></td>
</tr>
<tr>
<td><code>nullsLast()</code></td>
<td><code>null</code> 값을 나중에 정렬</td>
<td><code>list.sort(Comparator.nullsLast(Comparator.naturalOrder()));</code></td>
</tr>
</tbody></table>
<hr />
<h3 id="✅-comparator-고급-예시">✅ Comparator 고급 예시</h3>
<h4 id="1-이름-오름차순-나이-내림차순-정렬">1. 이름 오름차순, 나이 내림차순 정렬</h4>
<pre><code class="language-java">people.sort(Comparator.comparing(Person::getName)
                      .thenComparing(Comparator.comparingInt(Person::getAge).reversed()));
</code></pre>
<h4 id="2-null-값을-먼저-정렬">2. null 값을 먼저 정렬</h4>
<pre><code class="language-java">List&lt;String&gt; list = Arrays.asList(&quot;banana&quot;, null, &quot;apple&quot;);
list.sort(Comparator.nullsFirst(Comparator.naturalOrder()));
System.out.println(list); // [null, apple, banana]</code></pre>
<h4 id="3-comparator와-스트림-함께-사용">3. Comparator와 스트림 함께 사용</h4>
<pre><code class="language-java">List&lt;String&gt; names = Arrays.asList(&quot;banana&quot;, &quot;apple&quot;, &quot;cherry&quot;);
List&lt;String&gt; sortedNames = names.stream()
                                .sorted(Comparator.comparing(String::length))
                                .toList();

System.out.println(sortedNames); // [apple, banana, cherry]</code></pre>
<hr />
<h3 id="comparator-람다식-정리">Comparator 람다식 정리</h3>
<table>
<thead>
<tr>
<th>정렬 기준</th>
<th>사용 예시</th>
</tr>
</thead>
<tbody><tr>
<td>숫자 오름차순</td>
<td><code>(a, b) -&gt; a - b</code></td>
</tr>
<tr>
<td>숫자 내림차순</td>
<td><code>(a, b) -&gt; b - a</code></td>
</tr>
<tr>
<td>문자열 오름차순</td>
<td><code>(s1, s2) -&gt; s1.compareTo(s2)</code></td>
</tr>
<tr>
<td>문자열 내림차순</td>
<td><code>(s1, s2) -&gt; s2.compareTo(s1)</code></td>
</tr>
<tr>
<td>객체 필드 기준 오름차순</td>
<td><code>Comparator.comparing(Person::getAge)</code></td>
</tr>
<tr>
<td>객체 필드 기준 내림차순</td>
<td><code>Comparator.comparing(Person::getAge).reversed()</code></td>
</tr>
<tr>
<td>다중 정렬</td>
<td><code>Comparator.comparing(Person::getAge).thenComparing(Person::getName)</code></td>
</tr>
<tr>
<td>null을 먼저 정렬</td>
<td><code>Comparator.nullsFirst(Comparator.naturalOrder())</code></td>
</tr>
<tr>
<td>null을 나중에 정렬</td>
<td><code>Comparator.nullsLast(Comparator.naturalOrder())</code></td>
</tr>
</tbody></table>
<hr />
<br />
<br />

<hr />
<h2 id="compareto-메서드">compareTo() 메서드</h2>
<ul>
<li>compareTo()는 Java에서 Comparable 인터페이스에 정의된 메서드로, 객체를 기본 정렬(자연 정렬, Natural Ordering) 기준으로 비교할 때 사용됩니다.<blockquote>
<p><strong>Comparable</strong>을 구현한 클래스는 compareTo() 메서드를 오버라이딩하여 정렬 기준을 정의합니다.</p>
</blockquote>
</li>
</ul>
<hr />
<h3 id="✅-compareto-메서드-기본-구조">✅ compareTo() 메서드 기본 구조</h3>
<pre><code class="language-java">public int compareTo(T o)</code></pre>
<ul>
<li>매개변수: 비교 대상 객체 o.</li>
<li>반환값:<ul>
<li>양수 (&gt; 0) → 현재 객체가 비교 대상 객체보다 크다.</li>
<li>0 → 두 객체가 같다.</li>
<li>음수 (&lt; 0) → 현재 객체가 비교 대상 객체보다 작다.</li>
</ul>
</li>
</ul>
<hr />
<h3 id="✅-compareto가-어떻게-동작하는지">✅ compareTo()가 어떻게 동작하는지?</h3>
<h4 id="1-문자열string-비교">1. 문자열(String) 비교</h4>
<ul>
<li>String 클래스는 이미 Comparable을 구현하고 있어, compareTo()를 바로 사용할 수 있습니다.</li>
<li>사전순(lexicographical order, ASCII 값)을 기준으로 정렬됩니다.</li>
</ul>
<pre><code class="language-java">String a = &quot;apple&quot;;
String b = &quot;banana&quot;;

System.out.println(a.compareTo(b)); // -1 (apple이 banana보다 작음)
System.out.println(b.compareTo(a)); // 1  (banana가 apple보다 큼)
System.out.println(a.compareTo(a)); // 0  (동일함)</code></pre>
<ul>
<li>&quot;a&quot;의 아스키 값(97) - &quot;b&quot;의 아스키 값(98) → -1 → a가 b보다 작음.</li>
</ul>
<hr />
<h4 id="2-숫자integer-비교">2. 숫자(Integer) 비교</h4>
<ul>
<li>Integer 클래스도 Comparable을 구현하고 있어서 바로 사용 가능.<pre><code class="language-java">Integer num1 = 10;
Integer num2 = 20;
</code></pre>
</li>
</ul>
<p>System.out.println(num1.compareTo(num2)); // -1 (10 &lt; 20)
System.out.println(num2.compareTo(num1)); // 1  (20 &gt; 10)
System.out.println(num1.compareTo(num1)); // 0  (동일)</p>
<pre><code></code></pre>