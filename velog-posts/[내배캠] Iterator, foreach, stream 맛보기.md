<h3 id="iterator">Iterator</h3>
<ul>
<li>Iterator는 <strong><em>컬렉션(Collection)의 요소들을 순차적으로 탐색하는 인터페이스</em></strong>로, java.util 패키지에 포함되어 있습니다. 이를 사용하면 컬렉션의 내부 구현 방식에 관계없이 요소를 하나씩 가져올 수 있습니다.</li>
</ul>
<br />
<br />

<h3 id="iterator의-주요-메서드">Iterator의 주요 메서드</h3>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>boolean hasNext()</code></td>
<td><strong>다음 요소가 있는지 확인</strong> (<code>true</code>면 다음 요소가 존재)</td>
</tr>
<tr>
<td><code>E next()</code></td>
<td><strong>다음 요소 반환 및 커서 이동</strong></td>
</tr>
<tr>
<td><code>void remove()</code></td>
<td><strong>현재 요소 제거</strong> (선택적, 일부 컬렉션에서는 미지원)</td>
</tr>
</tbody></table>
<br />

<p>이터레이터 사용 예제</p>
<pre><code class="language-java">import java.util.*;

public class IteratorExample {
    public static void main(String[] args) {
        // 리스트 생성
        List&lt;String&gt; list = new ArrayList&lt;&gt;();
        list.add(&quot;Java&quot;);
        list.add(&quot;Python&quot;);
        list.add(&quot;C++&quot;);

        // Iterator 생성
        Iterator&lt;String&gt; iterator = list.iterator();

        // Iterator를 사용하여 요소 순회
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}</code></pre>
<blockquote>
<p>순차적으로 요소를 출력함</p>
</blockquote>
<br />

<p>remove() 메서드 사용 예제</p>
<pre><code class="language-java">import java.util.*;

public class IteratorRemoveExample {
    public static void main(String[] args) {
        List&lt;String&gt; list = new ArrayList&lt;&gt;(Arrays.asList(&quot;Apple&quot;, &quot;Banana&quot;, &quot;Orange&quot;, &quot;Grapes&quot;));

        Iterator&lt;String&gt; iterator = list.iterator();

        while (iterator.hasNext()) {
            String fruit = iterator.next();
            if (fruit.equals(&quot;Banana&quot;)) {
                iterator.remove(); // Banana 제거
            }
        }

        System.out.println(list); // [Apple, Orange, Grapes]
    }
}</code></pre>
<br />
<br />

<hr />
<br />

<h3 id="foreach">forEach</h3>
<p>forEach는 Java 8에서 <strong><em>Iterable 인터페이스에 추가된 default 메서드</em></strong>입니다.</p>
<blockquote>
<p>즉, List, Set, Queue 등 모든 Collection 객체는 Iterable을 구현하므로, forEach 메서드를 사용할 수 있습니다. </p>
</blockquote>
<p>참고</p>
<pre><code class="language-java">forEach(System.out::println);
는
list.forEach(s -&gt; System.out.println(s));
와 동일</code></pre>
<blockquote>
<p>향상된 for-each문 for(요소 : 요소배열) 을 메서드화 시킨 것</p>
</blockquote>
<br />

<br />

<hr />
<br />

<h3 id="stream">Stream</h3>
<p>✔ for-each</p>
<ul>
<li>간단한 컬렉션 순회에 가장 적합</li>
<li>가독성이 좋고 직관적</li>
<li>remove(), index 접근이 필요하면 사용 불가능</li>
</ul>
<p>✔ Iterator</p>
<ul>
<li>컬렉션을 순회하면서 안전하게 요소 제거 가능</li>
<li>보통 for-each보다 코드가 길어져 잘 사용되지 않음</li>
<li>최근에는 Stream API가 더 선호됨</li>
</ul>
<p>✔ Stream API (요즘 대세)</p>
<ul>
<li>코드가 간결하고 가독성이 뛰어남</li>
<li>필터링, 매핑, 정렬, 병렬 처리 등 강력한 기능 제공</li>
<li>하지만 요소 제거(remove())는 불가능</li>
<li>데이터를 한 번만 순회할 수 있어 반복 재사용이 어려울 수도 있음</li>
</ul>
<br />


<p>💡 즉,</p>
<ul>
<li>간단한 루프 → for-each</li>
<li>요소 제거 → Iterator</li>
<li>필터링/변환/병렬 처리 → Stream API</li>
</ul>
<p>요즘은 for-each와 Stream을 가장 많이 사용하고, Iterator는 특정 상황에서만 사용함! 🚀</p>
<br />
<br />
<br />