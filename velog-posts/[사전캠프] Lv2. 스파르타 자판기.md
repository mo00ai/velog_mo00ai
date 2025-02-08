<ul>
<li><strong>자바 코드를 이용해 자판기를 만들어 봅시다.</strong></li>
</ul>
<p><img alt="Untitled" src="https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/a9de961c-7751-4fb6-929a-893b1b10631c/Untitled.png" /></p>
<ol>
<li><p><strong>사용자가 볼 수 있게 메뉴를 표시합니다.</strong></p>
<ul>
<li><p>다음과 같은 음료를 실행창에 표시합니다.</p>
<ul>
<li>사이다 1,700원</li>
<li>콜라 1,900원</li>
<li>식혜 2,500원</li>
<li>솔의눈 3,000원</li>
</ul>
</li>
<li><p>힌트1</p>
<p>  맵 자료형을 사용해서 음료 정보를 담아보세요.</p>
<pre><code class="language-java">  Map&lt;String, Integer&gt; beverages = Map.of(
                  &quot;사이다&quot;, 1700,
                  &quot;콜라&quot;, 1900,
                  &quot;식혜&quot;, 2500,
                  &quot;솔의눈&quot;, 3000
          );
</code></pre>
</li>
<li><p>힌트2</p>
<p>  맵의 items 와 for 문을 조합해서 사용해보세요.</p>
<pre><code class="language-java">
  for (Map.Entry&lt;String, Integer&gt; beverage : beverages.entrySet()) {
          // 여기에 System.out.println 문을 적어주세요
  }
</code></pre>
</li>
</ul>
</li>
<li><p><strong>사용자는 음료를 선택할 수 있습니다.</strong> </p>
<ul>
<li><p>사용자에게 어떤 음료를 살 것인지를 입력받습니다.</p>
<ul>
<li>ex) 사이다</li>
<li>목록에 없는 음료일 경우 실행이 종료됩니다.</li>
</ul>
</li>
<li><p>힌트1</p>
<p>  Java  <code>Scanner</code> 클래스를 사용해보세요</p>
<pre><code class="language-java">
  Scanner scanner = new Scanner(System.in);
  String userChoice = scanner.nextLine();
</code></pre>
</li>
<li><p>힌트2</p>
<p>  맵의 <code>keys</code> / <code>keySet</code> 를 사용해보세요.</p>
<pre><code class="language-java">  System.out.println(beverages.keySet());</code></pre>
<pre><code class="language-java">  if (beverages.containsKey(userChoice)) {}</code></pre>
</li>
</ul>
</li>
<li><p><strong>사용자는 지불할 금액을 입력할 수 있습니다.</strong></p>
<ul>
<li><p>사용자에게 얼마를 넣을지 입력받습니다.</p>
<ul>
<li>ex) 2000</li>
<li>지불하는 금액이 선택한 음료의 비용보다 작다면 “돈이 부족합니다.” 를 출력합니다</li>
</ul>
</li>
<li><p>힌트1</p>
<pre><code class="language-java">
  int coin = scanner.nextInt();</code></pre>
</li>
<li><p>힌트2</p>
<pre><code class="language-java">
  System.out.println(beverages.get(&quot;콜라&quot;));
  System.out.println(beverages.get(&quot;사이다&quot;));
  System.out.println(beverages.get(&quot;식혜&quot;));

  String userChoice = &quot;콜라&quot;;
  System.out.println(beverages.get(userChoice));

  if (coin &lt; beverages.get(userChoice)) {
      // 실행 종료하기
      System.out.println(&quot;돈이 부족합니다&quot;);
  } else {
      // 돈이 충분할 경우
  }</code></pre>
</li>
</ul>
</li>
<li><p><strong>사용자는 음료를 구매하고 남은 잔액을 확인할 수 있습니다.</strong></p>
<ul>
<li><p>잔액을 화면에 표시합니다.</p>
<ul>
<li>ex) 입력한 돈 2000원, 사이다 1700원 일때 300원을 잔액으로 보여줍니다.</li>
</ul>
</li>
<li><p>힌트</p>
<pre><code class="language-java">
  int remain = beverages.get(userChoice) - coin
  println(remain)</code></pre>
</li>
</ul>
</li>
</ol>
<br />
<br />
<br />

<hr />
<br />
<br />

<h3 id="내-답">내 답</h3>
<pre><code class="language-java">package quest;

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class quest2 {

    static Map&lt;String, Integer&gt; map = new HashMap&lt;&gt;();
    static String beverage;
    static int coin;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        map.put(&quot;사이다&quot;, 1700);
        map.put(&quot;콜라&quot;, 1900);
        map.put(&quot;식혜&quot;, 2500);
        map.put(&quot;솔의눈&quot;, 3000);

        Menu();
        beverage = scanner.nextLine();

        if (map.containsKey(beverage)) {
            System.out.println(map.get(beverage));
            System.out.println(&quot;얼마를 넣겠습니까&quot;);
            coin = scanner.nextInt();
            if(coin &lt; map.get(beverage)) {
                System.out.println(&quot;돈이 부족합니다&quot;);
            } else {
                int result = map.get(beverage) - coin;
                System.out.println(&quot;거스름돈은 &quot; + result + &quot;원입니다.&quot;);
            }
        } else {
            System.out.println();
            System.out.println(&quot;그런 음료는 없습니다.&quot;);
            System.out.println(&quot;다시 작성해주세요.&quot;);
            Menu();
            beverage = scanner.nextLine();
        }


    }


    public static void Menu() {
        System.out.println(&quot;------자판기------&quot;);
        for (Map.Entry&lt;String, Integer&gt; entry : map.entrySet()) {
            System.out.println(entry.getKey() + &quot; : &quot; + entry.getValue() + &quot;원&quot;);
        }
        System.out.println(&quot;-----------------&quot;);
        System.out.println();
        System.out.println(&quot;원하는 음료를 작성해주세요.&quot;);

    }
}
</code></pre>
<br />

<p>피드백</p>
<blockquote>
<p>우선 메뉴 화면 출력은 따로 메서드로 빼서 호출하면 쓸 수 있도록 했다
정상 작동하지만 문제점은 사용자가 음료를 잘못 작성했을 경우, 메뉴를 보여주고 다시 map에 사용자가 재입력한 문자가 포함되는지를 확인해야한다.
gpt에게 조언을 구해보니 사용자가 제대로 된 음료를 적을 때까지 반복문을 돌리라고해서 그 조언을 바탕으로 다시 코드를 짜보기로 한다.</p>
</blockquote>
<br />
<br />

<hr />
<br />

<h3 id="새-코드">새 코드</h3>
<pre><code class="language-java">package quest;

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class quest2 {

    static Map&lt;String, Integer&gt; map = new HashMap&lt;&gt;();
    static String beverage;
    static int coin;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        map.put(&quot;사이다&quot;, 1700);
        map.put(&quot;콜라&quot;, 1900);
        map.put(&quot;식혜&quot;, 2500);
        map.put(&quot;솔의눈&quot;, 3000);

        Menu();
        beverage = scanner.nextLine();

        while (true) {
            if(map.containsKey(beverage)) {
                break;
            } else {
                System.out.println();
                System.out.println(&quot;그런 음료는 없습니다.&quot;);
                System.out.println(&quot;다시 작성해주세요.&quot;);
                Menu();
                beverage = scanner.nextLine();
            }
        }

        System.out.println(beverage+&quot;는 &quot; + map.get(beverage)+&quot;원입니다.&quot;);
        System.out.println(&quot;얼마를 넣겠습니까&quot;);
        coin = scanner.nextInt();
        if(coin &lt; map.get(beverage)) {
            System.out.println(&quot;돈이 부족합니다&quot;);
        } else {
            int result = map.get(beverage) - coin;
            System.out.println(&quot;거스름돈은 &quot; + result + &quot;원입니다.&quot;);
        }


    }


    public static void Menu() {
        System.out.println(&quot;------자판기------&quot;);
        for (Map.Entry&lt;String, Integer&gt; entry : map.entrySet()) {
            System.out.println(entry.getKey() + &quot; : &quot; + entry.getValue() + &quot;원&quot;);
        }
        System.out.println(&quot;-----------------&quot;);
        System.out.println();
        System.out.println(&quot;원하는 음료를 작성해주세요.&quot;);

    }
}
</code></pre>
<blockquote>
<ol>
<li>while 반복문과 break;를 통해 정상으로 처리 됐을 시엔 반복문을 빠져나와 나머지 로직을 수행함</li>
<li>아닐 경우엔 올바른 답을 작성할 때까지 음료 작성을 반복함</li>
</ol>
</blockquote>
<blockquote>
<p>배운 점</p>
</blockquote>
<ol>
<li>map 활용</li>
</ol>
<ul>
<li>Map &lt;String, Integer&gt; 변수명  = new HashMap&lt;&gt;();</li>
<li>map.containsKey(키 이름); -&gt; ArrayList.contains와 같이 배열 내 값이 있는지 확인</li>
<li>Map으로 for( : ) 반복문을 수행하고 싶을 때 사용 하는 메서드
  -for (Map.Entry&lt;String, Integer&gt; entry : map.entrySet()) {</li>
<li>map의 key값으로 value값 가져오기<ul>
<li>map.get(키값) = value</li>
</ul>
</li>
</ul>
<br />

<blockquote>
<p>부족한 점</p>
</blockquote>
<ul>
<li>static public private 개념 없음</li>
<li>반복문 구조 </li>
<li>메소드 호출 구조</li>
</ul>