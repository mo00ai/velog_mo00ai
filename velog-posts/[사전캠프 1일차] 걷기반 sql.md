<p>사전캠프 1일차
강의를 볼 수 없어서 과제만..</p>
<br />
<br />

<h3 id="sql-걷기반">sql 걷기반</h3>
<br />

<h3 id="1-돈을-벌기-위해-일을-합시다">1) 돈을 벌기 위해 일을 합시다!</h3>
<p>아래와 같은 sparta_employees(직원) 테이블이 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
<th>position</th>
<th>salary</th>
<th>hire_date</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>르탄이</td>
<td>개발자</td>
<td>30000</td>
<td>2022-05-01</td>
</tr>
<tr>
<td>2</td>
<td>배캠이</td>
<td>PM</td>
<td>40000</td>
<td>2021-09-25</td>
</tr>
<tr>
<td>3</td>
<td>구구이</td>
<td>파트장</td>
<td>35000</td>
<td>2023-06-01</td>
</tr>
<tr>
<td>4</td>
<td>이션이</td>
<td>팀장</td>
<td>50000</td>
<td>2021-07-09</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>sparta_employees</code></strong> 테이블에서 모든 직원의 이름(name)과 직급(position)을 선택하는 쿼리를 작성해주세요.<pre><code class="language-sql">select name, position from sparta_employees;</code></pre>
</li>
<li><strong><code>sparta_employees</code></strong> 테이블에서 중복 없이 모든 직급(position)을 선택하는 쿼리를 작성해주세요.<pre><code class="language-sql">select distinct position from sparta_employees;</code></pre>
</li>
<li><strong><code>sparta_employees</code></strong> 테이블에서 연봉(salary)이 40000과 60000 사이인 직원들을 선택하는 쿼리를 작성해주세요.<pre><code class="language-sql">select * from sparta_employees where salary between 40000 and 60000;</code></pre>
</li>
<li><strong><code>sparta_employees</code></strong> 테이블에서 입사일(hire_date)이 2023년 1월 1일 이전인 모든 직원들을 선택하는 쿼리를 작성해주세요.<pre><code class="language-sql">select * from sparta_employees where hire_date &lt; '2023-01-01';</code></pre>
</li>
</ol>
<hr />
<h3 id="2-이제-좀-벌었으니-flex-한-번-해볼까요">2) 이제 좀 벌었으니 flex 한 번 해볼까요?!</h3>
<aside>
⚡ **실제 데이터 베이스를 연결하기 전, SQL 문법을 탄탄하게 다져봅시다.**

</aside>

<p>여러분이 구매하고 싶은 상품들의 정보가 있는 products(상품) 테이블이 아래에 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>product_name</th>
<th>price</th>
<th>category</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>맥북 프로</td>
<td>1200</td>
<td>컴퓨터</td>
</tr>
<tr>
<td>2</td>
<td>다이슨 청소기</td>
<td>300</td>
<td>생활가전</td>
</tr>
<tr>
<td>3</td>
<td>갤럭시탭</td>
<td>600</td>
<td>컴퓨터</td>
</tr>
<tr>
<td>4</td>
<td>드롱기 커피머신</td>
<td>200</td>
<td>주방가전</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>products</code></strong> 테이블에서 제품 이름(product_name)과 가격(price)만을 선택하는 쿼리를 작성해주세요.<pre><code class="language-sql">select product_name, price from products;</code></pre>
</li>
<li><strong><code>products</code></strong> 테이블에서 제품 이름에 '프로'가 포함된 모든 제품을 선택하는 쿼리를 작성해주세요.<pre><code class="language-sql">select * from products where product_name like '%프로%';</code></pre>
</li>
<li><strong><code>products</code></strong> 테이블에서 제품 이름이 '갤'로 시작하는 모든 제품을 선택하는 쿼리를 작성해주세요.<pre><code class="language-sql">select * from products where product_name like '갤%';</code></pre>
</li>
<li><strong><code>products</code></strong> 테이블에서 모든 제품을 구매하기 위해 필요한 돈을 계산하는 쿼리를 작성해주세요.<pre><code class="language-sql">select sum(price) from products;</code></pre>
$\rarr$ <code>select sum(price) as total_price from products;</code></li>
</ol>
<hr />
<h3 id="3-상품-주문이-들어왔으니-주문을-처리해봅시다">3) 상품 주문이 들어왔으니 주문을 처리해봅시다!</h3>
<p>이제 상품 주문이 들어왔으니 어떤 고객에게 어떤 주문이 들어왔는지를 파악할 수 있는 orders(주문) 테이블이 아래에 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>customer_id</th>
<th>product_id</th>
<th>amount</th>
<th>shipping_fee</th>
<th>order_date</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>719</td>
<td>1</td>
<td>3</td>
<td>50000</td>
<td>2023-11-01</td>
</tr>
<tr>
<td>2</td>
<td>131</td>
<td>2</td>
<td>1</td>
<td>10000</td>
<td>2023-11-02</td>
</tr>
<tr>
<td>3</td>
<td>65</td>
<td>4</td>
<td>1</td>
<td>20000</td>
<td>2023-11-05</td>
</tr>
<tr>
<td>4</td>
<td>1008</td>
<td>3</td>
<td>2</td>
<td>25000</td>
<td>2023-11-05</td>
</tr>
<tr>
<td>5</td>
<td>356</td>
<td>1</td>
<td>1</td>
<td>15000</td>
<td>2023-11-09</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>orders</code></strong> 테이블에서 주문 수량(amount)이 2개 이상인 주문을 진행한 소비자의 ID(customer_id)만 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select customer_id from orders where amount &gt;=2;</code></pre>
</li>
<li><strong><code>orders</code></strong> 테이블에서 2023년 11월 2일 이후에 주문된 주문 수량(amount)이 2개 이상인 주문을 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select * from orders where order_date &gt; '2023-11-02' and amount &gt;= 2;</code></pre>
</li>
<li><strong><code>orders</code></strong> 테이블에서 주문 수량이 3개 미만이면서 배송비(shipping_fee)가 15000원보다 비싼 주문을 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select * from orders where amount &lt; 3 and shipping_fee &gt; 15000;</code></pre>
</li>
<li><strong><code>orders</code></strong> 테이블에서 배송비가 높은 금액 순으로 정렬하는 쿼리를 작성해주세요!<pre><code class="language-sql">select * from orders order by shipping-fee desc;</code></pre>
</li>
</ol>
<hr />
<h3 id="4-이제-놀만큼-놀았으니-다시-공부해봅시다">4) 이제 놀만큼 놀았으니 다시 공부해봅시다!</h3>
<p>아래와 같은 sparta_students(학생) 테이블이 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
<th>track</th>
<th>grade</th>
<th>enrollment_year</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>르탄이</td>
<td>Node.js</td>
<td>A</td>
<td>2023</td>
</tr>
<tr>
<td>2</td>
<td>배캠이</td>
<td>Spring</td>
<td>B</td>
<td>2022</td>
</tr>
<tr>
<td>3</td>
<td>구구이</td>
<td>Unity</td>
<td>C</td>
<td>2021</td>
</tr>
<tr>
<td>4</td>
<td>이션이</td>
<td>Node.js</td>
<td>B</td>
<td>2022</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>sparta_students</code></strong> 테이블에서 모든 학생의 이름(name)과 트랙(track)을 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select name, track from sparta_students;</code></pre>
</li>
<li><strong><code>sparta_students</code></strong> 테이블에서 Unity 트랙 소속이 아닌 학생들을 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select * from sparta_students where track != 'unity';
select * from sparta_students where track &lt;&gt; 'unity';
select * from sparta_students where not track = 'unity';</code></pre>
</li>
<li><strong><code>sparta_students</code></strong> 테이블에서 입학년도(enrollment_year)가 2021년인 학생과 2023년인 학생을 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select * from sparta_students where enrollment_year in (2021,2023);
select * from sparta_students where enrollment_year = 2021 or enrollment_year = 2023;</code></pre>
</li>
<li><strong><code>sparta_students</code></strong> 테이블에서 Node.js 트랙 소속이고 학점이 ‘A’인 학생의 입학년도를 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select enrollment_year from sparta_students where track = 'Node.js' and grad = 'A';</code></pre>
</li>
</ol>
<hr />
<h3 id="5-공부하다보니-팀-프로젝트-시간이-왔어요">5) 공부하다보니 팀 프로젝트 시간이 왔어요!</h3>
<p>공부를 한 결과를 점검하기 위해 팀 프로젝트를 수행해야 합니다! 이제, 아래와 같은 team_projects(프로젝트) 테이블이 있습니다. </p>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
<th>start_date</th>
<th>end_date</th>
<th>aws_cost</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>일조</td>
<td>2023-01-01</td>
<td>2023-01-07</td>
<td>30000</td>
</tr>
<tr>
<td>2</td>
<td>꿈꾸는이조</td>
<td>2023-03-15</td>
<td>2023-03-22</td>
<td>50000</td>
</tr>
<tr>
<td>3</td>
<td>보람삼조</td>
<td>2023-11-20</td>
<td>2023-11-30</td>
<td>80000</td>
</tr>
<tr>
<td>4</td>
<td>사조참치</td>
<td>2022-07-01</td>
<td>2022-07-30</td>
<td>75000</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>team_projects</code></strong> 테이블에서 AWS 예산(aws_cost)이 40000 이상 들어간 프로젝트들의 이름을 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select name from team_projects where aws_cost &gt; 40000;</code></pre>
</li>
<li><strong><code>team_projects</code></strong> 테이블에서 2022년에 시작된 프로젝트를 선택하는 쿼리를 작성해주세요! 단, <strong>start_date &lt; ‘2023-01-01’</strong> 조건을 <strong>사용하지 말고</strong> 쿼리를 작성해주세요!<pre><code class="language-sql">select * from team_projects where year(start_date) = 2022;</code></pre>
</li>
<li><strong><code>team_projects</code></strong> 테이블에서 현재 진행중인 프로젝트를 선택하는 쿼리를 작성해주세요. 단, 지금 시점의 날짜를 하드코딩해서 쿼리하지 말아주세요!<pre><code class="language-sql">select * from team_projects where end_date &gt; curdate();
SELECT id, name, start_date, end_date, aws_cost FROM team_projects WHERE CURDATE()  BETWEEN start_date AND end_date;</code></pre>
</li>
<li><strong><code>team_projects</code></strong> 테이블에서 각 프로젝트의 지속 기간을 일 수로 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select name, end_date - satrt date as duration from team_projects;
select name, dateiff(end_date, start_date) as duration from team_projects;</code></pre>
</li>
</ol>
<hr />
<h3 id="6-팀-프로젝트-열심히-했으니-다시-놀아볼까요">6) 팀 프로젝트 열심히 했으니 다시 놀아볼까요?!</h3>
<p>아래와 같은 lol_users(LOL 유저 테이블)이 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
<th>region</th>
<th>rating</th>
<th>join_date</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>르탄이</td>
<td>한국</td>
<td>1300</td>
<td>2019-06-15</td>
</tr>
<tr>
<td>2</td>
<td>배캠이</td>
<td>미국</td>
<td>1500</td>
<td>2020-09-01</td>
</tr>
<tr>
<td>3</td>
<td>구구이</td>
<td>한국</td>
<td>1400</td>
<td>2021-01-07</td>
</tr>
<tr>
<td>4</td>
<td>이션이</td>
<td>미국</td>
<td>1350</td>
<td>2019-11-15</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>lol_users</code></strong> 테이블에서 각 유저의 레이팅(rating) 순위를 계산하는 쿼리를 작성해주세요! 전체 지역(region) 기준이고 순위는 레이팅이 높을수록 높아야해요. (e.g. rating 1400 유저의 순위 &gt; rating 1350 유저의 순위)<pre><code class="language-sql">oracle subqeury 이용
select rownum as rank, t.* from (select * from lol_users order by rating desc) t;</code></pre>
<pre><code class="language-sql">mysql 
select *, row_number() over (order by rating desc) as rank from lol_users;</code></pre>
</li>
<li><strong><code>lol_users</code></strong> 테이블에서 가장 늦게 게임을 시작한(join_date) 유저의 이름을 선택하는 쿼리를 작성해주세요<pre><code class="language-sql">select name from lol_users where join_date = (select max(join_date) from lol_users);
select name from lol_users order by join_date desc limit 1;</code></pre>
</li>
<li><strong><code>lol_users</code></strong> 테이블에서 지역별로 레이팅이 높은 순으로 유저들을 정렬해서 나열하는 쿼리를 작성해주세요!<pre><code class="language-sql">select row_number() over(partition by region order by rating desc) as rank, * from team_projects;
SELECT id, name, region, rating, join_date FROM lol_users ORDER BY region, rating DESC;</code></pre>
</li>
<li><strong><code>lol_users</code></strong> 테이블에서 지역별로 평균 레이팅을 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select region, avg(rating) as region avg from lol_users group by region;</code></pre>
</li>
</ol>
<hr />
<h3 id="7-랭크게임-하다가-싸워서-피드백-남겼어요">7) 랭크게임 하다가 싸워서 피드백 남겼어요…</h3>
<p>아래와 같은 lol_feedbacks (LOL 피드백 테이블)이 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>user_name</th>
<th>satisfaction_score</th>
<th>feedback_date</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>르탄이</td>
<td>5</td>
<td>2023-03-01</td>
</tr>
<tr>
<td>2</td>
<td>배캠이</td>
<td>4</td>
<td>2023-03-02</td>
</tr>
<tr>
<td>3</td>
<td>구구이</td>
<td>3</td>
<td>2023-03-01</td>
</tr>
<tr>
<td>4</td>
<td>이션이</td>
<td>5</td>
<td>2023-03-03</td>
</tr>
<tr>
<td>5</td>
<td>구구이</td>
<td>4</td>
<td>2023-03-04</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>lol_feedbacks</code></strong> 테이블에서 만족도 점수(satisfaction_score)에 따라 피드백을 내림차순으로 정렬하는 쿼리를 작성해주세요!<pre><code class="language-sql">select * from lol_feedbacks order by satisfaction_score desc;</code></pre>
</li>
<li><strong><code>lol_feedbacks</code></strong> 테이블에서 각 유저별로 최신 피드백을 찾는 쿼리를 작성해주세요!<pre><code class="language-sql">select id, user_name,satisfaction_score, max(feedback_date) from lol_feedbacks group by user_name;
</code></pre>
</li>
</ol>
<pre><code>3. **`lol_feedbacks`** 테이블에서 만족도 점수가 5점인 피드백의 수를 계산하는 쿼리를 작성해주세요!
```sql
select count(*) from lol_feedbacks where sactisfaction_score = 5;</code></pre><ol start="4">
<li><strong><code>lol_feedbacks</code></strong> 테이블에서 가장 많은 피드백을 남긴 상위 3명의 고객을 찾는 쿼리를 작성해주세요!<pre><code class="language-sql">select user_name, count(*) as feedback_cnt from lol_feedbacks group by user_name order by feedback_cnt desc limit 3; </code></pre>
</li>
<li><strong><code>lol_feedbacks</code></strong> 테이블에서 평균 만족도 점수가 가장 높은 날짜를 찾는 쿼리를 작성해주세요!<pre><code class="language-sql">select feedback_date from lol_feedbacks group by feedback_date order by avg(satisfaction_score) desc limit 1;</code></pre>
</li>
</ol>
<hr />
<h3 id="8-lol을-하다가-홧병이-나서-병원을-찾아왔습니다"><strong>8) LOL을 하다가 홧병이 나서 병원을 찾아왔습니다.</strong></h3>
<p>이제, 아래와 같은 doctors(의사) 테이블이 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
<th>major</th>
<th>hire_date</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>르탄이</td>
<td>피부과</td>
<td>2018-05-10</td>
</tr>
<tr>
<td>2</td>
<td>배캠이</td>
<td>성형외과</td>
<td>2019-06-15</td>
</tr>
<tr>
<td>3</td>
<td>구구이</td>
<td>안과</td>
<td>2020-07-20</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>doctors</code></strong> 테이블에서 전공(major)가 성형외과인 의사의 이름을 알아내는 쿼리를 작성해주세요!<pre><code class="language-sql">select name from doctos where major = '성형외과';</code></pre>
</li>
<li><strong><code>doctors</code></strong> 테이블에서 각 전공 별 의사 수를 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select count(*) from doctors group by major;</code></pre>
</li>
<li><strong><code>doctors</code></strong> 테이블에서 현재 날짜 기준으로 5년 이상 근무(hire_date)한 의사 수를 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select count(*) from doctors where year(date_sub(hire_date, curdate())); -- 틀림
select count(*) from doctors where datediff(curdate(), hire_date) &gt;= 5*365;
select count(*) as num_of_doctors from doctors where hire_date &lt;= date_sub(curdate(),interval 5 year) ;</code></pre>
</li>
<li><strong><code>doctors</code></strong> 테이블에서 각 의사의 근무 기간을 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select *, dateiff(curdate(), hire_date) as duration from doctors;</code></pre>
</li>
</ol>
<hr />
<h3 id="9아프면-안됩니다-항상-건강-챙기세요">9)아프면 안됩니다! 항상 건강 챙기세요!</h3>
<p>의사가 있으면 당연히 의사에게 진료받는 환자가 있겠죠? 아래와 같은 patients(환자) 테이블이 있습니다.</p>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
<th>birth_date</th>
<th>gender</th>
<th>last_visit_date</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>르탄이</td>
<td>1985-04-12</td>
<td>남자</td>
<td>2023-03-15</td>
</tr>
<tr>
<td>2</td>
<td>배캠이</td>
<td>1990-08-05</td>
<td>여자</td>
<td>2023-03-20</td>
</tr>
<tr>
<td>3</td>
<td>구구이</td>
<td>1982-12-02</td>
<td>여자</td>
<td>2023-02-18</td>
</tr>
<tr>
<td>4</td>
<td>이션이</td>
<td>1999-03-02</td>
<td>남자</td>
<td>2023-03-17</td>
</tr>
</tbody></table>
<ol>
<li><strong><code>patients</code></strong> 테이블에서 각 성별(gender)에 따른 환자 수를 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select gender, count(*) from patients group by gender;</code></pre>
</li>
<li><strong><code>patients</code></strong> 테이블에서 현재 나이가 40세 이상인 환자들의 수를 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select count(*) from patients where datediff(curdate(), birth_date) &gt;= 40*365;
select count(*) from patients where birth_date &lt;= date_sub(curdate(), interval 40 year);</code></pre>
</li>
<li><strong><code>patients</code></strong> 테이블에서 마지막 방문 날짜(last_visit_date)가 1년 이상 된 환자들을 선택하는 쿼리를 작성해주세요!<pre><code class="language-sql">select * from patients where last_visit_date &lt;= date_sub(curdate(), interval 1 year);</code></pre>
</li>
<li><strong><code>patients</code></strong> 테이블에서 생년월일이 1980년대인 환자들의 수를 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select count(*) from patients where birth_date between '1980-01-01' and '1989-12-31';</code></pre>
</li>
</ol>
<hr />
<h3 id="10-이젠-테이블이-2개입니다">10) 이젠 테이블이 2개입니다</h3>
<p>다음과 같은 직원(employees) 테이블과 부서(departments) 테이블이 있습니다.</p>
<ul>
<li>employees 테이블</li>
</ul>
<table>
<thead>
<tr>
<th>id</th>
<th>department_id</th>
<th>name</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>101</td>
<td>르탄이</td>
</tr>
<tr>
<td>2</td>
<td>102</td>
<td>배캠이</td>
</tr>
<tr>
<td>3</td>
<td>103</td>
<td>구구이</td>
</tr>
<tr>
<td>4</td>
<td>101</td>
<td>이션이</td>
</tr>
</tbody></table>
<ul>
<li>departments 테이블</li>
</ul>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
</tr>
</thead>
<tbody><tr>
<td>101</td>
<td>인사팀</td>
</tr>
<tr>
<td>102</td>
<td>마케팅팀</td>
</tr>
<tr>
<td>103</td>
<td>기술팀</td>
</tr>
</tbody></table>
<ol>
<li>현재 존재하고 있는 총 부서의 수를 구하는 쿼리를 작성해주세요!<pre><code class="language-sql">select count(*) from departments;</code></pre>
</li>
<li>모든 직원과 그들이 속한 부서의 이름을 나열하는 쿼리를 작성해주세요!
``` sql
select </li>
</ol>
<p>*
from employees e
inner join departments d
on e.department_id = d.id;</p>
<pre><code>3. '기술팀' 부서에 속한 직원들의 이름을 나열하는 쿼리를 작성해주세요!
``` sql
select 
e.name
from employees e
inner join departments d
on e.department_id = d.id
where d.name = '기술팀';</code></pre><ol start="4">
<li>부서별로 직원 수를 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select 
d.name,
count(*)
from employees e
inner join departments d
on e.department_id = d.id
group by d.name;
</code></pre>
</li>
</ol>
<p>SELECT d.name, COUNT(e.id) AS employee_count FROM departments d LEFT JOIN employees e ON d.id = e.department_id GROUP BY d.id;</p>
<pre><code>5. 직원이 없는 부서의 이름을 찾는 쿼리를 작성해주세요!
``` sql
select 
d.name
from employees e
right join departments d
on e.department_id = d.id
where e.name is null;</code></pre><ol start="6">
<li>'마케팅팀' 부서에만 속한 직원들의 이름을 나열하는 쿼리를 작성해주세요!<pre><code class="language-sql">select 
e.name,
d.name
from employees e
inner join departments d
on e.department_id = d.id
where d.name = '마케팅팀';</code></pre>
</li>
</ol>
<hr />
<h3 id="마지막--연습-문제-">마지막  연습 문제 !</h3>
<p>다음과 같은 상품(products) 테이블과 주문(orders) 테이블이 있습니다.</p>
<ul>
<li>products 테이블</li>
</ul>
<table>
<thead>
<tr>
<th>id</th>
<th>name</th>
<th>price</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>랩톱</td>
<td>1200</td>
</tr>
<tr>
<td>2</td>
<td>핸드폰</td>
<td>800</td>
</tr>
<tr>
<td>3</td>
<td>타블렛</td>
<td>400</td>
</tr>
<tr>
<td>- orders 테이블</td>
<td></td>
<td></td>
</tr>
</tbody></table>
<table>
<thead>
<tr>
<th>id</th>
<th>product_id</th>
<th>quantity</th>
<th>order_date</th>
</tr>
</thead>
<tbody><tr>
<td>101</td>
<td>1</td>
<td>2</td>
<td>2023-03-01</td>
</tr>
<tr>
<td>102</td>
<td>2</td>
<td>1</td>
<td>2023-03-02</td>
</tr>
<tr>
<td>103</td>
<td>3</td>
<td>5</td>
<td>2023-03-04</td>
</tr>
</tbody></table>
<ol>
<li>모든 주문의 주문 ID와 주문된 상품의 이름을 나열하는 쿼리를 작성해주세요!<pre><code class="language-sql">select
o.id,
p.id,
p.name
from products p
inner join orders o
on p.id = o.product_id;</code></pre>
</li>
<li>총 매출(price * quantity의 합)이 가장 높은 상품의 ID와 해당 상품의 총 매출을 가져오는 쿼리를 작성해주세요!<pre><code class="language-sql">select
p.id,
sum(p.price*o.quentity) as total_sales
from products p
inner join orders o
on p.id = o.product_id
group p.id
order by total_sales desc limit 1;</code></pre>
</li>
<li>각 상품 ID별로 판매된 총 수량(quantity)을 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select
p.id
sum(o.quantity)
from products p
inner join orders o
on p.id = o.product_id
group by p.id;</code></pre>
</li>
<li>2023년 3월 3일 이후에 주문된 모든 상품의 이름을 나열하는 쿼리를 작성해주세요!<pre><code class="language-sql">select
p.name,
o.order_date
from products p
inner join orders o
on p.id = o.product_id
where order_date &gt;= '2023-03-03';</code></pre>
</li>
<li>가장 많이 판매된 상품의 이름을 찾는 쿼리를 작성해주세요!<pre><code class="language-sql">select
p.name,
sum(o.quantity) as total_amount
from products p
inner join orders o
on p.id = o.product_id
group by p.name
order by total_amount desc limit 1;</code></pre>
</li>
<li>각 상품 ID별로 평균 주문 수량을 계산하는 쿼리를 작성해주세요!<pre><code class="language-sql">select
p.id,
avg(p.quantity)
from products p
inner join orders o
on p.id = o.product_id
group by p.id;</code></pre>
</li>
<li>판매되지 않은 상품의 ID와 이름을 찾는 쿼리를 작성해주세요!<pre><code class="language-sql">p.id,
p.name
from products p
left join orders o
on p.id = o.product_id
where o.id is null;</code></pre>
</li>
</ol>