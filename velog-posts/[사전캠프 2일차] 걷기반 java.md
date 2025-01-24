<h2 id="걷기반-java--과제">걷기반 java  과제</h2>
<br />


<h3 id="반복문-연습하기-part-1">반복문 연습하기 Part 1</h3>
<h4 id="1-1부터-100까지의-숫자-출력하기">1. 1부터 100까지의 숫자 출력하기</h4>
<pre><code class="language-java">import java.util.*;
import java.lang.*;
import java.io.*;

// The main method must be in a class named &quot;Main&quot;.
class Main {
    public static void main(String[] args) {


        for(int i=1; i&lt;=100; i++) {
             System.out.println(i);
        }

        int i = 1;

        while(i&lt;=100) {
            System.out.println(i);
            i++;
        }

        do {
            System.out.println(i);
            i++;
        } while(i&lt;=100);

    }
}</code></pre>
<hr />
<h3 id="반복문-연습하기-part-2">반복문 연습하기 Part 2</h3>
<h4 id="1부터-100까지의-짝수만-출력하기">1부터 100까지의 짝수만 출력하기</h4>
<p>반복문을 사용하여 1부터 100까지의 숫자 중 짝수만 출력하세요.</p>
<pre><code class="language-java">import java.util.*;
import java.lang.*;
import java.io.*;

// The main method must be in a class named &quot;Main&quot;.
class Main {
    public static void main(String[] args) {

        for (int i=1; i&lt;=100; i++) {
            if (i%2==0) {
                System.out.println(i);
            } else {
                continue;
            }
        }

    }
}</code></pre>
<blockquote>
<p>처음에 continue 대신 return을 썼더니 작동이 안됐음 
return -&gt; 함수 종료가 아니라 포함된 메서드 종료
그리고 else 안 적고 if문만 적어도 됨</p>
</blockquote>
<blockquote>
<p><code>return</code>: 메서드 전체 종료 (반복문 포함).
<code>break</code>: 현재 반복문만 종료 (메서드는 계속 실행).
<code>continue</code>: 현재 반복을 건너뛰고 다음 반복으로 진행.</p>
</blockquote>
<pre><code class="language-java">import java.util.*;
import java.lang.*;
import java.io.*;

// The main method must be in a class named &quot;Main&quot;.
class Main {
    public static void main(String[] args) {

        int i = 1;
        while (i&lt;=100) {
            if (i%2==0) {
                System.out.println(i);
            } 
            i++;
        }

    }
}</code></pre>
<hr />
<h3 id="반복문-연습하기-part-3">반복문 연습하기 Part 3</h3>
<h4 id="구구단-출력하기">구구단 출력하기</h4>
<ul>
<li>2단부터 9단까지의 구구단을 출력하세요.</li>
<li>힌트 : 중첩 반복문</li>
</ul>
<pre><code class="language-java">import java.util.*;
import java.lang.*;
import java.io.*;

// The main method must be in a class named &quot;Main&quot;.
class Main {
    public static void main(String[] args) {

    for (int i=2; i&lt;=9; i++) {

        System.out.println(&quot;------&quot;+i+&quot;단------&quot;);

        for (int j=1; j&lt;=9; j++) {
            int result = 0;
            result = i * j;
            System.out.println(i+&quot; x &quot;+j+&quot; = &quot;+result);
        }
    }

    }
}</code></pre>
<p>결과</p>
<pre><code>------2단------
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
2 x 4 = 8
2 x 5 = 10
2 x 6 = 12
2 x 7 = 14
2 x 8 = 16
2 x 9 = 18
------3단------
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
3 x 4 = 12
3 x 5 = 15
3 x 6 = 18
3 x 7 = 21
3 x 8 = 24
3 x 9 = 27
------4단------
4 x 1 = 4
4 x 2 = 8
4 x 3 = 12
4 x 4 = 16
4 x 5 = 20
4 x 6 = 24
4 x 7 = 28
4 x 8 = 32
4 x 9 = 36
------5단------
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
------6단------
6 x 1 = 6
6 x 2 = 12
6 x 3 = 18
6 x 4 = 24
6 x 5 = 30
6 x 6 = 36
6 x 7 = 42
6 x 8 = 48
6 x 9 = 54
------7단------
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
7 x 6 = 42
7 x 7 = 49
7 x 8 = 56
7 x 9 = 63
------8단------
8 x 1 = 8
8 x 2 = 16
8 x 3 = 24
8 x 4 = 32
8 x 5 = 40
8 x 6 = 48
8 x 7 = 56
8 x 8 = 64
8 x 9 = 72
------9단------
9 x 1 = 9
9 x 2 = 18
9 x 3 = 27
9 x 4 = 36
9 x 5 = 45
9 x 6 = 54
9 x 7 = 63
9 x 8 = 72
9 x 9 = 81
</code></pre><blockquote>
<h4 id="소감">소감</h4>
<p>예전엔 어려워서 손도 못대고 머리 끙끙 싸맸던 구구단을 몇 분만에 해결했다.. 감회가 새로움
근데 아직도 변수 초기화 위치는 헷갈린다 반복문+조건문 알고리즘 문제 해결 경험을 a많이 쌓아야겠다는 생각이 들었다.</p>
</blockquote>
<br />

<hr />
<br />