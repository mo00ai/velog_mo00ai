<h3 id="쓰레드">쓰레드</h3>
<ul>
<li><code>쓰레드</code>는 프로그램 내에서 독립적으로 실행되는 하나의 작업 단위입니다.(한 명의 일꾼)</li>
<li><code>싱글 쓰레드</code> 는 한 번에 하나의 작업만 처리하지만 <code>멀티쓰레드</code>는 여러 작업을 동시에 처리할 수 있습니다.</li>
<li><code>멀티 쓰레드</code>를 활용하면 여러 작업을 병렬로 수행할 수 있어 처리 성능을 향상시킬 수 있습니다.</li>
</ul>
<br />
<br />

<hr />
<br />

<h3 id="싱글-쓰레드single-thread">싱글 쓰레드(Single Thread)</h3>
<p><strong>싱글 쓰레드 예시를 살펴봅시다.</strong></p>
<ul>
<li><code>싱글 쓰레드</code>는 <strong>한 명의 일꾼이 작업을 처리</strong>하는 것과 같습니다.</li>
<li>일꾼이 한 명이기 때문에 여러 개의 작업이 있다면 순차적으로 처리해야 합니다.</li>
<li><code>main()</code> 메서드는 프로그램 시작과 동시에 생성되는 하나의 쓰레드입니다.</li>
<li>아래 코드는 <code>main()</code>  메서드 하나의 쓰레드가 작업을 처리하는 예시입니다.</li>
</ul>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {
        System.out.println(&quot;::: main 쓰레드 시작 :::&quot;);
        String threadName = Thread.currentThread().getName();

        // ✅ 하나의 작업 단위: 숫자를 0 부터 9 까지 출력
        for (int i = 0; i &lt; 10; i++) {
            System.out.println(&quot;현재 쓰레드: &quot; + threadName + &quot; - &quot; + i);
            try {
                Thread.sleep(500); // 0.5 초 대기
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        // ✅ 추가작업
        for (int i = 0; i &lt; 10; i++) {
            System.out.println(&quot;현재 쓰레드: &quot; + threadName + &quot; - &quot; + i);
            try {
                Thread.sleep(500); // 0.5 초 대기
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println(&quot;::: 작업 끝 :::&quot;);
    }
}</code></pre>
<br />

<hr />
<br />

<h3 id="멀티-쓰레드multi-thread-와-쓰레드-구현">멀티 쓰레드(Multi-Thread) 와 쓰레드 구현</h3>
<p><strong>멀티쓰레드 예시를 살펴봅시다.</strong></p>
<ul>
<li><code>멀티쓰레드</code>는 작업을 처리할 수 있는 여러 명의 일꾼을 의미합니다.</li>
<li>멀티 쓰레드를 활용해서 여러 작업(0 ~9 출력)을 병렬(동시)로 처리할 수 있습니다.</li>
<li><code>Thread</code> 클래스를 상속받아 <code>쓰레드</code>를 구현할 수 있습니다.</li>
<li><code>Thread.run()</code> 메서드를 오버라이드 해서 <code>쓰레드</code>가 수행할 작업을 정의할 수 있습니다.</li>
<li><code>start()</code> 메서드를 호출하면 새로운 쓰레드가 생성되고 <code>run()</code> 의 작업 내용이 실행됩니다.</li>
<li><strong>총 세 개의 쓰레드(<code>main</code>, <code>thread0</code>, <code>thread1</code>) <code>병렬</code>로 실행됩니다.</strong></li>
<li><code>main</code> 쓰레드는 <code>thread0</code>, <code>thread1</code> 을 생성하고 실행시킵니다.</li>
<li>생성된 <strong><code>thread0</code>, <code>thread1</code></strong> 는 0.5초마다 0 ~ 9까지 숫자를 출력합니다.</li>
</ul>
<p>쓰레드를 실행시킬 때 꼭 <code>start()</code> 를 사용하세요!</p>
<ul>
<li><code>start()</code>는 <strong>새로운 쓰레드에서 <code>run()</code>을 실행</strong>하지만 <code>run()</code>을 직접 호출하면 <strong>현재 쓰레드에서 실행</strong>됩니다.</li>
</ul>
<br />

<pre><code class="language-java">// ✅ Thread 클래스 상속으로 쓰레드 구현
public class MyThread extends Thread {

    @Override
    public void run() {
        String threadName = Thread.currentThread().getName();
        System.out.println(&quot;::: &quot; + threadName + &quot;쓰레드 시작 :::&quot;);
        for (int i = 0; i &lt; 10; i++) {
            System.out.println(&quot;현재 쓰레드: &quot; + threadName + &quot; - &quot; + i);
            try {
                Thread.sleep(500); // 딜레이 0.5 초
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println(&quot;::: &quot; + threadName + &quot;쓰레드 종료 :::&quot;);
    }
}</code></pre>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {
        System.out.println(&quot;::: main 쓰레드 시작&quot;);

        MyThread thread0 = new MyThread();
        MyThread thread1 = new MyThread();

        // 1. thread0 실행
        System.out.println(&quot;::: main 이 thread0 을 실행&quot;);
        thread0.start();

        // 2. thread1 실행
        System.out.println(&quot;::: main 이 thread1 을 실행&quot;);
        thread1.start();

        System.out.println(&quot;::: main 쓰레드 종료&quot;);
    }
}</code></pre>
<br />

<hr />
<br />

<h3 id="join---특정-쓰레드가-끝날-때까지-기다리기">join() - 특정 쓰레드가 끝날 때까지 기다리기</h3>
<p><strong><code>join()</code> 을 학습해 봅시다.</strong></p>
<ul>
<li><code>join()</code> 은 <code>main()</code> 쓰레드가 다른 쓰레드가 종료될 때까지 기다리게 하는 메서드입니다.</li>
<li><code>join()</code> 을 호출한 쓰레드가 끝날 때까지 <code>main()</code> 쓰레드가 대기합니다.</li>
<li><code>main()</code> 쓰레드가 너무 빨리 끝나지 않고 모든 작업이 완료된 후 종료되도록 할 때 유용합니다.
→ 응용하면 <code>main()</code> 쓰레드가 총 작업 완료 시간을 측정할 수 있게 만들 수 있습니다.</li>
<li>아래의 두 개의 쓰레드(<code>thread0</code>, <code>thread1</code>) 가 실행되고 끝날 때까지 <code>main()</code> 이 기다립니다.</li>
<li>모든 작업이 완료되면 <code>main()</code> 은 종료됩니다.</li>
</ul>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {
        System.out.println(&quot;::: main 쓰레드 시작&quot;);
        MyThread thread0 = new MyThread();
        MyThread thread1 = new MyThread();

        // 시작시간 기록
        long startTime = System.currentTimeMillis();

        // 1. thread0 시작
        System.out.println(&quot;thread0 시작&quot;);
        thread0.start();

        // 2. thread1 시작
        System.out.println(&quot;thread1 시작&quot;);
        thread1.start();

        // ⌛️ main 쓰레드 대기 시키기
        try {
            thread0.join();
            thread1.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        long endTime = System.currentTimeMillis();
        long totalTime = endTime - startTime;
        System.out.println(&quot;총 작업 시간: &quot; + totalTime + &quot;ms&quot;);
        System.out.println(&quot;::: main 쓰레드 종료&quot;);
    }
}</code></pre>
<br />
<br />

<hr />
<br />

<h3 id="runnable-인터페이스-활용권장">Runnable 인터페이스 활용(권장)</h3>
<p><strong><code>Runnalbe</code> 인터페이스를 활용해 쓰레드를 구현하는 것을 권장합니다.</strong></p>
<aside>
1️⃣
**유지 보수성과 재사용성 향상**

</aside>

<aside>
2️⃣
확장 가능성

</aside>

<br />

<p>1️⃣ <strong><em>유지 보수성과 재사용성 향상됩니다.</em></strong></p>
<ul>
<li><p><code>Thread</code> 는 <strong>쓰레드를 제어하기 위해 존재</strong>하는 클래스입니다.</p>
</li>
<li><p><code>Thread</code> 클래스를 상속받아 <code>MyThread</code>를 구현하면 <code>실행 로직</code>과 <code>쓰레드 제어 로직</code>이 결합되어 <strong>한 가지 클래스에서 두 가지 역할을 담당</strong>하게 됩니다.</p>
<p>  →  쓰레드 제어 로직: <code>start()</code> , <code>join()</code> , <code>isAlive()</code> 등</p>
<p>  → 실행 로직: 숫자 0 ~ 9 출력</p>
<p>  → 하나의 클래스는 하나의 책임만 가지는 것이 유지 보수에 좋습니다.</p>
</li>
<li><p><code>Runnable</code> 을 활용하면 <strong>실행 로직을 별도의 구현체로 분리</strong>할 수 있습니다.</p>
<p>  → <code>Thread</code>는 쓰레드를 제어하는 역할.</p>
<p>  → <code>Runnable 구현체</code> 는 실행 로직을 관리.</p>
</li>
</ul>
<pre><code class="language-java">// ⚠️ Thread는 Thread 제어 역할 그리고 실행로직 두가지를 담당합니다.
public class MyThread extends Thread {

    @Override
    public void run() {
        String threadName = Thread.currentThread().getName();
        System.out.println(&quot;현재 시작된 쓰레드: &quot; + threadName);

        for(int i = 0; i &lt; 10; i++) {
            System.out.println(&quot;현재 쓰레드 : &quot; + threadName + &quot; - &quot; + i);
            try {
                Thread.sleep(500); // 딜레이 0.5 초
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println(&quot;종료된 쓰레드: &quot; + threadName);
    }
}</code></pre>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        MyRunnable task = new MyRunnable(); // ✅ 하나의 작업 객체 선언

                // ✅ 하나의 작업을 여러 쓰레드에서 공유
        Thread thread0 = new Thread(task); // 작업 객체 공유
        Thread thread1 = new Thread(task); // 작업 객체 공유

                // 실행
        thread0.start();
        thread1.start();
    }
}</code></pre>
<br />

<p>2️⃣ <strong><em>기존 클래스를 유지하면서 확장 가능</em></strong></p>
<ul>
<li><p><code>Thread</code> 를 상속해서 <code>MyThread</code> 를 구현하면 다른 클래스를 상속받지 못합니다.</p>
<p>  → Java는 클래스의 다중 상속을 지원하지 않습니다.</p>
<p>  → <code>Thread</code>  를 상속하면 다른 클래스를 상속할 수 없어서 확장성이 떨어집니다.</p>
</li>
<li><p><code>Runnable</code> 은 인터페이스이므로 기존 클래스의 기능을 유지하면서 상속을 통해 확장할 수 있습니다.</p>
</li>
</ul>
<pre><code class="language-java">public class MyNewClass { // ✅ 새로운 클래스 

    public void printMessage() {
        System.out.println(&quot;MyClass 기능 실행&quot;);
    }
}</code></pre>
<pre><code class="language-java">public class MyThread extends Thread, MyNewClass{ // ❌ 다중 상속 불가
        ...
}</code></pre>
<pre><code class="language-java">public class MyRunnable extends MyNewClass implements Runnable { // ✅ 다중 상속

    @Override
    public void run() {
        String threadName = Thread.currentThread().getName();
        for (int i = 0; i &lt; 10; i++) {
            System.out.println(&quot;현재 쓰레드: &quot; + threadName + &quot; - &quot; + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
</code></pre>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        MyRunnable task = new MyRunnable();

        // ✅ 기존 클래스를 유지하면서 확장해서 활용
        task.printMessage(); 

        Thread thread0 = new Thread(task);
        Thread thread1 = new Thread(task);

        thread0.start();
        thread1.start();
    }
}</code></pre>