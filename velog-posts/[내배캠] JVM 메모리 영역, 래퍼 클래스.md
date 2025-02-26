<h3 id="jvm-메모리-영역">JVM 메모리 영역</h3>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/522f8a21-2512-4cb5-a2fb-761199f62117/image.png" /></p>
<ul>
<li><code>Method Area</code>(도서관 비유)<ul>
<li>프로그램 시작 시 정보가 저장됩니다.</li>
<li>클래스 정보(<code>.class 파일</code>) 가 올라가는 곳.</li>
<li>클래스의 메서드 정보, static 변수 등이 저장됩니다.</li>
<li>모든 객체가 공유하는 공용 공간</li>
</ul>
</li>
<li><code>Stack Area</code>(접시 쌓기 비유)<ul>
<li>가장 위에 있는 접시를 먼저 꺼내듯 비슷한 구조로 생각하시면 됩니다.</li>
<li>선입후출(LIFO) 구조 입니다. 먼저 들어온 것이 가장 늦게 나간다는 뜻입니다.</li>
<li>메서드가 호출될 때마다 새로운 접시한장(스택프레임)이 쌓입니다.</li>
<li>가장 위의 접시(최근 호출된 메서드)가 먼저 실행됩니다.</li>
<li>메서드 실행이 끝나면 스택에서 제거됩니다.</li>
<li>메서드 내에 선언된 지역변수들도 저장됨</li>
</ul>
</li>
<li><code>Heap Area</code>(풍선 비유)<ul>
<li><code>new</code> 키워드로 생성된 객체가 저장되는 곳입니다.</li>
<li>객체의 실제 데이터가 저장되고 데이터의 주소는 <code>stack</code> 영역에 저장됩니다.</li>
</ul>
</li>
</ul>
<br />

<hr />
<br />

<h3 id="래퍼-클래스">래퍼 클래스</h3>
<ul>
<li><code>기본자료형</code> 을 객체로 감싸는 클래스입니다.</li>
</ul>
<table>
<thead>
<tr>
<th><strong>기본 자료형 (Primitive Type)</strong></th>
<th><strong>래퍼 클래스 (Wrapper Class)</strong></th>
</tr>
</thead>
<tbody><tr>
<td><code>byte</code></td>
<td><code>Byte</code></td>
</tr>
<tr>
<td><code>short</code></td>
<td><code>Short</code></td>
</tr>
<tr>
<td><code>int</code></td>
<td><code>Integer</code></td>
</tr>
<tr>
<td><code>long</code></td>
<td><code>Long</code></td>
</tr>
<tr>
<td><code>float</code></td>
<td><code>Float</code></td>
</tr>
<tr>
<td><code>double</code></td>
<td><code>Double</code></td>
</tr>
<tr>
<td><code>char</code></td>
<td><code>Character</code></td>
</tr>
<tr>
<td><code>boolean</code></td>
<td><code>Boolean</code></td>
</tr>
</tbody></table>
<br />

<p>참조형</p>
<ul>
<li>변수에 객체가 담기면 해당 변수를 <code>참조형변수</code>라고 말합니다.</li>
<li>참조형 변수는 데이터가 저장된 메모리 주소를 가리킵니다. 
→ <code>Heap</code> 메모리 주소</li>
<li>객체 데이터는 <code>Heap</code> 영역에 저장되어 있기 때문입니다.</li>
<li><code>객체</code>, <code>배열</code>등이 참조형에 속합니다.</li>
</ul>
<blockquote>
<p>래퍼클래스 -&gt; 참조형 변수 -&gt; 객체!!</p>
</blockquote>
<br />

<pre><code>Integer num = 100;
System.out.println(num); // 출력 100</code></pre><p>그냥 출력해도 상관없음 내부에서 toString 처리 해주기 때문임</p>
<br />

<p>래퍼 클래스 사용 이유</p>
<ul>
<li>기본형은 객체처럼 속성, 기능을 가질 수 없습니다.</li>
<li>하지만 객체는 기능을 제공할 수 있습니다.</li>
<li>기본형을 감싼 객체를 만들어 기능을 제공하면 편리하게 데이터처리를 할 수 있습니다.<pre><code>Integer num = 123; // 래퍼클래스
String str = num.toString(); // ✅ 편리한 기능
</code></pre></li>
</ul>
<p>int a = 100; // 그냥 데이터 100
String str = a.toString(); // ❌ 변환 불가</p>
<pre><code>&lt;br&gt;
&lt;br&gt;

오토박싱
- `Integer`는 참조형(객체)이지만 기본형 `int` 값을 직접 대입할 수 있습니다.
- 내부적으로 컴파일러가 자동으로 `Integer.valueOf(10)`을 호출하여 객체를 생성하기 때문입니다.</code></pre><p>Integer num3 = 10; // ✅ 오토박싱
// ✅ 내부적 자동 처리(래퍼형 &lt;- 기본형)
Integer num = Integer.valueOf(10);</p>
<pre><code>&lt;br&gt;

오토 언박싱
래퍼형 → 기본형으로 변환하는 과정으로 오토언박싱
- `num`은 `Integer` 객체(참조형변수)지만 기본형 `int` 변수에 대입할 수 있습니다.
- 내부적으로 컴파일러가 자동으로 `num.intValue()`를 호출하여 기본형으로 변환하기 때문입니다.</code></pre><p>Integer num3 = 10; 
int num = num3;   // ✅ 오토 언박싱</p>
<p>// ✅ 내부적 자동처리(기본형 &lt;- 래퍼형)
int a = num.intValue();</p>
<p>```</p>
<br />
<br />

<p>단점 : 객체에서 추가작업 후 값을 꺼내기 때문에 속도가 느림
빠른 작업이 필요한 경우엔 기본형(int)활용하셈</p>