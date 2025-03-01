<h3 id="스트림">스트림</h3>
<ul>
<li><p><code>스트림</code>은 <strong>데이터를 효율적으로 처리할 수 있는 흐름</strong>입니다.</p>
</li>
<li><p><strong>선언형 스타일</strong>로 가독성이 굉장히 뛰어납니다.</p>
</li>
<li><p><code>데이터 준비 → 중간 연산 → 최종 연산</code> 순으로  처리됩니다.</p>
</li>
<li><p>스트림은 <code>컬렉션(List, Set 등)</code>과 함께 자주 활용됩니다.</p>
</li>
<li><p>오늘 수업에서는 실무에서 자주 활용되는 <code>map()</code> 과 <code>filter()</code> 예시를 살펴보겠습니다.</p>
</li>
<li><p>데이터 컬렉션(List, Set, Map 등)을 함수형 스타일로 처리할 수 있도록 도와주는 API</p>
</li>
</ul>
<br />

<hr />
<br />

<h3 id="비교해보기-for-vs-스트림">비교해보기 (for vs 스트림)</h3>
<p>각 요소를 10배로 변환 후 출력하는 예시로 알아봅시다.</p>
<ul>
<li><code>arrayList</code> 의 각 요소를 10배로 변환합니다.</li>
<li>아래 예시를 보고 <code>for</code> 문과 <code>스트림</code> 을 비교해 봅시다.</li>
</ul>
<br />

<p>for문</p>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        // ArrayList 선언
        List&lt;Integer&gt; arrayList = new ArrayList&lt;&gt;(List.of(1, 2, 3, 4, 5));

        // ✅ for 명령형 스타일: 각 요소 * 10 처리
        List&lt;Integer&gt; ret1 = new ArrayList&lt;&gt;();
        for (Integer num : arrayList) {
            int multipliedNum = num * 10; // 각 요소 * 10
            ret1.add(multipliedNum);
        }
        System.out.println(&quot;ret1 = &quot; + ret1); 
    }
}</code></pre>
<br />

<p>스트림 사용</p>
<pre><code>public class Main {

    public static void main(String[] args) {

        // ArrayList 선언
        List&lt;Integer&gt; arrayList = new ArrayList&lt;&gt;(List.of(1, 2, 3, 4, 5));

        // ✅ 스트림 선언적 스타일: 각 요소 * 10 처리
        List&lt;Integer&gt; ret2 = arrayList.stream().map(num -&gt; num * 10).collect(Collectors.toList());
        System.out.println(&quot;ret2 = &quot; + ret2);
    }
}</code></pre><br />

<p><strong><em>ArrayList 를 List 로 받는 이유</em></strong></p>
<ul>
<li><code>다형성</code>을 활용해 <code>List 인터페이스</code>로 <code>ArrayList</code> 구현체를 받으면 나중에 다른 구현체(<code>LinkedList</code> , <code>Vector</code>) 로 변경할 때 코드 수정을 최소화할 수 있기 때문입니다.</li>
<li>실무에서 리스트를 선언할 때 대부분 아래와 같이 <code>List</code> 타입으로 받는 것을 권장합니다.</li>
</ul>
<br />
<br />

<hr />
<br />

<h3 id="스트림-살펴보기선언형-스타일">스트림 살펴보기(선언형 스타일)</h3>
<p><strong><em>스트림 처리 단계를 살펴봅시다.</em></strong></p>
<ul>
<li>스트림은 데이터 처리를 위해 여러 API를 제공합니다.</li>
<li>관련 문서 → <a href="https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html">https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html</a></li>
<li>아래는 대표적인 API 예시입니다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/64596171-3562-4264-a636-c0242c7a5650/image.png" /></p>
<table>
<thead>
<tr>
<th>단계</th>
<th>설명</th>
<th>주요 API</th>
</tr>
</thead>
<tbody><tr>
<td><strong><em>1. 데이터 준비</em></strong></td>
<td>컬렉션을 스트림으로 변환</td>
<td><code>stream()</code>, <code>parallelStream()</code></td>
</tr>
<tr>
<td><strong><em>2. 중간 연산 등록 (즉시 실행되지 않음)</em></strong></td>
<td>데이터 변환 및 필터링</td>
<td><code>map()</code>, <code>filter()</code>, <code>sorted()</code></td>
</tr>
<tr>
<td><strong>3. 최종 연산</strong></td>
<td>최종 처리 및 데이터 변환</td>
<td><code>collect()</code>, <code>forEach()</code>, <code>count()</code></td>
</tr>
</tbody></table>
<br />
<br />

<p><strong>스트림을 사용하여 각 요소를 10배로 변환 후 리스트로 변환하는 예제입니다.</strong></p>
<ul>
<li><code>stream()</code> → <code>map()</code> → <code>collect()</code> 순으로 데이터 흐름을 처리합니다.</li>
<li><code>stream()</code>:  데이터 준비 - 데이터를 스트림으로 변환하여 연산 흐름을 만들 준비합니다.</li>
<li><code>map()</code>:  중간 연산 등록 - 각 요소를 주어진 함수에 적용해서 변환합니다.</li>
<li><code>collect()</code>: 최종 연산 - 결과를 원하는 형태(<code>List</code>, <code>Set</code>)로 수집합니다.</li>
<li>반복문 없이 간결하게 데이터 변환이 가능합니다.</li>
</ul>
<br />

<pre><code class="language-java">arrayList
    .stream()  // 1. 데이터 준비
    .map()     // 2. 중간 연산 등록
    .collect() // 3. 최종 연산</code></pre>
<pre><code class="language-java">// 1. 데이터 준비: 스트림 생성
Stream&lt;Integer&gt; stream = arrayList.stream();

// 2. 중간 연산 등록: 각 요소를 10배로 변환 로직 등록
Stream&lt;Integer&gt; mappedStream = stream.map(num -&gt; num * 10);

// 3. 최종 연산: 최종 결과 리스트로 변환
List&lt;Integer&gt; ret2 = mappedStream.collect(Collectors.toList());</code></pre>
<pre><code class="language-java">// ✅ 한 줄로 표현 가능
List&lt;Integer&gt; ret2 = arrayList.stream() // 1. 데이터 준비
    .map(num -&gt; num * 10)               // 2. 중간 연산 등록
    .collect(Collectors.toList());  // 3. 최종 연산</code></pre>
<br />
<br />

<h3 id="스트림과-람다식-활용">스트림과 람다식 활용</h3>
<br />

<p><strong><em>스트림과 람다식을 함께 사용해서 다시 한번 각 요소 * 10 예시를 만들어 봅시다.</em></strong></p>
<pre><code class="language-java">// map() 메서드를 살펴봅시다.
&lt;R&gt; Stream&lt;R&gt; map(Function&lt;? super T, ? extends R&gt; mapper);</code></pre>
<p><strong>스트림과 람다식을 함께 사용해서 다시 한번 <code>각 요소 * 10</code> 예시를 만들어 봅시다.</strong></p>
<pre><code class="language-java">// map() 메서드를 살펴봅시다.
&lt;R&gt; Stream&lt;R&gt; map(Function&lt;? super T, ? extends R&gt; mapper);
</code></pre>
<p>→ 함수형 인터페이스를 매개변수로 가지고 있습니다.</p>
<p>→ 즉, 함수형 인터페이스를 구현한 구현체를 매개변수로 받을 수 있습니다.</p>
<ul>
<li>익명 클래스와 람다를 만들고 <code>map()</code> 을 활용해 봅시다.</li>
<li>람다식을 활용했을 때와 아닐 때를 비교해 보세요.</li>
</ul>
<br />
<br />

<p><strong><em>익명 클래스를 변수에 담아 활용</em></strong></p>
<ul>
<li>Function&lt;T, R&gt; T 는 매개변수, R 은 반환 타입을 의미합니다.</li>
</ul>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        // ArrayList 선언
        List&lt;Integer&gt; arrayList = new ArrayList&lt;&gt;(List.of(1, 2, 3, 4, 5));

        // ✅ 1. 익명클래스를 변수에 담아 활용
        Function&lt;Integer, Integer&gt; function = new Function&lt;&gt;() {

            @Override
            public Integer apply(Integer integer) {
                return integer * 10;
            }
        };

        List&lt;Integer&gt; ret3 = arrayList.stream()
                .map(function)
                .collect(Collectors.toList());
        System.out.println(&quot;ret3 = &quot; + ret3);
    }
}</code></pre>
<br />

<p><strong><em>람다식을 변수로 활용</em></strong></p>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        // ArrayList 선언
        List&lt;Integer&gt; arrayList = new ArrayList&lt;&gt;(List.of(1, 2, 3, 4, 5));

        // ✅ 2. 람다식을 변수에 담아 활용
        Function&lt;Integer, Integer&gt; functionLambda = (num -&gt; num * 10);
        List&lt;Integer&gt; ret4 = arrayList.stream()
                .map(functionLambda)
                .collect(Collectors.toList());
        System.out.println(&quot;ret4 = &quot; + ret4);
    }
}</code></pre>
<br />

<p><strong><em>람다식을 매개변수에 직접 활용</em></strong></p>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        // ArrayList 선언
        List&lt;Integer&gt; arrayList = new ArrayList&lt;&gt;(List.of(1, 2, 3, 4, 5));

        // ✅ 3. 람다식을 직접 활용
        List&lt;Integer&gt; ret5 = arrayList.stream()
                .map(num -&gt; num * 10)
                .collect(Collectors.toList());
        System.out.println(&quot;ret5 = &quot; + ret5);
    }
}</code></pre>
<br />
<br />

<hr />
<br />

<h3 id="스트림-중간연산-함께-사용하기예-filter--map">스트림 중간연산 함께 사용하기(예: filter + map)</h3>
<p><strong>리스트에서 짝수만 10배로 변환시키는 예시를 통해 알아봅시다.</strong></p>
<ul>
<li>다양한 중간 연산을 조립하여 데이터 처리 흐름을 만들 수 있습니다.</li>
<li>아래 예시에서는 중간 연산(<code>filter()</code> 와 <code>map()</code> ) 을 조합하여 짝수만 10배 변환시킵니다.</li>
<li>선언적 코딩으로 코드의 유지 보수성과 가독성이 뛰어납니다.
→ 명령형 스타일(<code>for</code> 문) 과 비교해 보세요.</li>
</ul>
<br />

<p><strong><em>스트림 사용</em></strong></p>
<pre><code class="language-java">List&lt;Integer&gt; arrayList = new ArrayList&lt;&gt;(List.of(1, 2, 3, 4, 5));

// ✅ filter() + map() 사용 예제
List&lt;Integer&gt; ret6 = arrayList.stream() // 1. 데이터 준비: 스트림 생성
        .filter(num -&gt; num % 2 == 0)    // 2. 중간 연산: 짝수만 필터링
        .map(num -&gt; num * 10)           // 3. 중간 연산: 10배로 변환
        .collect(Collectors.toList()); // 4. 최종 연산: 리스트로 변환

System.out.println(ret6); // 출력: [20, 40]</code></pre>
<br />


<p><strong><em>for문 사용</em></strong></p>
<pre><code class="language-java">// For 문 예시
List&lt;Integer&gt; arrayList = new ArrayList&lt;&gt;(List.of(1, 2, 3, 4, 5));


List&lt;Integer&gt; ret6 = new ArrayList&lt;&gt;();
for (int num : arrayList) {
    int remain = num % 2;
    if (remain == 0) {
        int data = num * 10;
        ret6.add(data);
    }
}
// 5. 결과 출력
System.out.println(ret6); // 출력: [20, 40]</code></pre>
<br />
<br />
<br />

<hr />
<hr />
<hr />
<br />

<h2 id="생성-중간연산-최종-연산-메서드-정리">생성, 중간연산, 최종 연산 메서드 정리</h2>
<br />
<br />

<h3 id="stream-생성단계">Stream 생성단계</h3>
<table>
<thead>
<tr>
<th>방법</th>
<th>설명</th>
<th>코드 예시</th>
</tr>
</thead>
<tbody><tr>
<td><strong>1. 컬렉션에서 생성</strong></td>
<td><code>Collection</code>의 <code>stream()</code> 메서드를 사용</td>
<td><code>List&lt;String&gt; list = Arrays.asList(&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;);</code><br /><code>Stream&lt;String&gt; stream = list.stream();</code></td>
</tr>
<tr>
<td><strong>2. 배열에서 생성</strong></td>
<td><code>Arrays.stream()</code>을 사용하여 배열을 스트림으로 변환</td>
<td><code>String[] array = {&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;};</code><br /><code>Stream&lt;String&gt; stream = Arrays.stream(array);</code></td>
</tr>
<tr>
<td><strong>3. Stream 직접 생성</strong></td>
<td><code>Stream.of()</code>를 사용하여 명시적으로 스트림 생성</td>
<td><code>Stream&lt;Integer&gt; stream = Stream.of(1, 2, 3, 4, 5);</code></td>
</tr>
<tr>
<td><strong>4. Stream.generate() 사용</strong></td>
<td>무한 스트림 생성 (ex: 난수)</td>
<td><code>Stream&lt;Double&gt; randomStream = Stream.generate(Math::random).limit(5);</code><br /><code>randomStream.forEach(System.out::println);</code></td>
</tr>
<tr>
<td><strong>5. Stream.iterate() 사용</strong></td>
<td>초기값과 람다식을 이용해 스트림 생성</td>
<td><code>Stream&lt;Integer&gt; iteratedStream = Stream.iterate(1, n -&gt; n + 2).limit(5);</code><br /><code>iteratedStream.forEach(System.out::println);</code></td>
</tr>
</tbody></table>
<blockquote>
<p>즉, System.out::println은 s -&gt; System.out.println(s)의 축약 버전!
📌 forEach(System.out::println) 하면 각 요소를 그대로 출력할 때 유용해! </p>
</blockquote>
<br />

<hr />
<br />



<h3 id="1️⃣-중간-연산-intermediate-operations">1️⃣ 중간 연산 (Intermediate Operations)</h3>
<p>중간 연산은 스트림을 변환하거나 필터링하는 역할을 하며, <strong>최종 연산이 호출되기 전까지 실행되지 않는 지연 연산</strong>입니다.</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
<th>예제</th>
</tr>
</thead>
<tbody><tr>
<td><code>filter(Predicate&lt;T&gt;)</code></td>
<td>조건을 만족하는 요소만 남김</td>
<td><code>list.stream().filter(s -&gt; s.startsWith(&quot;a&quot;))</code></td>
</tr>
<tr>
<td><code>map(Function&lt;T, R&gt;)</code></td>
<td>요소를 변환</td>
<td><code>list.stream().map(String::toUpperCase)</code></td>
</tr>
<tr>
<td><code>flatMap(Function&lt;T, Stream&lt;R&gt;&gt;)</code></td>
<td>중첩 구조를 평탄화</td>
<td><code>list.stream().flatMap(Collection::stream)</code></td>
</tr>
<tr>
<td><code>distinct()</code></td>
<td>중복 제거</td>
<td><code>list.stream().distinct()</code></td>
</tr>
<tr>
<td><code>sorted()</code></td>
<td>기본 정렬</td>
<td><code>list.stream().sorted()</code></td>
</tr>
<tr>
<td><code>sorted(Comparator&lt;T&gt;)</code></td>
<td>사용자 정의 정렬</td>
<td><code>list.stream().sorted(Comparator.reverseOrder())</code></td>
</tr>
<tr>
<td><code>peek(Consumer&lt;T&gt;)</code></td>
<td>요소를 확인 (디버깅 용도)</td>
<td><code>list.stream().peek(System.out::println)</code></td>
</tr>
<tr>
<td><code>limit(long maxSize)</code></td>
<td>개수 제한</td>
<td><code>list.stream().limit(5)</code></td>
</tr>
<tr>
<td><code>skip(long n)</code></td>
<td>처음 n개 요소 건너뜀</td>
<td><code>list.stream().skip(2)</code></td>
</tr>
</tbody></table>
<br />

<hr />
<br />


<h3 id="2️⃣-최종-연산-terminal-operations">2️⃣ 최종 연산 (Terminal Operations)</h3>
<p>최종 연산은 <strong>스트림을 실행하여 결과를 반환</strong>하며, 한 번 실행되면 스트림을 다시 사용할 수 없습니다.</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
<th>예제</th>
</tr>
</thead>
<tbody><tr>
<td><code>forEach(Consumer&lt;T&gt;)</code></td>
<td>각 요소에 대해 동작 수행</td>
<td><code>list.stream().forEach(System.out::println)</code></td>
</tr>
<tr>
<td><code>collect(Collector&lt;T, A, R&gt;)</code></td>
<td>컬렉션으로 변환</td>
<td><code>list.stream().collect(Collectors.toList())</code></td>
</tr>
<tr>
<td><code>count()</code></td>
<td>요소 개수 반환</td>
<td><code>list.stream().count()</code></td>
</tr>
<tr>
<td><code>findFirst()</code></td>
<td>첫 번째 요소 반환</td>
<td><code>list.stream().findFirst()</code></td>
</tr>
<tr>
<td><code>findAny()</code></td>
<td>임의의 요소 반환</td>
<td><code>list.stream().findAny()</code></td>
</tr>
<tr>
<td><code>allMatch(Predicate&lt;T&gt;)</code></td>
<td>모든 요소가 조건을 만족하는지 검사</td>
<td><code>list.stream().allMatch(s -&gt; s.length() &gt; 2)</code></td>
</tr>
<tr>
<td><code>anyMatch(Predicate&lt;T&gt;)</code></td>
<td>하나라도 조건을 만족하는지 검사</td>
<td><code>list.stream().anyMatch(s -&gt; s.startsWith(&quot;a&quot;))</code></td>
</tr>
<tr>
<td><code>noneMatch(Predicate&lt;T&gt;)</code></td>
<td>모든 요소가 조건을 만족하지 않는지 검사</td>
<td><code>list.stream().noneMatch(s -&gt; s.isEmpty())</code></td>
</tr>
<tr>
<td><code>min(Comparator&lt;T&gt;)</code></td>
<td>최소값 반환</td>
<td><code>list.stream().min(Integer::compareTo)</code></td>
</tr>
<tr>
<td><code>max(Comparator&lt;T&gt;)</code></td>
<td>최대값 반환</td>
<td><code>list.stream().max(Integer::compareTo)</code></td>
</tr>
<tr>
<td><code>reduce(BinaryOperator&lt;T&gt;)</code></td>
<td>요소를 하나의 값으로 합침</td>
<td><code>list.stream().reduce((a, b) -&gt; a + b)</code></td>
</tr>
</tbody></table>
<br />


<hr />
<br />

<h4 id="3️⃣-예제-코드">3️⃣ 예제 코드</h4>
<pre><code class="language-java">import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List&lt;String&gt; list = Arrays.asList(&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;, &quot;avocado&quot;);

        // &quot;a&quot;로 시작하는 단어 필터링 후 대문자로 변환
        List&lt;String&gt; result = list.stream()
                                  .filter(s -&gt; s.startsWith(&quot;a&quot;))
                                  .map(String::toUpperCase)
                                  .collect(Collectors.toList());

        System.out.println(result); // [APPLE, AVOCADO]
    }
}</code></pre>
<br />

<p>1) filter와 collect를 이용한 리스트 필터링</p>
<pre><code class="language-java">List&lt;String&gt; list = Arrays.asList(&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;, &quot;avocado&quot;);

List&lt;String&gt; filteredList = list.stream()
    .filter(s -&gt; s.startsWith(&quot;a&quot;))
    .collect(Collectors.toList());

System.out.println(filteredList); // [apple, avocado]</code></pre>
<br />

<p>2) map을 이용한 데이터 변환</p>
<pre><code class="language-java">List&lt;String&gt; list = Arrays.asList(&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;);

List&lt;Integer&gt; lengths = list.stream()
    .map(String::length)
    .collect(Collectors.toList());

System.out.println(lengths); // [5, 6, 6]</code></pre>
<br />

<p>3) sorted()을 이용한 정렬</p>
<pre><code class="language-java">List&lt;Integer&gt; numbers = Arrays.asList(5, 3, 8, 1, 2);

List&lt;Integer&gt; sortedList = numbers.stream()
    .sorted()
    .collect(Collectors.toList());

System.out.println(sortedList); // [1, 2, 3, 5, 8]</code></pre>
<br />

<p>4) reduce()를 이용한 합계 계산</p>
<pre><code class="language-java">List&lt;Integer&gt; numbers = Arrays.asList(1, 2, 3, 4, 5);

int sum = numbers.stream()
    .reduce(0, Integer::sum); // 0은 초기값

System.out.println(sum); // 15</code></pre>
<br />

<p>5) groupingBy()를 이용한 그룹화</p>
<pre><code class="language-java">List&lt;String&gt; list = Arrays.asList(&quot;apple&quot;, &quot;banana&quot;, &quot;avocado&quot;, &quot;blueberry&quot;, &quot;cherry&quot;);

Map&lt;Character, List&lt;String&gt;&gt; groupedByFirstLetter = list.stream()
    .collect(Collectors.groupingBy(s -&gt; s.charAt(0)));

System.out.println(groupedByFirstLetter);

출력결과
{a=[apple, avocado], b=[banana, blueberry], c=[cherry]}</code></pre>
<br />
<br />

<hr />
<br />

<h3 id="은-뭐냐---그것-또한-람다식을-축약한-것">::은 뭐냐?? -&gt; 그것 또한 람다식을 축약한 것</h3>
<blockquote>
<p>개발자들은 귀찮은 걸 싫어함
익명 클래스 람다식으로 축약하고 또 람다식도 귀찮아서 ::로 축약함...대박..
주로 클래스(익명클래스,래퍼클래스)의 내장메서드를 사용할 때 그 람다식을 축약하고 싶어서 사용함</p>
</blockquote>
<p>예를 들자면</p>
<h4 id="integersum의-의미">Integer::sum의 의미</h4>
<br />

<ol>
<li>원래 방식 (일반 메서드 호출)<pre><code class="language-java">int result = Integer.sum(3, 5);
System.out.println(result); // 8</code></pre>
</li>
</ol>
<blockquote>
<p>정적 메서드 직접 호출</p>
</blockquote>
<br />

<ol start="2">
<li>람다식으로 표현<pre><code class="language-java">BinaryOperator&lt;Integer&gt; sumLambda = (a, b) -&gt; Integer.sum(a, b);
System.out.println(sumLambda.apply(3, 5)); // 8</code></pre>
</li>
</ol>
<blockquote>
<p>✔ BinaryOperator&lt;인티저&gt; → (a, b) -&gt; a + b 형태의 함수
✔ apply(3, 5) 호출 시 Integer.sum(3, 5) 실행</p>
</blockquote>
<br />

<ol start="3">
<li>메서드 참조 (::)로 축약<pre><code class="language-java">BinaryOperator&lt;Integer&gt; sumMethodRef = Integer::sum;
System.out.println(sumMethodRef.apply(3, 5)); // 8</code></pre>
</li>
</ol>
<blockquote>
<p>✔ Integer::sum 은 (a, b) -&gt; Integer.sum(a, b) 를 축약한 형태!
✔ 같은 결과지만 코드가 더 간결하고 직관적!</p>
</blockquote>
<br />
<br />
<br />

<h4 id="정리">정리</h4>
<table>
<thead>
<tr>
<th>표현</th>
<th>의미</th>
<th>람다식으로 변환</th>
</tr>
</thead>
<tbody><tr>
<td><code>ClassName::staticMethod</code></td>
<td><strong>클래스의 정적 메서드</strong> 참조</td>
<td><code>(args) -&gt; ClassName.staticMethod(args)</code></td>
</tr>
<tr>
<td><code>object::instanceMethod</code></td>
<td><strong>객체의 인스턴스 메서드</strong> 참조</td>
<td><code>(args) -&gt; object.instanceMethod(args)</code></td>
</tr>
<tr>
<td><code>ClassName::instanceMethod</code></td>
<td><strong>특정 타입의 인스턴스 메서드</strong> 참조</td>
<td><code>(obj, args) -&gt; obj.instanceMethod(args)</code></td>
</tr>
<tr>
<td><code>ClassName::new</code></td>
<td><strong>생성자 참조</strong> (객체 생성)</td>
<td><code>(args) -&gt; new ClassName(args)</code></td>
</tr>
</tbody></table>
<br />
<br />

<ol>
<li>정적 메서드 참조 (ClassName::staticMethod)<pre><code class="language-java">import java.util.function.BinaryOperator;
</code></pre>
</li>
</ol>
<p>public class Main {
    public static void main(String[] args) {
        // 일반 람다식
        BinaryOperator sum1 = (a, b) -&gt; Integer.sum(a, b);</p>
<pre><code>    // 메서드 참조로 축약
    BinaryOperator&lt;Integer&gt; sum2 = Integer::sum;

    System.out.println(sum1.apply(3, 4)); // 7
    System.out.println(sum2.apply(3, 4)); // 7
}</code></pre><p>}</p>
<pre><code>
&gt;Integer::sum 은 (a, b) -&gt; Integer.sum(a, b) 를 축약한 형태!

&lt;br&gt;

2. 인스턴스 메서드 참조 (object::instanceMethod)
```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List&lt;String&gt; words = Arrays.asList(&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;);

        // 일반 람다식
        words.forEach(word -&gt; System.out.println(word));

        // 메서드 참조로 축약
        words.forEach(System.out::println);
    }
}</code></pre><blockquote>
<p>✔ System.out::println 은 (word) -&gt; System.out.println(word) 를 축약한 형태!</p>
</blockquote>
<br />

<ol start="3">
<li>특정 타입의 인스턴스 메서드 참조 (ClassName::instanceMethod)<pre><code class="language-java">import java.util.function.Function;
</code></pre>
</li>
</ol>
<p>public class Main {
    public static void main(String[] args) {
        // 일반 람다식
        Function&lt;String, Integer&gt; strLength1 = s -&gt; s.length();</p>
<pre><code>    // 메서드 참조로 축약
    Function&lt;String, Integer&gt; strLength2 = String::length;

    System.out.println(strLength1.apply(&quot;Hello&quot;)); // 5
    System.out.println(strLength2.apply(&quot;Hello&quot;)); // 5
}</code></pre><p>}</p>
<pre><code>
&gt;✔ String::length 는 (s) -&gt; s.length() 를 축약한 형태!

&lt;br&gt;

 4. 생성자 참조 (ClassName::new)
```java
 import java.util.function.Supplier;
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        // 기본 생성자 호출 (매개변수 없음)
        Supplier&lt;StringBuilder&gt; sb1 = () -&gt; new StringBuilder();
        Supplier&lt;StringBuilder&gt; sb2 = StringBuilder::new; // 축약

        // 매개변수 있는 생성자 호출
        Function&lt;String, Integer&gt; strToInt1 = s -&gt; new Integer(s);
        Function&lt;String, Integer&gt; strToInt2 = Integer::new; // 축약

        System.out.println(sb1.get()); // 빈 StringBuilder 객체
        System.out.println(sb2.get());
        System.out.println(strToInt1.apply(&quot;123&quot;)); // 123
        System.out.println(strToInt2.apply(&quot;123&quot;));
    }
}</code></pre><blockquote>
<p>✔ StringBuilder::new 은 () -&gt; new StringBuilder() 를 축약한 형태!
✔ Integer::new 은 (s) -&gt; new Integer(s) 를 축약한 형태!</p>
</blockquote>
<br />
<br />
<br />

<p>이 블로그도 잘 정리해놓음
헷갈리면 이거 보기
이미지도 여기서 가져옴</p>
<blockquote>
<p><a href="https://hirodevelodiary.tistory.com/entry/Java-Stream%EC%9D%98-%EA%B8%B0%EC%B4%88-%EB%AC%B8%EB%B2%95-%EB%B0%8F-%EC%98%88%EC%8B%9C%EC%BD%94%EB%93%9C">https://hirodevelodiary.tistory.com/entry/Java-Stream%EC%9D%98-%EA%B8%B0%EC%B4%88-%EB%AC%B8%EB%B2%95-%EB%B0%8F-%EC%98%88%EC%8B%9C%EC%BD%94%EB%93%9C</a></p>
</blockquote>