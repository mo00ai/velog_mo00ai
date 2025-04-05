<h2 id="캐시">캐시</h2>
<p><code>캐시</code>의 사전적 의미</p>
<ul>
<li>물건을 임시적으로 저장,보관하기 위해 사용하는 곳</li>
</ul>
<p><code>캐시</code>의 기술적 의미</p>
<ul>
<li>자주 필요한 데이터나 값의 복사본을 일시적으로 저장, 보관하기 위해 사용하는 곳</li>
</ul>
<p><code>캐싱</code> (Cahching) == Cache + ing</p>
<ul>
<li>캐시를 사용하는 것을 <code>캐싱</code>이라 한다.</li>
</ul>
<hr />
<br />

<hr />
<h2 id="컴퓨터-동작흐름">컴퓨터 동작흐름</h2>
<p><code>**CPU**</code> &lt;-&gt; <code>**RAM**</code> &lt;-&gt; <code>**Hard Drive**</code></p>
<p><code>RAM</code>은 하드 디스크에서 데이터를 불러오고,
<code>CPU</code>는 <code>RAM</code>에 저장되어있는 데이터를 이용하여 연산작업을 수행함</p>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/daaa607b-ef5a-4f45-89cb-a94ebf9b1309/image.png" /></p>
<p><strong><code>CPU</code>와 <code>RAM</code>의 성능차이</strong>
-눈에 띄는 속도로 성장하는 CPU와 그에 반해 더디게 성장하는 RAM 성능
    - 메모리는 속도보다 메모리 자체 용량을 늘리는 것이 주 목표이기 때문</p>
<p>이로 인해,</p>
<ul>
<li>CPU는 데이터 처리를 위해 메모리와 끊임없이 데이터를 주고 받는 구조인데</li>
<li>메모리가 CPU의 데이터 처리 속도를 따라가지 못함
  ➡️ CPU가 메모리를 기다려야 하는 <code>병목현상</code> 발생</li>
</ul>
<blockquote>
<p>따라서, 이 <code>병목현상</code>을 완화하기 위해 CPU와 메인 메모리 사이에 
크기는 작지만 속도가 빠른<code>캐시 메모리</code>를 두고
‼️ 재사용 가능성이 높은 데이터 복사본을 저장해둔 후, CPU가 요청하는 데이터를 바로바로 전달함</p>
</blockquote>
<hr />
<br />

<hr />
<h2 id="메모리-계층-구조의-목적">메모리 계층 구조의 목적</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/838450d0-5279-414b-bc33-531636dbde11/image.png" /></p>
<ul>
<li>⬆️ 위로 갈 수록 빠르고, 비싸고, 작은 용량을 가며 CPU와 가까움</li>
<li>캐싱은 CPU와 RAM 사이에서만 사용되는 것은 아님</li>
<li>한 계층은 바로 아래 계층에 대하여 캐싱 작업을 수행
  ➡️ 캐싱을 이용하여 빠르고 작은 메모리와 크고 느린 메모리의 장점을 조합
  ➡️ <strong>크고 빠른 메모리처럼 행동하도록 만듦</strong></li>
</ul>
<hr />
<br />

<hr />
<h2 id="데이터-지역성의-원리">데이터 지역성의 원리</h2>
<blockquote>
<p>재사용할 가능성이 클 것으로 예상되는 데이터의 복사본을 저장함으로써 캐싱을 할 수 있다.
    🤔 재사용성이 큰지는 어떻게 알 수 있을까?
        ➡️ 데이터의 지역성의 원리로 판단함</p>
</blockquote>
<br />

<h3 id="데이터-지역성의-원리란">데이터 지역성의 원리란</h3>
<ul>
<li>데이터 접근이 <strong>시간적</strong> 혹은 <strong>공간적</strong>으로 가깝게 일어나는 것을 의미<ul>
<li>(ex) 한 번 참조된 변수는 잠시 후에 또 참조될 가능성이 높다.</li>
<li>(ex) 어떤 데이터에 접근할 때, 그 데이터 근처에 있는 다른 데이터도 참조될 가능성이 높다.</li>
</ul>
</li>
</ul>
<br />


<h3 id="1-시간-지역성">1. 시간 지역성</h3>
<ul>
<li>최근에 접근한 데이터는 가까운 미래에 다시 접근할 가능성이 높다.</li>
<li>ex) for문, while문의 조건 변수 i </li>
</ul>
<p>자바 코드로 보는 <code>시간 지역성</code> 간단 예시</p>
<pre><code class="language-java">        int x = 0;

        for (int i = 0; i &lt; 5; i++) {
            x = x + 1; // 같은 변수 x에 반복적으로 접근
            System.out.println(x);
        }</code></pre>
<ul>
<li>변수 x와 변수 i를 반복문 안에서 계속 접근하고 사용함
  ➡️ 짧은 시간 안에 여러 번 접근 하는게 바로 <code>시간 지역성</code></li>
</ul>
<br />


<h3 id="2-공간-지역성">2. 공간 지역성</h3>
<ul>
<li>한 번 접근한 데이터 근처의 데이터도 곧 접근될 가능성이 높다.</li>
<li>ex) 배열 - 순서대로 접근할 가능성이 큼</li>
</ul>
<p>자바 코드로 보는 <code>공간 지역성</code> 간단 예시</p>
<pre><code class="language-java">        int[] arr = {1, 2, 3, 4, 5};

        for (int i = 0; i &lt; arr.length; i++) {
            System.out.println(arr[i]); // 배열 요소를 순차적으로 접근
        }</code></pre>
<ul>
<li>배열 arr의 요소들을 순차적으로 접근</li>
<li>배열은 메모리에 <strong>연속적으로 저장</strong> 되기 때문에, arr[0]을 가져오면 다음 배열들도 그 근처에 있음
  ➡️ 그래서 CPU는 한 번 불러온 메모리 블록 근처 데이터도 미리 캐싱해두면 성능이 올라감<pre><code>  고게 바로 `공간 지역성`</code></pre></li>
</ul>
<hr />
<br />

<hr />
<h2 id="캐시-히트와-캐시-미스">캐시 히트와 캐시 미스</h2>
<p>데이터 지역성의 원리를 사용해서 캐시에 데이터를 넣음
그러면 이제 cpu가 메모리에 데이터를 요청할 때
메인 메모리에 접근하기에 앞서 캐시 메모리에 접근해서 캐시 메모리 내 데이터 존재 여부를 확인</p>
<p>이 때 캐시 메모리가 해당 데이터를 가지고 있다면 
-&gt; 캐시 히트(캐시 적중)</p>
<p>해당 데이터가 없어서 메인 메모리에서 가져와야 한다면
-&gt; 캐시 미스</p>
<hr />
<br />

<hr />
<h2 id="캐시의-쓰기-동작write">캐시의 쓰기 동작(write)</h2>
<ul>
<li><strong>캐시와 메인 메모리 간의 일관성을 어떻게 유지하느냐</strong></li>
</ul>
<blockquote>
<p>가정)
CPU가 어떤 데이터를 쓰려고 할 때, (데이터를 저장하거나 수정할 때)(값변경이 일어날 때)
그 데이터의 주소가 <strong>캐시에 이미 존재(캐시 히트상태)</strong> 한다면 바로 메모리에 쓰는 게 아니라 <strong>캐시의 데이터만 먼저 바뀜</strong>
🤔 근데 캐시만 바꾸고 메모리는 안 바꾸면?
❌ 캐시와 메모리의 데이터가 달라짐
 ➡️ 이를 보완하기 위해 언제 메모리를 업데이트 할지 정하는 정책 2가지 있음</p>
</blockquote>
<br />

<h3 id="1️⃣-write-through-쓰기-관통-정책">1️⃣ Write Through (쓰기-관통) 정책</h3>
<ul>
<li>매번 메모리 업데이트</li>
<li>캐시에 쓰는 동시에 메인 메모리도 바로 같이 업데이트</li>
<li>⭕ 항상 캐시와 메모리가 동기화됨 (일관성 ⬆️)</li>
<li>❌ 느림 - 매번 메모리를 접근함</li>
</ul>
<br />

<h3 id="2️⃣-write-back-쓰기-되돌리기-정책">2️⃣ Write-Back (쓰기-되돌리기) 정책</h3>
<ul>
<li>미루다 한꺼번에 메모리 업데트</li>
<li>일단 캐시만 변경, 나중에 데이터가 캐시에서 제거될 때 메모리를 업데이트</li>
<li>⭕ 성능 좋음 - 매번 메모리에 접근하지 않음</li>
<li>❌ 캐시와 메모리 사이의 값이 일시적으로 다를 수 있음
  ➡️ 캐시에 dirty bit이라는 더러움 표시를 둬서 나중에 메모리에 반영함</li>
</ul>
<hr />
<br />

<br />

<hr />
<br />

<h1 id="spring에서의-캐싱">Spring에서의 캐싱</h1>
<br />

<h2 id="캐시-추상화">캐시 추상화</h2>
<ul>
<li>스프링에서 빈의 메서드에 캐시를 적용할 수 있는 기능을 제공</li>
<li>AOP를 이용해 메서드 내부 구현에 영향을 미치지 않고 적용</li>
<li>특정 캐시 기술에 종속하지 않음</li>
<li>캐싱이 필요한 비즈니스 로직에서 EnCache, Redis 등 캐싱 종류에 의존할 필요 없음
  ➡️ 캐시 사용 환경이나, 캐시 종류(EnCache, Redis)가 변경되더라도 어플리케이션 코드를 수정할 필요 없음 스프링에서 알아서 처리해주니까</li>
</ul>
<br />

<hr />
<blockquote>
<p>🤔 AOP를 이용해 메서드 내부 구현에 영향을 미치지 않고 적용? 뭔 말?</p>
</blockquote>
<p><code>AOP(관점 지향 프로그래밍)</code></p>
<ul>
<li>핵심 비즈니스 로직(예: 유저 조회) <strong>앞뒤에 끼어드는 코드(예: 캐시 처리, 트랜잭션 처리, 로깅)</strong>를 따로 분리해서 관리하는 방식</li>
<li>AOP는 쉽게 말하면 <strong>&quot;몰래 끼어들기 기술&quot;</strong><ul>
<li>ex) @Transactional</li>
</ul>
</li>
</ul>
<br />

<p><code>ex1) Transactional</code></p>
<pre><code class="language-java">@Transactional
public void doSomething() {
    // 비즈니스 로직
}</code></pre>
<ul>
<li>이 메서드가 실행되면, Spring AOP가 프록시 객체를 만들어서 트랜잭션 시작/커밋/롤백을 자동으로 끼워넣음.</li>
<li>개발자는 몰라도 되고, 스프링이 AOP로 처리함.</li>
</ul>
<br />

<p><code>ex2) Cacheable (캐싱도 트랜잭셔널과 똑같이 동작한다)</code></p>
<pre><code class="language-java">@Cacheable(&quot;users&quot;)
public User getUser(Long id) {
    return userRepository.findById(id).orElse(null);
}</code></pre>
<ul>
<li>이 메서드도 스프링이 프록시를 만들어서 실행 전에 이렇게 처리함:<ol>
<li>캐시에 이미 있는지 확인<ul>
<li>있으면 → DB 호출 없이 캐시 값 리턴</li>
<li>없으면 → 진짜 메서드 실행하고 결과를 캐시에 저장</li>
</ul>
</li>
</ol>
</li>
<li>즉, 캐싱 로직도 AOP 방식으로 &quot;끼어듦&quot;!</li>
</ul>
<hr />
<br />

<hr />
<h2 id="의존성-추가">의존성 추가</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/3405a132-8335-43a3-8e3b-7f5fc6e1d47d/image.png" /></p>
<ul>
<li>캐시 추상화를 하려면 의존성 추가해야함</li>
</ul>
<p>implementation 'org.springframework.boot:spring-boot-starter-cache'</p>
<blockquote>
<p>build.gradle에 추가</p>
</blockquote>
<hr />
<br />

<hr />
<h2 id="캐시-매니저-설정">캐시 매니저 설정</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/2e7160b3-c624-4e6e-baae-7a07878bf89a/image.png" /></p>
<ul>
<li><p>캐시 추상화에서는 캐시 기술을 지원하는 캐시 매니저를 Bean으로 등록해야 한다.</p>
</li>
<li><p>캐시를 사용하기 위해선 캐시 매니저를 스프링 빈으로 등록해야된다는 말임.</p>
</li>
<li><p>그래야  @Cacheable, @CachePut, @CacheEvict 같은 캐시 어노테이션을 쓸 수 있고
  어떤 방식으로 캐싱할지를 스프링이 알 수 있음</p>
<ul>
<li>ex) 캐시 종류(Redis, EhCache, Caffeine)에 따라 다른 캐시 매니저 등록</li>
</ul>
<ul>
<li>@EnableCaching 어노테이션 필수로 달기</li>
<li>저장할 캐시공간 이름 set하기 (movies)</li>
</ul>
</li>
</ul>
<blockquote>
<p>프로젝트에서 필터 기능을 쓰려고 FilterRegistarationBean을 빈으로 등록했듯이</p>
</blockquote>
<p> <img alt="" src="https://velog.velcdn.com/images/mo00ai/post/fdfc48b4-8e0f-4f42-94a0-67db8f476a87/image.png" /></p>
<hr />
<h3 id="캐시-매니저-종류-참고">캐시 매니저 종류 (참고)</h3>
<ul>
<li><p><code>ConcurrentMapCacheManager</code>: JRE에서 제공하는 ConcurrentHashMap을 캐시 저장소로 사용할 수 있는 구현체다. 캐시 정보를 Map 타입으로 메모리에 저장해두기 때문에 빠르고 별다른 설정이 필요 없다는 장점이 있지만, 실제 서비스에서 사용하기엔 기능이 빈약하다.</p>
</li>
<li><p><code>SimpleCacheManager</code>: 기본적으로 제공하는 캐시가 없다. 사용할 캐시를 직접 등록하여 사용하기 위한 캐시 매니저 구현체다.</p>
</li>
<li><p><code>EhCacheCacheManager</code>: Java에서 유명한 캐시 프레임워크 중 하나인 EhCache를 지원하는 캐시 매니저 구현체다.</p>
</li>
<li><p><code>CaffeineCacheManager</code>: Java 8로 Guava 캐시를 재작성한 Caffeine 캐시 저장소를 사용할 수 있는 구현체다. EhCache와 함께 인기 있는 매니저인데, 이보다 좋은 성능을 갖는다고 한다.</p>
</li>
<li><p><code>JCacheCacheManager</code>: JSR-107 표준을 따르는 JCache 캐시 저장소를 사용할 수 있는 구현체다.</p>
</li>
<li><p><code>RedisCacheManager</code>: Redis를 캐시 저장소로 사용할 수 있는 구현체다.</p>
</li>
<li><p><code>CompositeCacheManager</code>: 한 개 이상의 캐시 매니저를 사용할 수 있는 혼합 캐시 매니저다.</p>
</li>
</ul>
<br />


<hr />
<br />

<h2 id="실제-구현">실제 구현</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/95dd89e5-f0c9-4b18-a305-5c1de4c967fe/image.png" /></p>
<ul>
<li><p>Service 계층의 메서드에 @Cacheable 어노테이션 부착</p>
</li>
<li><p>비캐시와 캐시 시간 차이를 주목</p>
</li>
<li><p>전체 목록 조회를 3번 할 경우</p>
</li>
<li><p>비캐시 - 매번 전체 목록 조회할 시에 데이터를 가져오는데 2초가 걸림</p>
</li>
<li><p>캐시 - 처음 전체 목록 조회만 2초가 걸리고 그 뒤부터 전체 목록 조회는 시간이 매우 절약됨</p>
</li>
</ul>
<br />

<p>블로그 참고</p>
<blockquote>
<p><a href="https://bcp0109.tistory.com/385">https://bcp0109.tistory.com/385</a></p>
</blockquote>
<ul>
<li>눌러서 보여드릴 것</li>
<li>실제 어노테이션 적용, 어노테이션 종류</li>
</ul>
<hr />
<br />

<hr />
<h2 id="주의할-점">주의할 점</h2>
<h3 id="️모든-상황에서-캐싱을-사용하는-것은-좋지-않다️">‼️모든 상황에서 캐싱을 사용하는 것은 좋지 않다‼️</h3>
<ul>
<li>캐시는 값을 저장하고 불러오기 때문에 <strong>반복적으로 동일한 결과를 반환하는 경우에 용이</strong></li>
<li>매번 다른 결과를 돌려줘야 하는 상황이라면 오히려 성능 저하를 야기</li>
<li>캐시 저장 및 확인 작업에서 부하가 생김</li>
<li><strong>작업의 시간이 오래 걸리거나 서버에 부담을 주는 경우에 사용</strong>을 고려</li>
</ul>
<hr />
<br />

<hr />
<blockquote>
<p>참고
<a href="https://www.youtube.com/watch?v=JBFT4KyEvoY">https://www.youtube.com/watch?v=JBFT4KyEvoY</a>
<a href="https://www.youtube.com/watch?v=H4J-8pPMvEU&amp;list=LL">https://www.youtube.com/watch?v=H4J-8pPMvEU&amp;list=LL</a>
<a href="https://bcp0109.tistory.com/385">https://bcp0109.tistory.com/385</a>
<a href="https://velog.io/@songs4805/Spring-Cache%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90">https://velog.io/@songs4805/Spring-Cache%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90</a></p>
</blockquote>