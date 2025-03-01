<h3 id="불변객체-가변객체">불변객체, 가변객체</h3>
<p><strong><em>String</em></strong></p>
<ul>
<li>불변객체</li>
<li>String은 기본형(int,boolean)이 아니라 <code>객체(참조)</code> 이다.</li>
<li>메모리를 효율적으로 사용하기 위해서</li>
<li>한 번 생성하면 변경할 수 없음. </li>
</ul>
<pre><code class="language-java">String str1 = &quot;Hello &quot;;
String str2 = &quot;Java&quot;;
str1 += str2;

System.out.println(str1); //&quot;Hello Java&quot;</code></pre>
<ul>
<li>이런 식으로 2개의 String객체가 있을 때, str1 + str2와 같은 연산을 하게 되면 새로운 String을 생성하는 것을 알 수 있다.</li>
</ul>
<p>-String은 소위 불변(immutable) 객체라고 한다. 즉, String 객체는 한 번 생성되면 변경할 수 없다. 위와 같이 + 연산자를 사용하여 문자열을 연결하면, 연결할 때마다 새로운 문자열 객체가 생성된다는 것을 의미한다. 또한 이전에 있던 문자열은 JVM의 GC가 처리하게 된다.</p>
<p>따라서, String 객체와 String 객체를 더하는 행위는 메모리 할당과 메모리 해제를 발생시키며 더하는 연산이 많아진다면 성능적으로 좋지 않다.</p>
<blockquote>
<p>int a=1; int b=2; a +=b 하면 a=3으로 변하고 걍 a값이 변경되는건데
String은 객체이기 때문에 새로운 Hello Java라는 객체가 생성됨</p>
</blockquote>
<blockquote>
<p>이는 메모리 낭비를 자아냄</p>
</blockquote>
<br />
<br />

<h3 id="stringbuilder">StringBuilder</h3>
<ul>
<li>스트링빌더는 이런 문자열 연산이 나타날 때, 새로운 문자열 객체를 만드는 것이 아니라 원본 문자열 객체를 <strong><em>수정</em></strong> 하기 때문에 메모리 낭비가 발생하지 않음!</li>
</ul>
<blockquote>
<p>그래서 문자열을 자주 변경해야 할 때는 String이 아니라 StringBuilder나 StringBuffer를 사용해야함</p>
</blockquote>
<br />
<br />

<h4 id="주요-사용-메서드">주요 사용 메서드</h4>
<br />

<p>생성자</p>
<pre><code class="language-java">//생성자
StringBuilder sb = new StringBuilder();

// int 타입의 값으로 빌더의 사이즈를 정ㅇ함
StringBuilder sb = new StringBuilder(20);

//String 문자열을 인자로 하는 생성자
StringBuilder sb = new StringBuilder(&quot;aaa&quot;);</code></pre>
<br />

<p>주요 메서드</p>
<pre><code class="language-java">//문자열 추가
StringBuilder sb = new StringBuilder();
sb.append(&quot;abc&quot;);
sb.append(4).append(&quot;\n&quot;);

//offset위치에 str추가
sb.insert(int offset, String str);
sb.insert(2, &quot;ccc&quot;)

//index1, index2 -&gt; 숫자 범위 위치에 있는 문자열을 str로 대체
sb.replace(int index1, int index2, String str);
sb.replace(3, 6, &quot;hi&quot;)

//인덱싱
//파라미터가 하나라면? 해당 인덱스부터 끝까지 인덱싱
//두 개라면? start부터 end-1까지 인덱싱
sb.substring(int start);
sb.substring(int start, int end);
sb.substring(5);
sb.substring(3, 7)

//인덱스 위치의 문자 하나 삭제
sb.deleteCharAt(int index);
sb.deleteCharAt(3);

//start부터 end-1까지 문자 삭제
sb.delete(int start, int end);
sb.delete(3, sb.length());

//String으로 변환
sb.toString();</code></pre>
<blockquote>
<p>이런식으로 문자열을 조작함</p>
</blockquote>
<br />
<br />

<hr />
<br />

<h3 id="stringbuilder-vs-stringbuffer">StringBuilder vs StringBuffer</h3>
<h1 id="✅-stringbuffer-vs-stringbuilder-차이점">✅ StringBuffer vs StringBuilder 차이점</h1>
<table>
<thead>
<tr>
<th>특징</th>
<th>StringBuffer</th>
<th>StringBuilder</th>
</tr>
</thead>
<tbody><tr>
<td><strong>가변성</strong></td>
<td>✅ (O)</td>
<td>✅ (O)</td>
</tr>
<tr>
<td><strong>스레드 안전(Thread-safe)</strong></td>
<td>✅ (O) (동기화 지원)</td>
<td>❌ (X) (비동기)</td>
</tr>
<tr>
<td><strong>속도</strong></td>
<td>느림 (동기화로 인해)</td>
<td>빠름 (동기화 없음)</td>
</tr>
<tr>
<td><strong>사용 추천</strong></td>
<td>멀티스레드 환경</td>
<td>단일 스레드 환경</td>
</tr>
</tbody></table>
<hr />
<h2 id="🔹-정리">🔹 정리</h2>
<p>✔ <strong>멀티스레드 환경</strong>에서는 <code>StringBuffer</code><br />✔ <strong>싱글스레드 환경</strong>에서는 <code>StringBuilder</code>  </p>
<br />

<blockquote>
<p>참고
<a href="https://myeongju00.tistory.com/61">https://myeongju00.tistory.com/61</a></p>
</blockquote>