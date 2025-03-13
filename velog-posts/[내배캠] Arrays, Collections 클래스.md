<h2 id="arrays-클래스">Arrays 클래스</h2>
<ul>
<li>java.util 패키지에 포함된 배열을 다루기 위한 유틸리티 클래스입니다.</li>
<li>배열의 정렬, 검색, 비교, 복사, 변환 등 다양한 기능을 제공합니다.</li>
<li>배열을 보다 쉽게 처리할 수 있도록 도와주는 정적(static) 메서드들로 구성되어 있습니다.</li>
</ul>
<h3 id="📚-java-arrays-클래스-주요-메서드-정리">📚 Java <code>Arrays</code> 클래스 주요 메서드 정리</h3>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
<th>사용 예시</th>
</tr>
</thead>
<tbody><tr>
<td><code>Arrays.toString()</code></td>
<td>배열을 문자열로 출력. 보기 좋게 출력할 때 사용.</td>
<td>int[] arr = {1, 2, 3}; System.out.println(Arrays.toString(arr)); // 출력: [1, 2, 3]</td>
</tr>
<tr>
<td><code>Arrays.sort()</code></td>
<td>배열을 오름차순으로 정렬.</td>
<td>int[] arr = {3, 1, 2}; Arrays.sort(arr); System.out.println(Arrays.toString(arr)); // 출력: [1, 2, 3]</td>
</tr>
<tr>
<td><code>Arrays.sort(T[] a, Comparator&lt;? super T&gt; c)</code></td>
<td>사용자 정의 기준으로 배열을 정렬.</td>
<td>String[] strings = {&quot;sun&quot;, &quot;bed&quot;, &quot;car&quot;}; int n = 1; Arrays.sort(strings, (s1, s2) -&gt; { if (s1.charAt(n) == s2.charAt(n)) { return s1.compareTo(s2); } return Character.compare(s1.charAt(n), s2.charAt(n)); }); System.out.println(Arrays.toString(strings)); // 출력: [car, bed, sun]</td>
</tr>
<tr>
<td><code>Arrays.equals()</code></td>
<td>두 배열의 내용을 비교하여 같으면 <code>true</code>, 다르면 <code>false</code> 반환.</td>
<td>int[] arr1 = {1, 2}; int[] arr2 = {1, 2}; System.out.println(Arrays.equals(arr1, arr2)); // 출력: true</td>
</tr>
<tr>
<td><code>Arrays.deepEquals()</code></td>
<td>다차원 배열을 깊은 비교로 동일 여부를 판단.</td>
<td>int[][] arr1 = {{1, 2}}; int[][] arr2 = {{1, 2}}; System.out.println(Arrays.deepEquals(arr1, arr2)); // 출력: true</td>
</tr>
<tr>
<td><code>Arrays.copyOf()</code></td>
<td>배열을 복사하고 새로운 길이로 반환.</td>
<td>int[] arr = {1, 2, 3}; int[] copy = Arrays.copyOf(arr, 2); System.out.println(Arrays.toString(copy)); // 출력: [1, 2]</td>
</tr>
<tr>
<td><code>Arrays.copyOfRange()</code></td>
<td>배열의 특정 범위를 복사.</td>
<td>int[] arr = {1, 2, 3, 4}; int[] copy = Arrays.copyOfRange(arr, 1, 3); System.out.println(Arrays.toString(copy)); // 출력: [2, 3]</td>
</tr>
<tr>
<td><code>Arrays.fill()</code></td>
<td>배열을 특정 값으로 초기화.</td>
<td>int[] arr = new int[3]; Arrays.fill(arr, 5); System.out.println(Arrays.toString(arr)); // 출력: [5, 5, 5]</td>
</tr>
<tr>
<td><code>Arrays.binarySearch()</code></td>
<td>배열에서 이진 탐색으로 값의 인덱스를 반환. 정렬된 배열에서만 사용.</td>
<td>int[] arr = {1, 2, 3}; int index = Arrays.binarySearch(arr, 2); System.out.println(index); // 출력: 1</td>
</tr>
<tr>
<td><code>Arrays.asList()</code></td>
<td>배열을 <code>List</code>로 변환.</td>
<td>String[] array = {&quot;a&quot;, &quot;b&quot;}; List&lt;스트링&gt; list = Arrays.asList(array); System.out.println(list); // 출력: [a, b]</td>
</tr>
<tr>
<td><code>Arrays.stream()</code></td>
<td>배열을 스트림으로 변환하여 함수형 프로그래밍 처리 가능.</td>
<td>int[] arr = {1, 2, 3}; int sum = Arrays.stream(arr).sum(); System.out.println(sum); // 출력: 6</td>
</tr>
<tr>
<td><code>Arrays.deepToString()</code></td>
<td>다차원 배열을 문자열로 출력.</td>
<td>int[][] arr = {{1, 2}, {3, 4}}; System.out.println(Arrays.deepToString(arr)); // 출력: [[1, 2], [3, 4]]</td>
</tr>
</tbody></table>
<hr />
<h4 id="⚠️-사용-시-주의-사항">⚠️ 사용 시 주의 사항</h4>
<ul>
<li><code>Arrays.binarySearch()</code>는 <strong><em>반드시 정렬된 배열</em></strong>에서만 사용해야 올바른 결과가 나옴.</li>
<li><code>Arrays.asList()</code>는 고정된 크기의 리스트를 반환하므로, <code>add()</code>나 <code>remove()</code>는 사용할 수 없음.</li>
<li><code>Arrays.copyOf()</code>와 <code>Arrays.copyOfRange()</code>는 원본 배열을 변경하지 않고 <strong><em>새로운 배열</em></strong>을 반환.</li>
</ul>
<hr />
<br />
<br />

<hr />
<h2 id="collections-클래스란">Collections 클래스란?</h2>
<ul>
<li>Java에서 제공하는 <strong>java.util 패키지`</strong>에 포함된 유틸리티 클래스입니다.</li>
<li><strong>컬렉션(List, Set, Map 등)</strong>을 효율적으로 다룰 수 있도록 다양한 정적(static) 메서드를 제공합니다.</li>
<li>주로 정렬, 검색, 최대/최소값 찾기, 스레드 안전 처리 등을 할 때 사용됩니다.</li>
<li>배열을 다루는 Arrays 클래스와는 다르게, Collections는 List, Set, Map과 같은 컬렉션을 다룹니다.</li>
</ul>
<hr />
<h3 id="📚-java-collections-클래스-주요-메서드-정리">📚 Java <code>Collections</code> 클래스 주요 메서드 정리</h3>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
<th>사용 예시</th>
</tr>
</thead>
<tbody><tr>
<td><code>sort()</code></td>
<td>리스트를 정렬 (오름차순 기본, <code>Comparator</code>로 커스텀 정렬 가능)</td>
<td>List list = Arrays.asList(3, 1, 2); Collections.sort(list); // [1, 2, 3]</td>
</tr>
<tr>
<td><code>reverse()</code></td>
<td>리스트의 순서를 뒤집음</td>
<td>List list = Arrays.asList(1, 2, 3); Collections.reverse(list); // [3, 2, 1]</td>
</tr>
<tr>
<td><code>shuffle()</code></td>
<td>리스트의 순서를 랜덤하게 섞음</td>
<td>List list = Arrays.asList(1, 2, 3); Collections.shuffle(list);</td>
</tr>
<tr>
<td><code>max()</code></td>
<td>컬렉션에서 최대값 반환</td>
<td>List list = Arrays.asList(1, 2, 3); int max = Collections.max(list); // 3</td>
</tr>
<tr>
<td><code>min()</code></td>
<td>컬렉션에서 최소값 반환</td>
<td>List list = Arrays.asList(1, 2, 3); int min = Collections.min(list); // 1</td>
</tr>
<tr>
<td><code>frequency()</code></td>
<td>컬렉션에서 특정 요소가 몇 번 등장하는지 반환</td>
<td>List list = Arrays.asList(&quot;a&quot;, &quot;b&quot;, &quot;a&quot;); int freq = Collections.frequency(list, &quot;a&quot;); // 2</td>
</tr>
<tr>
<td><code>binarySearch()</code></td>
<td>정렬된 리스트에서 이진 탐색으로 요소의 인덱스를 반환</td>
<td>List list = Arrays.asList(1, 2, 3); int index = Collections.binarySearch(list, 2); // 1</td>
</tr>
<tr>
<td><code>fill()</code></td>
<td>리스트의 모든 요소를 특정 값으로 채움</td>
<td>List list = Arrays.asList(&quot;a&quot;, &quot;b&quot;); Collections.fill(list, &quot;z&quot;); // [z, z]</td>
</tr>
<tr>
<td><code>copy()</code></td>
<td>한 리스트의 내용을 다른 리스트에 복사</td>
<td>List src = Arrays.asList(&quot;a&quot;, &quot;b&quot;); List dest = Arrays.asList(&quot;&quot;, &quot;&quot;); Collections.copy(dest, src); // dest = [a, b]</td>
</tr>
<tr>
<td><code>replaceAll()</code></td>
<td>리스트의 특정 값을 다른 값으로 일괄 변경</td>
<td>List list = Arrays.asList(&quot;a&quot;, &quot;b&quot;, &quot;a&quot;); Collections.replaceAll(list, &quot;a&quot;, &quot;z&quot;); // [z, b, z]</td>
</tr>
<tr>
<td><code>nCopies()</code></td>
<td>동일한 요소를 지정된 개수만큼 포함하는 불변 리스트 생성</td>
<td>List list = Collections.nCopies(3, &quot;a&quot;); // [a, a, a]</td>
</tr>
<tr>
<td><code>singletonList()</code></td>
<td>단일 요소만 포함하는 불변 리스트 생성</td>
<td>List list = Collections.singletonList(&quot;a&quot;); // [a]</td>
</tr>
<tr>
<td><code>synchronizedList()</code></td>
<td>스레드 안전한 리스트 생성</td>
<td>List list = Collections.synchronizedList(new ArrayList&lt;&gt;());</td>
</tr>
<tr>
<td><code>unmodifiableList()</code></td>
<td>읽기 전용 불변 리스트 생성</td>
<td>List list = Collections.unmodifiableList(Arrays.asList(&quot;a&quot;, &quot;b&quot;));</td>
</tr>
</tbody></table>