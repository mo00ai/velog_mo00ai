<h3 id="fetch">Fetch</h3>
<p>fetch는 서버에 웹 통신을 요청하고 그 안의 데이터를 받아오기 위해 사용하는 함수!
이번 강의에선 미세먼지 api를 가져왔다</p>
<br />

<br />

<h3 id="fetch-foreach문으로-각-데이터-value-뽑기">Fetch (Foreach문으로 각 데이터 value 뽑기)</h3>
<pre><code class="language-html">&lt;!doctype html&gt;
&lt;html lang=&quot;ko&quot;&gt;

&lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;title&gt;Fetch 시작하기&lt;/title&gt;
    &lt;script src=&quot;https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js&quot;&gt;&lt;/script&gt;
    &lt;script&gt;
        function hey() {
            let url = 'http://spartacodingclub.shop/sparta_api/seoulair';
            fetch(url)
                // 이 URL로 웹 통신을 요청한다. 괄호 안에 다른 것이 없다면 GET!
                .then(res =&gt; res.json())
                // 통신 요청을 받은 데이터는 res라는 이름으로 JSON화 한다
                .then(data =&gt; {
                    let rows = data['RealtimeCityAir']['row'];

                    rows.forEach(a =&gt; {
                        let gu_name = a['MSRSTE_NM'];
                        let gu_mise = a['IDEX_NM'];
                        console.log(gu_name, gu_mise);
                    });

                }) // JSON 형태로 바뀐 데이터를 data라는 이름으로 붙여 사용한다
        }
    &lt;/script&gt;
&lt;/head&gt;

&lt;body&gt;
    &lt;button onclick=&quot;hey()&quot;&gt;fetch 연습!&lt;/button&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
<br />
<br />


<hr />
<br />

<pre><code class="language-html">&lt;!doctype html&gt;
&lt;html lang=&quot;ko&quot;&gt;

&lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;title&gt;미세먼지 API로Fetch 연습하고 가기!&lt;/title&gt;

    &lt;script src=&quot;https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js&quot;&gt;&lt;/script&gt;

    &lt;style type=&quot;text/css&quot;&gt;
        div.question-box {
            margin: 10px 0 20px 0;
        }

        .bad {
            color: red;
        }
    &lt;/style&gt;

    &lt;script&gt;
        function q1() {

            //기본 태그 정보 지우기
            $('#names-q1').empty();

            let url = 'http://spartacodingclub.shop/sparta_api/seoulair';
            fetch(url).then(res =&gt; res.json()).then(data =&gt; {
                let rows = data['RealtimeCityAir']['row'];
                rows.forEach(a =&gt; {
                    let gu_name = a['MSRSTE_NM'];
                    let gu_mise = a['IDEX_MVL'];

                    let temp_html = ``;

                    if (gu_mise &gt; 40) {
                        temp_html = `&lt;li class=&quot;bad&quot;&gt;${gu_name} : ${gu_mise}&lt;/li&gt;`;
                    } else {
                        temp_html = `&lt;li&gt;${gu_name} : ${gu_mise}&lt;/li&gt;`;
                    }


                    $('#names-q1').append(temp_html);
                });
            })
        }
    &lt;/script&gt;

&lt;/head&gt;

&lt;body&gt;
    &lt;h1&gt;Fetch 연습하자!&lt;/h1&gt;

    &lt;hr /&gt;

    &lt;div class=&quot;question-box&quot;&gt;
        &lt;h2&gt;1. 서울시 OpenAPI(실시간 미세먼지 상태)를 이용하기&lt;/h2&gt;
        &lt;p&gt;모든 구의 미세먼지를 표기해주세요&lt;/p&gt;
        &lt;p&gt;업데이트 버튼을 누를 때마다 지웠다 새로 씌여져야 합니다.&lt;/p&gt;
        &lt;button onclick=&quot;q1()&quot;&gt;업데이트&lt;/button&gt;
        &lt;ul id=&quot;names-q1&quot;&gt;
            &lt;li&gt;중구 : 82&lt;/li&gt;
            &lt;li&gt;종로구 : 87&lt;/li&gt;
            &lt;li&gt;용산구 : 84&lt;/li&gt;
            &lt;li&gt;은평구 : 82&lt;/li&gt;
        &lt;/ul&gt;
    &lt;/div&gt;
&lt;/body&gt;

&lt;/html&gt;</code></pre>
<br />
<br />

<hr />
<br />

<h3 id="fetch-내-if문-활용-태그-내-class-부여로-글씨색-바꾸기">Fetch 내 if문 활용, 태그 내 class 부여로 글씨색 바꾸기</h3>
<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;

&lt;head&gt;
  &lt;meta charset=&quot;UTF-8&quot; /&gt;
  &lt;meta http-equiv=&quot;X-UA-Compatible&quot; content=&quot;IE=edge&quot; /&gt;
  &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1.0&quot; /&gt;
  &lt;title&gt;나만의 추억앨범&lt;/title&gt;
  &lt;script src=&quot;https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js&quot;&gt;&lt;/script&gt;
  &lt;link href=&quot;https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css&quot; rel=&quot;stylesheet&quot;
    integrity=&quot;sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC&quot; crossorigin=&quot;anonymous&quot; /&gt;
  &lt;style&gt;
    @import url(&quot;https://fonts.googleapis.com/css2?family=Do+Hyeon&amp;family=IBM+Plex+Sans+KR&amp;display=swap&quot;);

    * {
      font-family: &quot;IBM Plex Sans KR&quot;, serif;
    }

    .mytitle {
      background-color: green;

      height: 250px;
      color: white;

      /* 박스 안 내용물 정렬(세로or가로) */
      /* 세로:가로 flex-direction : column or low */
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;

      background-image: url(&quot;https://images.unsplash.com/photo-1511992243105-2992b3fd0410?ixlib=rb-4.0.3&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&amp;auto=format&amp;fit=crop&amp;w=1470&amp;q=80&quot;);
      background-position: center;
      background-size: cover;
    }

    .mytitle&gt;button {
      width: 150px;
      height: 50px;
      background-color: transparent;
      color: white;
      border: 1px solid white;
      border-radius: 5px;

      margin-top: 20px;
    }

    .mycards {
      width: 1200px;
      margin: 30px auto 0px auto;
    }

    .mypostingbox {
      width: 500px;
      margin: 30px auto 0px auto;
      padding: 20px;
      box-shadow: 0px 0px 3px 0px blue;
      border-radius: 5px;
    }

    .mybtn {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: center;
    }

    .mybtn&gt;button {
      margin-right: 5px;
    }
  &lt;/style&gt;

  &lt;script&gt;
    $(document).ready(function () {
      let url = &quot;http://spartacodingclub.shop/sparta_api/seoulair&quot;;
      fetch(url).then(res =&gt; res.json()).then(data =&gt; {
        let mise = data['RealtimeCityAir']['row'][0]['IDEX_NM'];
        $('#msg').text(mise);
      })
    });



    function openclose() {
      //숨기고 생기는 함수 style=&quot;display:none&quot;;을 해줌
      $('#postingbox').toggle();
    }

    function makeCard() {
      //입력값 가져오기
      let image = $('#image').val();
      let title = $('#title').val();
      let content = $('#content').val();
      let date = $('#date').val();

      //카드 만들기 
      let temp_html = `       
      &lt;div class=&quot;col&quot;&gt; 
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img
            src=&quot;${image}&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;${title}&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;${content}&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;${date}&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;`;
      $('#card').append(temp_html);
    }

  &lt;/script&gt;

&lt;/head&gt;

&lt;body&gt;
  &lt;div class=&quot;mytitle&quot;&gt;
    &lt;h1&gt;나만의 추억앨범&lt;/h1&gt;
    &lt;p&gt;현재 서울의 미세먼지 : &lt;span id=&quot;msg&quot;&gt;좋음&lt;/span&gt;&lt;/p&gt;
    &lt;button onclick=&quot;openclose()&quot;&gt;추억 저장하기&lt;/button&gt;
  &lt;/div&gt;
  &lt;div class=&quot;mypostingbox&quot; id=&quot;postingbox&quot;&gt;
    &lt;div class=&quot;form-floating mb-3&quot;&gt;
      &lt;input type=&quot;email&quot; class=&quot;form-control&quot; id=&quot;image&quot; placeholder=&quot;앨범 이미지&quot; /&gt;
      &lt;label for=&quot;floatingInput&quot;&gt;앨범 이미지&lt;/label&gt;
    &lt;/div&gt;
    &lt;div class=&quot;form-floating mb-3&quot;&gt;
      &lt;input type=&quot;email&quot; class=&quot;form-control&quot; id=&quot;title&quot; placeholder=&quot;앨범 제목&quot; /&gt;
      &lt;label for=&quot;floatingInput&quot;&gt;앨범 제목&lt;/label&gt;
    &lt;/div&gt;
    &lt;div class=&quot;form-floating mb-3&quot;&gt;
      &lt;input type=&quot;email&quot; class=&quot;form-control&quot; id=&quot;content&quot; placeholder=&quot;앨범 내용&quot; /&gt;
      &lt;label for=&quot;floatingInput&quot;&gt;앨범 내용&lt;/label&gt;
    &lt;/div&gt;
    &lt;div class=&quot;form-floating mb-3&quot;&gt;
      &lt;input type=&quot;email&quot; class=&quot;form-control&quot; id=&quot;date&quot; placeholder=&quot;앨범 날짜&quot; /&gt;
      &lt;label for=&quot;floatingInput&quot;&gt;앨범 날짜&lt;/label&gt;
    &lt;/div&gt;
    &lt;div class=&quot;mybtn&quot;&gt;
      &lt;button onclick=&quot;makeCard()&quot; type=&quot;button&quot; class=&quot;btn btn-dark&quot;&gt;기록하기&lt;/button&gt;
      &lt;button type=&quot;button&quot; class=&quot;btn btn-outline-dark&quot;&gt;닫기&lt;/button&gt;
    &lt;/div&gt;
  &lt;/div&gt;
  &lt;div class=&quot;mycards&quot;&gt;
    &lt;div id=&quot;card&quot; class=&quot;row row-cols-1 row-cols-md-4 g-4&quot;&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img
            src=&quot;https://images.unsplash.com/photo-1446768500601-ac47e5ec3719?ixlib=rb-4.0.3&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&amp;auto=format&amp;fit=crop&amp;w=1446&amp;q=80&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;앨범 제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;앨범 내용&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;앨범날짜&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img
            src=&quot;https://images.unsplash.com/photo-1446768500601-ac47e5ec3719?ixlib=rb-4.0.3&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&amp;auto=format&amp;fit=crop&amp;w=1446&amp;q=80&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;앨범 제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;앨범 내용&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;앨범날짜&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img
            src=&quot;https://images.unsplash.com/photo-1446768500601-ac47e5ec3719?ixlib=rb-4.0.3&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&amp;auto=format&amp;fit=crop&amp;w=1446&amp;q=80&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;앨범 제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;앨범 내용&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;앨범날짜&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img
            src=&quot;https://images.unsplash.com/photo-1446768500601-ac47e5ec3719?ixlib=rb-4.0.3&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&amp;auto=format&amp;fit=crop&amp;w=1446&amp;q=80&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;앨범 제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;앨범 내용&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;앨범날짜&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
<blockquote>
<p>$(document).ready(function () {
    })
    -&gt; 기존에 버튼을 누르면 함수가 실행되는 방법과 다르게 이번은
    브라우저가 열리면 곧바로 미세먼지api 데이터를 가져와야 한다.
    이렇게 곧바로 실행되는 경우에 이 함수를 쓴다.</p>
</blockquote>
<blockquote>
<p>&lt;스팬&gt; 태그는 &lt;피&gt;태그 안에서 문자를 구분할 때 사용함</p>
</blockquote>
<br />
<br />

<hr />
<br />

<h3 id="서울날씨-api로-현재-날씨-반영하기">서울날씨 api로 현재 날씨 반영하기</h3>
<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;

&lt;head&gt;
  &lt;meta charset=&quot;UTF-8&quot; /&gt;
  &lt;meta http-equiv=&quot;X-UA-Compatible&quot; content=&quot;IE=edge&quot; /&gt;
  &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1.0&quot; /&gt;
  &lt;title&gt;스파르타플릭스&lt;/title&gt;
  &lt;script src=&quot;https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js&quot;&gt;&lt;/script&gt;
  &lt;link href=&quot;https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css&quot; rel=&quot;stylesheet&quot;
    integrity=&quot;sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC&quot; crossorigin=&quot;anonymous&quot; /&gt;
  &lt;style&gt;
    @import url(&quot;https://fonts.googleapis.com/css2?family=Do+Hyeon&amp;family=IBM+Plex+Sans+KR&amp;display=swap&quot;);

    * {
      font-family: &quot;IBM Plex Sans KR&quot;, serif;
    }

    .main {
      background-image: url(&quot;https://occ-0-1123-1217.1.nflxso.net/dnm/api/v6/6AYY37jfdO6hpXcMjf9Yu5cnmO0/AAAABeIfo7VL_VDyKnljV66IkR-4XLb6xpZqhpLSo3JUtbivnEW4s60PD27muH1mdaANM_8rGpgbm6L2oDgA_iELHZLZ2IQjG5lvp5d2.jpg?r=e6e.jpg&quot;);
      background-size: cover;
      background-position: center;
      color: white;
    }

    body {
      background-color: black;
    }

    .mycards {
      width: 1200px;
      margin: 20px auto 20px auto;
    }

    .mypostingbox {
      width: 500px;
      margin: 20px auto 20px auto;

      border: 1px solid white;
      padding: 20px;
      border-radius: 5px;
    }

    .form-floating&gt;input {
      background-color: transparent;
    }

    .form-floating&gt;label {
      color: white;
    }

    .input-group&gt;label {
      background-color: transparent;
      color: white;
    }

    .mypostingbox&gt;button {
      width: 100%;
    }
  &lt;/style&gt;

  &lt;!-- &lt;script&gt;
    // //변수
    // let a = &quot;hello&quot;;
    // console.log(a);

    //배열
    // let a = [&quot;사과&quot;, &quot;배&quot;, &quot;수박&quot;];
    // console.log(a[0]);

    // let person = {'name': 'bob', 'age': 30, height: 180 };
    // // console.log(person['name']);
    // console.log(person.name);

    // let name = person['name'];
    // let age = person['age'];
    // console.log(name, age);

    //리스트 딕셔너리
    // let a = [&quot;사과&quot;, &quot;배&quot;, &quot;수박&quot;];
    // console.log(a);


    // let ages = [15, 30, 28, 7, 40, 13];

    // ages.forEach(a =&gt; {
    //   if (a &lt; 20) {
    //     console.log('청소년입니다');
    //   } else {
    //     console.log('어른입니다');
    //   }
    // });
  &lt;/script&gt; --&gt;


  &lt;script&gt;

    $(document).ready(function () {
      let url = &quot;http://spartacodingclub.shop/sparta_api/weather/seoul&quot;;
      fetch(url).then(res =&gt; res.json()).then(data =&gt; {
        let mise = data['temp'];
        $('#msg').text(mise);
      })
    });

    function openclose() {
      $('#postingbox').toggle();
    }

    function makeCard() {
      let image = $('#image').val();
      let title = $('#title').val();
      let comment = $('#comment').val();
      let star = $('#star').val();

      let temp_html = `
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img src=&quot;${image}&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;${title}&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;${star}&lt;/p&gt;
            &lt;p class=&quot;card-text&quot;&gt;${comment}&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;Last updated 3 mins ago&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;`;

      $('#card').append(temp_html);
    }

  &lt;/script&gt;
&lt;/head&gt;

&lt;body&gt;
  &lt;header class=&quot;p-3 text-bg-dark&quot;&gt;
    &lt;div class=&quot;container&quot;&gt;
      &lt;div class=&quot;d-flex flex-wrap align-items-center justify-content-center justify-content-lg-start&quot;&gt;
        &lt;a href=&quot;/&quot; class=&quot;d-flex align-items-center mb-2 mb-lg-0 text-white text-decoration-none&quot;&gt;
          &lt;svg class=&quot;bi me-2&quot; width=&quot;40&quot; height=&quot;32&quot; role=&quot;img&quot; aria-label=&quot;Bootstrap&quot;&gt;
            &lt;use xlink:href=&quot;#bootstrap&quot;&gt;&lt;/use&gt;
          &lt;/svg&gt;
        &lt;/a&gt;

        &lt;ul class=&quot;nav col-12 col-lg-auto me-lg-auto mb-2 justify-content-center mb-md-0&quot;&gt;
          &lt;li&gt;&lt;a href=&quot;#&quot; class=&quot;nav-link px-2 text-danger&quot;&gt;홈&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href=&quot;#&quot; class=&quot;nav-link px-2 text-white&quot;&gt;시리즈&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href=&quot;#&quot; class=&quot;nav-link px-2 text-white&quot;&gt;영화&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href=&quot;#&quot; class=&quot;nav-link px-2 text-white&quot;&gt;내가 찜한 콘텐츠&lt;/a&gt;&lt;/li&gt;
          &lt;li&gt;&lt;a href=&quot;#&quot; class=&quot;nav-link px-2 text-white&quot;&gt;현재 서울의 날씨: &lt;span id=&quot;msg&quot;&gt;27&lt;/span&gt;도&lt;/a&gt;&lt;/li&gt;
        &lt;/ul&gt;

        &lt;form class=&quot;col-12 col-lg-auto mb-3 mb-lg-0 me-lg-3&quot; role=&quot;search&quot;&gt;
          &lt;input type=&quot;search&quot; class=&quot;form-control form-control-dark text-bg-dark&quot; placeholder=&quot;Search...&quot;
            aria-label=&quot;Search&quot; /&gt;
        &lt;/form&gt;

        &lt;div class=&quot;text-end&quot;&gt;
          &lt;button type=&quot;button&quot; class=&quot;btn btn-outline-light me-2&quot;&gt;
            Login
          &lt;/button&gt;
          &lt;button type=&quot;button&quot; class=&quot;btn btn-danger&quot;&gt;Sign-up&lt;/button&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/header&gt;

  &lt;div class=&quot;main&quot;&gt;
    &lt;div class=&quot;p-5 mb-4 bg-body-tertiary rounded-3&quot;&gt;
      &lt;div class=&quot;container-fluid py-5&quot;&gt;
        &lt;h1 class=&quot;display-5 fw-bold&quot;&gt;킹덤&lt;/h1&gt;
        &lt;p class=&quot;col-md-8 fs-4&quot;&gt;
          병든 왕을 둘러싸고 흉흉한 소문이 떠돈다. 어둠에 뒤덮인 조선, 기이한
          역병에 신음하는 산하. 정체 모를 악에 맞서 백성을 구원할 희망은 오직
          세자뿐이다.
        &lt;/p&gt;
        &lt;button onclick=&quot;openclose()&quot; type=&quot;button&quot; class=&quot;btn btn-outline-light&quot;&gt;
          영화 기록하기
        &lt;/button&gt;
        &lt;button type=&quot;button&quot; class=&quot;btn btn-outline-light&quot;&gt;상세정보&lt;/button&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;

  &lt;div class=&quot;mypostingbox&quot; id=&quot;postingbox&quot;&gt;
    &lt;div class=&quot;form-floating mb-3&quot;&gt;
      &lt;input type=&quot;email&quot; class=&quot;form-control&quot; id=&quot;image&quot; placeholder=&quot;영화 이미지 주소&quot; /&gt;
      &lt;label for=&quot;floatingInput&quot;&gt;영화 이미지 주소&lt;/label&gt;
    &lt;/div&gt;
    &lt;div class=&quot;form-floating mb-3&quot;&gt;
      &lt;input type=&quot;email&quot; class=&quot;form-control&quot; id=&quot;title&quot; placeholder=&quot;영화 제목&quot; /&gt;
      &lt;label for=&quot;floatingInput&quot;&gt;영화 제목&lt;/label&gt;
    &lt;/div&gt;
    &lt;div class=&quot;input-group mb-3&quot;&gt;
      &lt;label class=&quot;input-group-text&quot; for=&quot;inputGroupSelect01&quot;&gt;별점&lt;/label&gt;
      &lt;select id=&quot;star&quot; class=&quot;form-select&quot;&gt;
        &lt;option selected&gt;별점 선택&lt;/option&gt;
        &lt;option value=&quot;⭐&quot;&gt;⭐&lt;/option&gt;
        &lt;option value=&quot;⭐⭐&quot;&gt;⭐⭐&lt;/option&gt;
        &lt;option value=&quot;⭐⭐⭐&quot;&gt;⭐⭐⭐&lt;/option&gt;
        &lt;option value=&quot;⭐⭐⭐⭐&quot;&gt;⭐⭐⭐⭐&lt;/option&gt;
        &lt;option value=&quot;⭐⭐⭐⭐⭐&quot;&gt;⭐⭐⭐⭐⭐&lt;/option&gt;
      &lt;/select&gt;
    &lt;/div&gt;
    &lt;div class=&quot;form-floating mb-3&quot;&gt;
      &lt;input type=&quot;email&quot; class=&quot;form-control&quot; id=&quot;comment&quot; placeholder=&quot;추천 이유&quot; /&gt;
      &lt;label for=&quot;floatingInput&quot;&gt;추천 이유&lt;/label&gt;
    &lt;/div&gt;
    &lt;button onclick=&quot;makeCard()&quot; type=&quot;button&quot; class=&quot;btn btn-danger&quot;&gt;기록하기&lt;/button&gt;
  &lt;/div&gt;

  &lt;div class=&quot;mycards&quot;&gt;
    &lt;div id=&quot;card&quot; class=&quot;row row-cols-1 row-cols-md-4 g-4&quot;&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img src=&quot;https://movie-phinf.pstatic.net/20210728_221/1627440327667GyoYj_JPEG/movie_image.jpg&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;영화제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;⭐⭐⭐&lt;/p&gt;
            &lt;p class=&quot;card-text&quot;&gt;영화 코멘트&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;Last updated 3 mins ago&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img src=&quot;https://movie-phinf.pstatic.net/20210728_221/1627440327667GyoYj_JPEG/movie_image.jpg&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;영화제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;⭐⭐⭐&lt;/p&gt;
            &lt;p class=&quot;card-text&quot;&gt;영화 코멘트&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;Last updated 3 mins ago&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img src=&quot;https://movie-phinf.pstatic.net/20210728_221/1627440327667GyoYj_JPEG/movie_image.jpg&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;영화제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;⭐⭐⭐&lt;/p&gt;
            &lt;p class=&quot;card-text&quot;&gt;영화 코멘트&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;Last updated 3 mins ago&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
      &lt;div class=&quot;col&quot;&gt;
        &lt;div class=&quot;card h-100&quot;&gt;
          &lt;img src=&quot;https://movie-phinf.pstatic.net/20210728_221/1627440327667GyoYj_JPEG/movie_image.jpg&quot;
            class=&quot;card-img-top&quot; alt=&quot;...&quot; /&gt;
          &lt;div class=&quot;card-body&quot;&gt;
            &lt;h5 class=&quot;card-title&quot;&gt;영화제목&lt;/h5&gt;
            &lt;p class=&quot;card-text&quot;&gt;⭐⭐⭐&lt;/p&gt;
            &lt;p class=&quot;card-text&quot;&gt;영화 코멘트&lt;/p&gt;
          &lt;/div&gt;
          &lt;div class=&quot;card-footer&quot;&gt;
            &lt;small class=&quot;text-body-secondary&quot;&gt;Last updated 3 mins ago&lt;/small&gt;
          &lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/body&gt;

&lt;/html&gt;</code></pre>
<blockquote>
<p>서울온도 오픈 api에서 날씨 정보 가져와 반영하기
중간중간 변수에 담긴 데이터가 맞는지, 다중배열구조에서 틀리진 않았는지
console.log()로 틈틈이 확인해주면 좋다</p>
</blockquote>