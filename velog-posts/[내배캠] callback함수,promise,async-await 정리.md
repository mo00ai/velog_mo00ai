<p>정말 죽어도<del>~</del>
죽어도 모르겠는 개념들이다 
오늘 시간도 많겠다 하루종일 이것만 들여댜 보고있었다
<strong>철저히 나를 위한 나만의 언어들로 설명했으니 이해 안갈 수도 있음</strong></p>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/d9b3f909-bb16-48a4-ae19-15dc0f9aaea5/image.png" /></p>
<p>됐고 아무튼 시작!</p>
<hr />
<br />

<h3 id="동기-vs-비동기">동기 vs 비동기</h3>
<p>가 중요!
<code>동기</code> -&gt; 순차적으로 진행함 한 번에 한 개 진행
<code>비동기</code> -&gt; 비동기 작업 진행되는 동안 다른 코드도 실행됨 한번에 여러개 </p>
<blockquote>
<p>주로 비동기 작업은
<strong>서버 요청, 파일 읽기, 애니메이션, 타이머</strong>에 사용됨</p>
</blockquote>
<br />

<hr />
<br />


<h3 id="callback-함수">callback 함수</h3>
<p>자바스크립트에서 함수를 인자로 전달하고,
그 전달된 함수가 나중에 호출되는 경우, 전달된 그 함수를 &quot;콜백(callback)&quot; 이라고 부릅니다.</p>
<p>즉,</p>
<p>&quot;함수의 인자로 전달되어 특정 시점이나 작업 완료 후에 실행되는 함수&quot;</p>
<p>를 콜백함수라고 합니다.</p>
<br />

<p>📌 함수가 인자로 들어가면 무조건 콜백일까?
함수가 함수의 인자로 들어갔다고 해서 무조건 콜백이 되는 것은 아닙니다.
엄밀히 말하면, 자바스크립트에선 용도에 따라 달라집니다.</p>
<p>다만, 대부분 자바스크립트에서는
<strong>함수를 인자로 받아서 나중에 호출한다면 일반적으로 그것을 &quot;콜백 함수&quot;</strong>라고 표현합니다.</p>
<br />

<p>✅ 예시로 명확히 이해하기:
[콜백 함수의 대표적인 예시]</p>
<pre><code class="language-java">// 일반적인 콜백 함수의 예시
function getData(callback) {
  setTimeout(() =&gt; {
    callback(&quot;결과&quot;);
  }, 1000);
}

getData(result =&gt; {
  console.log(result);
});</code></pre>
<p>위에서 callback은 나중에 데이터가 준비되었을 때 호출됩니다.
이 경우는 분명한 콜백입니다.
특히나 비동기 콜백</p>
<blockquote>
<p>비동기작업에서 (setTimeout) 인자로 들어온 함수가 호출됐기 때문입니다.</p>
</blockquote>
<br />

<p>📌 단순히 함수가 인자로 들어가도 &quot;즉시 실행&quot;되는 경우도 있다!
예를 들어 map 메서드를 생각해봅시다.</p>
<pre><code class="language-java">[1, 2, 3].map((item) =&gt; item * 2);</code></pre>
<p>map도 함수를 인자로 받지만, 이 함수는 즉시 동기적으로 실행됩니다.</p>
<ul>
<li>이런 경우에도 보통 &quot;콜백 함수&quot;라고 부르긴 하지만,</li>
<li>비동기 작업이 아니고 즉시 실행되는 동기적인 콜백으로 분류합니다.</li>
</ul>
<br />

<p><code>즉시 실행되는 콜백 예시 (동기 콜백):</code></p>
<ul>
<li>배열 메서드: map, forEach, filter, reduce</li>
<li>sort 함수의 비교함수</li>
</ul>
<p><code>나중에 실행되는 콜백 예시 (비동기 콜백):</code></p>
<ul>
<li>setTimeout, setInterval</li>
<li>AJAX 호출 (fetch, axios 등)</li>
<li>이벤트 리스너 (addEventListener)</li>
</ul>
<br />
<br />

<hr />
<br />

<pre><code>function fetchData() {
  setTimeout(() =&gt; {
    return &quot;데이터 도착!&quot;;
  }, 2000);
}

const result = fetchData();
console.log(result); // undefined</code></pre><pre><code>---출력----
undefined
(2초 후) 데이터 도착!</code></pre><p>이런 식으로 <strong>콜백함수를 이용하지 않았을 경우</strong>엔
 setTimeout이 실행되었지만, 결과를 기다리지 않고 다음 줄이 실행되면서 undefined가 출력됨
콜백함수를 썼다면 </p>
<br />

<pre><code>function fetchData(callback) {
  setTimeout(() =&gt; {
    callback(&quot;데이터 도착!&quot;);
  }, 2000);
}

fetchData((data) =&gt; {
  console.log(data); // 2초 후 &quot;데이터 도착!&quot; 출력
});</code></pre><blockquote>
<p>이런식으로 가져온 데이터를 처리하는 함수를 fetchData의 인자로 받아 비동기작업(ex데이터요청)후에 실행함으로써 데이터가 필요한 작업들이 데이터를 모두 받아온 후에 실행할 수 있도록 함.</p>
</blockquote>
<blockquote>
<p>이 과정을 하고 있는 중에 일반 코드(동기작업)들을 진행해서 시간을 효율적으로 쓰는 거임! 
동기적으로(순차적)으로 수행하면 데이터 요청 다 되기도 전에 데이터를 활용해서 에러가 난다던가, 비동기작업 기다리느라 다른 작업 수행 못하던가 그러니까</p>
</blockquote>
<br />

<h4 id="콜백함수-사용-예시">콜백함수 사용 예시</h4>
<pre><code>function getUserData(callback) {
  setTimeout(() =&gt; {
    const user = { id: 1, name: &quot;홍길동&quot; };
    callback(user); // 데이터가 도착하면 콜백 실행
  }, 2000);
}

// 콜백 함수 안에서 데이터를 활용
getUserData((user) =&gt; {
  console.log(&quot;가져온 데이터:&quot;, user); // 데이터 받은 후 실행
});</code></pre><p>화살표 함수 사용한 콜백예시</p>
<pre><code>function getUserData(callback) { // callback은 함수
  setTimeout(function() {  // 2초 후 실행
    const user = { id: 1, name: &quot;홍길동&quot; };
    callback(user); // 여기서 callback 함수 실행!
  }, 2000);
}

// 콜백 함수 정의
function printUser(user) {
  console.log(&quot;가져온 데이터:&quot;, user);
}

// getUserData를 실행하면서 printUser를 콜백으로 전달
getUserData(printUser);</code></pre><br />

<p><strong><em>callback은 단순히 함수를 인자로 받는 매개변수일 뿐이다</em></strong></p>
<blockquote>
<p>우리가 메서드를 만들 때 ex) public void method(String name)를 예로 들자면
String 변수를 인자로 받는 매개변수인 String name처럼 
callback도 함수를 인자로 받는 매개변수인 거임</p>
</blockquote>
<blockquote>
<p>여기선 printUser란 함수가 getUserData(printUser)에 인자로 들어가게 됨
<strong><em>이렇게 함수의 인자로 들어간 함수를 <code>콜백함수</code></em></strong> 라고함
<strong><em>이걸 동기로 쓸 거냐 비동기로 쓸 거냐는 개발자의 선택으로 달라지는 거임</em></strong></p>
</blockquote>
<blockquote>
<p>매개변수이기 때문에 callback이라 안 써도 되고 cb, ck 이런 식으로 써도 됨 ㅇㅇ</p>
</blockquote>
<pre><code class="language-java">function getUserData(callback)
function getUserData(cb)
function getUserData(ck)</code></pre>
<br />
<br />


<p>마지막 설명</p>
<pre><code class="language-java">function fetchData(callback) {
  console.log(&quot;서버 요청 시작!&quot;);
  setTimeout(() =&gt; {
    callback(&quot;서버 데이터 도착!&quot;);
  }, 2000);
}

function printResult(result) {
  console.log(result);
}

// 비동기 요청 시작
fetchData(printData);

// 아래 코드는 즉시 실행됩니다.
console.log(&quot;이 코드는 바로 실행됨&quot;);
console.log(&quot;다른 동기 작업을 계속 수행 중...&quot;);



---출력결과---
이 코드는 바로 실행됨
다른 동기 작업을 계속 수행 중...
(약 2초 후)
데이터 도착!</code></pre>
<ul>
<li>데이터가 올 때까지 2초 동안 멈춰 있지 않고, 다른 코드(console.log)를 실행합니다.</li>
<li>데이터를 기다리는 동안 브라우저는 계속 다른 일을 하고 있으며, 데이터를 기다리느라 시간을 낭비하지 않습니다.</li>
</ul>
<br />

<p> 현실적인 예로 풀어보면:
웹 페이지가 로딩될 때 서버로부터 데이터를 받아오는 작업을 예로 들어보면:</p>
<ul>
<li>데이터를 기다리느라 아무 작업도 안 하면 → 화면이 멈춘 듯 보여서 사용자 경험이 나쁨</li>
<li>데이터를 기다리는 동안 화면에 로딩 스피너를 보여주거나 다른 버튼이 동작되도록 하면 </li>
<li>→ 사용자는 페이지가 부드럽게 작동하는 느낌을 받음</li>
</ul>
<p>이때 비동기적으로 처리하면:</p>
<ul>
<li>화면에 로딩 애니메이션을 띄워주고,</li>
<li>데이터가 오기 전에 다른 요소들을 미리 그려주거나,</li>
<li>사용자와 상호작용이 멈추지 않아 더 나은 UX를 제공합니다.</li>
</ul>
<br />
<br />


<h3 id="비동기-작업--콜백함수-예시">비동기 작업 / 콜백함수 예시</h3>
<table>
<thead>
<tr>
<th>비동기 작업 예시</th>
<th>대표적인 콜백 사용 예시</th>
</tr>
</thead>
<tbody><tr>
<td>서버 요청 (<code>fetch</code>, AJAX 등)</td>
<td>서버로부터 데이터를 받은 후 실행될 함수</td>
</tr>
<tr>
<td>타이머 (<code>setTimeout</code>, <code>setInterval</code>)</td>
<td>일정 시간이 지난 후 실행될 함수</td>
</tr>
<tr>
<td>애니메이션 (<code>requestAnimationFrame</code>)</td>
<td>다음 프레임이 준비된 후 실행될 함수</td>
</tr>
<tr>
<td>이벤트 핸들러 (<code>addEventListener</code>)</td>
<td>클릭, 입력 등 이벤트 발생 후 실행될 함수</td>
</tr>
<tr>
<td>파일 I/O (<code>fs.readFile</code>)</td>
<td>파일을 읽은 후 실행될 함수</td>
</tr>
<tr>
<td>Promise 작업 (<code>then</code>, <code>catch</code>)</td>
<td>비동기 작업 완료 후 실행되는 함수</td>
</tr>
<tr>
<td>Async/Await</td>
<td>비동기 작업의 완료를 기다리는 함수</td>
</tr>
<tr>
<td>데이터베이스 요청</td>
<td>DB에서 데이터를 받은 후 처리할 함수</td>
</tr>
<tr>
<td>사용자 입력 이벤트 (<code>onClick</code>, <code>onChange</code>)</td>
<td>특정 이벤트 발생 후 실행될 함수</td>
</tr>
</tbody></table>
<br />
<br />

<hr />
<br />

<h4 id="콜백지옥">콜백지옥</h4>
<ul>
<li>콜백이 중첩되면 콜백지옥이라고 코드가 드러워짐 이것의 해결책으로 promise(), async/await이 나오게 된거임</li>
</ul>
<br />

<hr />
<br />
<br />

<h3 id="promise">PROMISE()</h3>
<ul>
<li>Promise는 자바스크립트에서 비동기 작업(asynchronous operation)을 깔끔하게 처리하기 위해 제공되는 객체입니다. 비동기 작업은 보통 데이터를 서버에서 받아오는 API 요청이나 파일 읽기, 타이머 같은 작업에서 많이 사용됩니다.</li>
</ul>
<br />

<p>📌 <strong><em>Promise의 핵심 개념</em></strong>
Promise는 세 가지 상태(state)를 가집니다:</p>
<ul>
<li>Pending (대기 상태): 비동기 작업이 아직 진행 중인 상태</li>
<li>Fulfilled (성공 상태): 작업이 성공적으로 완료되어 결과값이 전달된 상태</li>
<li>Rejected (실패 상태): 작업 수행 도중 에러가 발생한 상태
한 번 상태가 결정(Fulfilled/Rejected)되면 더 이상 상태가 바뀌지 않습니다.</li>
</ul>
<br />

<p><strong><em>Promise 사용법</em></strong></p>
<ul>
<li>메서드 체이닝을 이용해 다룬다.<pre><code class="language-js">promise
.then((result) =&gt; {
  // 성공한 경우 실행
  console.log(result);
})
.catch((error) =&gt; {
  // 실패한 경우 실행
  console.error(error);
})
.finally(() =&gt; {
  // 성공, 실패 여부와 관계없이 항상 실행
  console.log('작업 종료');
});
</code></pre>
</li>
</ul>
<pre><code>- `then` : Promise가 성공하면 실행
- `catch` : Promise가 실패하면 실행
- `finally` : 결과와 상관없이 작업이 끝나면 실행

&gt; 콜백지옥(중첩콜백)을 예방하여 가독성 좋은 비동기 코드 작성 가능 -&gt; 체이닝의 장접
비동기 작업을 구조적이고 예측 가능한 방식으로 처리 가능
오류 처리와 상태 관리가 쉬워짐

&lt;br&gt;
&lt;br&gt;


#### Promise 사용 예제1 (라면 끓이기) - 라면 끓이는데 3초 걸림
```java
// 라면 끓이는 함수 정의하기 (3초 후 라면 완성!)
const cookRamen = () =&gt; {
  return new Promise((resolve, reject) =&gt; {
    setTimeout(() =&gt; {
      const isSuccess = true; // 라면이 잘 끓여졌는지 (실패상황을 만들고 싶으면 false로!)

      if (isSuccess) {
        resolve('🍜 라면 완성!');
      } else {
        reject('🔥 라면 끓이다 태움!');
      }

    }, 3000); // 3초 뒤 완료
  });
};

// 함수 실행하기
cookRamen()
  .then((successMessage) =&gt; {
    console.log(successMessage); // 성공하면 여기로!
  })
  .catch((errorMessage) =&gt; {
    console.error(errorMessage); // 실패하면 여기로!
  });</code></pre><p>이 함수를 뜯어보자!</p>
<br />

<p>1.Promise를 반환하는 함수 생성</p>
<pre><code class="language-java">const cookRamen = () =&gt; {
  return new Promise((resolve, reject) =&gt; {
    // 여기서 비동기 작업 수행!
  });
};</code></pre>
<ul>
<li>함수명은 cookRamen입니다.</li>
<li>새로운 Promise를 반환해요.</li>
<li>Promise는 내부에서 resolve, reject 두 가지 매개변수를 받습니다.</li>
<li><code>resolve</code>: 성공하면 호출하는 함수</li>
<li><code>reject</code>: 실패하면 호출하는 함수</li>
</ul>
<br />

<ol start="2">
<li>비동기 작업 추가<pre><code class="language-java">setTimeout(() =&gt; {
// 3초 후 여기 코드가 실행됨!
}, 3000);</code></pre>
</li>
</ol>
<br />

<ol start="3">
<li>성공 여부를 확인하고 resolve 또는 reject 호출<pre><code class="language-java">const isSuccess = true; // 성공 여부를 설정 (false로 바꾸면 reject로)
</code></pre>
</li>
</ol>
<p>if (isSuccess) {
  resolve('🍜 라면 완성!');
} else {
  reject('🔥 라면 끓이다 태움!');
}</p>
<pre><code>
&lt;br&gt;

4. 실행 부분
```java
cookRamen()
  .then((successMessage) =&gt; {
    console.log(successMessage); // 성공 시 호출
  })
  .catch((errorMessage) =&gt; {
    console.error(errorMessage); // 실패 시 호출
  });</code></pre><ul>
<li>cookRamen() 함수를 실행하면 Promise가 시작됩니다.</li>
<li><strong>성공(resolve)</strong>하면 .then()으로 전달되고,</li>
<li><strong>실패(reject)</strong>하면 .catch()로 전달됩니다.</li>
</ul>
<br />

<blockquote>
<p>resolve()는 다양한 값을 반환 </p>
</blockquote>
<ul>
<li>문자열, 숫자, 객체, 배열, boolean, 다른 Promise객체 등 다양한 값을 반환하여 then으로 넘길 수 있음</li>
</ul>
<br />
<br />


<h4 id="promise-사용-예제2">Promise 사용 예제2</h4>
<pre><code class="language-java">function getUserData() {
  console.log(&quot;서버에서 데이터 요청 중...&quot;);

  return new Promise((resolve) =&gt; {
    setTimeout(() =&gt; {
      const userData = { id: 1, name: &quot;홍길동&quot;, age: 25 };
      console.log(&quot;서버 응답 완료!&quot;);
      resolve(userData); // 데이터가 준비되면 resolve 호출
    }, 2000);
  });
}

// then을 사용해서 데이터를 처리
getUserData().then((data) =&gt; {
  console.log(&quot;가져온 데이터:&quot;, data);
});



---실행순서
서버에서 데이터 요청 중...
(2초 후)
서버 응답 완료!
가져온 데이터: { id: 1, name: '홍길동', age: 25 }</code></pre>
<br />
<br />

<h4 id="promise-활용-예시">Promise 활용 예시</h4>
<pre><code class="language-java">const getData = () =&gt; new Promise((resolve, reject) =&gt; {
  $.get('url 주소/products/1', (response) =&gt; {
    if (response) {
      resolve(response);
    } else {
      reject(new Error(&quot;Request is failed&quot;));
    }
  });
});

getData()
  .then((data) =&gt; console.log(data))
  .catch((err) =&gt; console.error(err));</code></pre>
<blockquote>
<p>이렇게도 쓴다는 걸 걍 알아만 두쇼</p>
</blockquote>
<br />
<br />

<h4 id="promise-활용-예시-1">Promise 활용 예시</h4>
<pre><code class="language-java">const cookRamen = () =&gt; {
  return new Promise((resolve) =&gt; {
    setTimeout(() =&gt; {
      resolve({ menu: '신라면', time: 3 });
    }, 3000);
  });
};

cookRamen()
  .then((ramenInfo) =&gt; {
    console.log(ramenInfo.menu); // &quot;신라면&quot;
    console.log(ramenInfo.time); // 3
  });</code></pre>
<blockquote>
<p>라면 객체를 then으로 보냄</p>
</blockquote>
<blockquote>
<p>왜 라면 <strong><em>객체</em></strong>이냐?</p>
</blockquote>
<p>자바스크립트에서 <strong><em>객체(Object)</em></strong>는 여러 가지 데이터를 { } 안에 <strong><em>키(key)</em></strong>와 <strong><em>값(value)</em></strong>의 쌍으로 묶어서 표현한 걸 말합니다.</p>
<pre><code class="language-java">resolve({ menu: '신라면', time: 3 });</code></pre>
<blockquote>
<p>중괄호로 묶여있고, munu, time과 같은 key에 대응되는 값이 존재
이렇게 키와 값이 쌍으로 이루어진 데이터 형테를 js에선 객체라고 함</p>
</blockquote>
<br />
<br />

<p>참고</p>
<pre><code class="language-java">// 포스트 id가 1인 포스트를 검색하고 프로미스를 반환한다.
promiseAjax('GET', `${url}/1`)
  // 포스트 id가 1인 포스트를 작성한 사용자의 아이디로 작성된 모든 포스트를 검색하고 프로미스를 반환한다.
  .then(res =&gt; promiseAjax('GET', `${url}?userId=${JSON.parse(res).userId}`))
  .then(JSON.parse)
  .then(render)
  .catch(console.error);</code></pre>
<br />
<br />

<h4 id="promise-asyncawait과-함께-사용하기">promise, async/await과 함께 사용하기</h4>
<pre><code class="language-java">const fetchData = () =&gt; new Promise((resolve) =&gt; {
  setTimeout(() =&gt; resolve('데이터 로딩 완료!'), 1000);
});

async function load() {
  try {
    const data = await fetchData(); // 비동기 작업을 기다림
    console.log(data);
  } catch (error) {
    console.error('에러:', error);
  } finally {
    console.log('작업 끝!');
  }
}

load();</code></pre>
<br />
<br />



<hr />
<br />
<br />

<h3 id="async--await-개념">async / await 개념</h3>
<br />

<h4 id="1-async-비동기-함수-선언">1. async (비동기 함수 선언)</h4>
<p>함수 앞에 async를 붙이면 그 함수는 비동기 함수가 됩니다.</p>
<blockquote>
<p>async 함수는 항상 Promise를 반환합니다.</p>
</blockquote>
<pre><code class="language-js">async function myFunc() {
  return '완료!';
}

// 또는 화살표 함수로 표현
const myFunc = async () =&gt; { /* 비동기 작업 */ };</code></pre>
<br />

<h4 id="await-promise를-기다림">await (promise)를 기다림</h4>
<ul>
<li>await 키워드는 async로 선언된 함수 내에서만 사용 가능하며,</li>
<li>Promise 작업이 완료될 때까지 기다리는 역할을 합니다.</li>
</ul>
<pre><code class="language-js">const cookRamen = () =&gt; new Promise((resolve) =&gt; {
  setTimeout(() =&gt; resolve('라면 완성!'), 3000);
});

async function ramenReady() {
  const result = await cookRamen(); // 완료될 때까지 여기서 기다림
  console.log(result); // '라면 완성!' 출력
}

cookRamen();</code></pre>
<ul>
<li>3초 후에 결과를 받아서 처리</li>
</ul>
<br />
<br />

<h4 id="아까-promise-코드와-비교해-보기">아까 promise 코드와 비교해 보기</h4>
<br />

<p>아까 작성한 promise 방식</p>
<pre><code class="language-js">cookRamen().then((data) =&gt; {
  console.log(data);
});</code></pre>
<br />

<p>async/await 으로 작성한 방식</p>
<pre><code class="language-js">const cookRamen = () =&gt; {
  return new Promise((resolve) =&gt; {
    setTimeout(() =&gt; resolve({ menu: '신라면', time: 3 }), 3000);
  });
};

async function startCooking() {
  const result = await cookRamen();
  console.log(result.menu);  // 신라면
  console.log(result.time);  // 3
}

load();</code></pre>
<blockquote>
<p>async함수들은 promise 객체를 반환함, <code>then</code>,<code>catch</code> 사용 가능</p>
</blockquote>
<br />

<pre><code class="language-java">const cookRamen = () =&gt; new Promise((resolve, reject) =&gt; {
  setTimeout(() =&gt; resolve({ menu: '진라면', time: '3분' }), 3000);
});

async function load() {
  const ramenInfo = await cookRamen(); // await로 결과 기다림
  console.log(ramen.menu); // 신라면
  console.log(ramen.time); // 3
}

// 함수 호출 부분에서는 then()을 사용 가능!
load()
  .then(() =&gt; {
    console.log('라면 끓이기 끝!');
  })
  .catch((error) =&gt; {
    console.error('에러 발생:', error);
  });</code></pre>
<blockquote>
<p>일케 혼합 사용도 가능하다</p>
</blockquote>