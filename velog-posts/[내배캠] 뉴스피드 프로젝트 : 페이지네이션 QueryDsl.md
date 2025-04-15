<h1 id="페이지네이션">페이지네이션</h1>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/7856fe2e-952d-438a-8662-58950aeab9c1/image.png" /></p>
<p>게시글 전체 목록 조회의 RequestParam으로 3가지 조건이 옴</p>
<ol>
<li>제목 검색</li>
<li>팔로잉한 사람들 게시글 조회</li>
<li>페이지 검색</li>
</ol>
<p>조건들을 따로 입력 안 할 경우엔 RequestParam은 null값이 들어감</p>
<h2 id="1-service에서-조건에-따라-다른-jparepository-메서드-호출---하드코딩">1. service에서 조건에 따라 다른 JPArepository 메서드 호출 - 하드코딩</h2>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/91e4de3b-6ba1-4354-a5bd-0068e77dd3b0/image.png" /></p>
<p>board service 각 조건에 따른 repository를 호출</p>
<pre><code class="language-java">   @Query(value = &quot;SELECT new com.example.sns_feed.domain.board.dto.response.BoardPageResponseDto( &quot; +
           &quot; b.id, u.userName, b.title, COUNT(c.comment_id), b.updatedAt ) &quot; +
           &quot;FROM Board b &quot; +
           &quot;JOIN b.user u &quot; +
           &quot;LEFT JOIN Comment c ON c.board.id = b.id &quot; +
           &quot;GROUP BY b.id&quot;,

               countQuery = &quot;select count(b) from Board b&quot;)
   Page&lt;BoardPageResponseDto&gt; findBoardPageWithCommentCount(Pageable pageable);

   @Query(value = &quot;SELECT new com.example.sns_feed.domain.board.dto.response.BoardPageResponseDto( &quot; +
           &quot; b.id, u.userName, b.title, COUNT(c.comment_id), b.updatedAt ) &quot; +
           &quot;FROM Board b &quot; +
           &quot;JOIN b.user u &quot; +
           &quot;LEFT JOIN Comment c ON c.board.id = b.id &quot; +
           &quot;WHERE b.title LIKE CONCAT('%', :titleSearch, '%') &quot; +
           &quot;GROUP BY b.id, u.userName, b.title, b.updatedAt&quot;,

           countQuery =  &quot;SELECT COUNT(b) FROM Board b WHERE b.title LIKE CONCAT('%', :titleSearch, '%')&quot;)
   Page&lt;BoardPageResponseDto&gt; findSearchBoardPageWithCommentCount(@Param(&quot;titleSearch&quot;) String titleSearch, Pageable pageable);

   @Query(value = &quot;SELECT new com.example.sns_feed.domain.board.dto.response.BoardPageResponseDto(&quot; +
           &quot;b.id, u.userName, b.title, COUNT(c.comment_id), b.updatedAt) &quot; +
           &quot;FROM Board b &quot; +
           &quot;JOIN b.user u &quot; +
           &quot;JOIN Comment c ON c.comment_id = u.id &quot; +
           &quot;JOIN Follow f ON f.receiver.id = u.id&quot;+
           &quot; GROUP BY b.id&quot;,

           countQuery =  &quot;SELECT COUNT(b) FROM Board b JOIN b.user u JOIN Follow f ON f.receiver.id = u.id&quot;)
   Page&lt;BoardPageResponseDto&gt; findFollowingBoardPageWithCommentCount(Pageable pageable);



   @Query(value = &quot;SELECT new com.example.sns_feed.domain.board.dto.response.BoardPageResponseDto(&quot; +
           &quot;b.id, u.userName, b.title, COUNT(c.comment_id), b.updatedAt) &quot; +
           &quot;FROM Board b &quot; +
           &quot;JOIN b.user u &quot; +
           &quot;JOIN Comment c ON c.comment_id = u.id &quot; +
           &quot;JOIN Follow f ON f.receiver.id = u.id &quot;+
           &quot;WHERE b.title LIKE CONCAT('%', :titleSearch, '%') &quot; +
           &quot; GROUP BY b.id&quot;,

           countQuery =  &quot;SELECT COUNT(b) FROM Board b JOIN b.user u JOIN Follow f ON f.receiver.id = u.id WHERE b.title LIKE CONCAT('%', :titleSearch, '%')&quot;)
   Page&lt;BoardPageResponseDto&gt; findSerachFollowingPageWithCommentCount(@Param(&quot;titleSearch&quot;) String titleSearch, Pageable pageable);


   @Query(value = &quot;SELECT new com.example.sns_feed.domain.board.dto.response.BoardLikeResponseDto( &quot; +
       &quot; b.id, u.userName, b.title, COUNT(c.comment_id), b.updatedAt ) &quot; +
       &quot;FROM Board b &quot; +
       &quot;JOIN b.user u &quot; +
       &quot;LEFT JOIN Comment c ON c.board.id = b.id &quot; +
       &quot;WHERE b.title LIKE CONCAT('%', :titleSearch, '%') &quot; +
       &quot;GROUP BY b.id, u.userName, b.title, b.updatedAt&quot;,
   BoardResponseDto findByIdWithLikeCount(Long idWithLikeCount);</code></pre>
<br />

<p>JPA Repository의 JPQL(@Query)로 직접 쿼리 작성</p>
<p>🤔왜 이렇게 했나?</p>
<blockquote>
<ul>
<li>JPA의 메서드 쿼리 메서드(findBy~)만으로는 복잡한 join 처리나 원하는 컬럼만 조회하기 어려움</li>
</ul>
</blockquote>
<ul>
<li>특정 컬럼만 조회하려면 DTO Projection이 필요한데, 이를 QueryDSL 없이 간단하게 처리하기 위해 JPQL 사용</li>
<li>JPQL은 SQL과 유사하게 원하는 컬럼, 조건, join 등을 유연하게 작성 가능</li>
</ul>
<p>❌튜터님 피드백
: 너무 하드코딩이다.
  JDBD의 String Builder를 사용해서 동적 쿼리를 작성해라
  동적 쿼리를 작성하는 방법은</p>
<ol>
<li>QueryDsl</li>
<li>JDBCtemplate</li>
</ol>
<blockquote>
<p>내가 생각하기에도 하드코딩이라 생각되었음
애초에 JPQL이 일반 쿼리문이랑 구조가 다르기도 하고 결국엔 where절만 바꾸면 되는건데 그 외에 select문을 모두 반복해서 코딩하니까 너무 힘들었음..</p>
</blockquote>
<blockquote>
<p>그래서 여기서 바로 QueryDSL로 넘어가면 좋았겠지만 나, 뻘짓의 왕은 또 말을 잘못 알아듣고
JDBCtemplate으로 페이지네이션을 만들었다^^</p>
</blockquote>
<br />

<hr />
<h2 id="2-jdbctemplate으로-페이징-구현---취지에-어긋남">2. JDBCtemplate으로 페이징 구현 - 취지에 어긋남</h2>
<pre><code class="language-java">   public Page&lt;BoardPageResponseDto&gt; findAllPage(Long id,String titleSearch, Boolean isFollowingBoard, Pageable pageable) {

       StringBuilder querySql = new StringBuilder(
           &quot;select &quot; +
                   &quot;    b.id,&quot; +
                   &quot;    u.user_name,&quot; +
                   &quot;    b.title,&quot; +
                   &quot;    (select&quot; +
                   &quot;         COUNT(c.user_id)&quot; +
                   &quot;     from boards bb&quot; +
                   &quot;              inner join users u on b.user_id = u.id&quot; +
                   &quot;              left join comments c on c.board_id = b.id&quot; +
                   &quot;     where bb.id  = b.id&quot; +
                   &quot;     group by b.id) as comment_count,&quot; +
                   &quot;    b.updated_at,&quot; +
                   &quot;    COUNT(*) OVER() AS total_count&quot; +
                   &quot; from boards b&quot; +
                   &quot;         inner join users u on b.user_id = u.id&quot; +
                   &quot;         left join follows f on b.user_id = f.receiver &quot;
       );

       List&lt;Object&gt; params = new ArrayList&lt;&gt;();

       if( titleSearch!=null) {
           querySql.append(&quot;where title like ? &quot;);
           params.add(&quot;%&quot; + titleSearch + &quot;%&quot;);
       }

       if(isFollowingBoard) {
           if(titleSearch!=null) {
               querySql.append(&quot;and f.follow_status = 'ACCEPTED' and  f.sender = ? &quot;);
           } else {
               querySql.append(&quot;where f.follow_status = 'ACCEPTED' and  f.sender = ? &quot;);
           }
           params.add(id);
       }

       querySql.append(&quot;order by updated_at desc &quot;);

       querySql.append(&quot;limit ? offset ?&quot;);
       params.add(pageable.getPageSize());
       params.add(pageable.getPageSize()* pageable.getPageNumber());


       return jdbcTemplate.query(querySql.toString(), rs -&gt; {
           List&lt;BoardPageResponseDto&gt; pageBoardList = new ArrayList&lt;&gt;();
           int total = 0;
           while(rs.next()) {
               if(total==0) {
                   total = rs.getInt(&quot;total_count&quot;);
               }
               BoardPageResponseDto pageResponseDto = new BoardPageResponseDto(
                       rs.getLong(&quot;id&quot;),
                       rs.getString(&quot;user_name&quot;),
                       rs.getString(&quot;title&quot;),
                       rs.getLong(&quot;comment_count&quot;),
                       rs.getTimestamp(&quot;updated_at&quot;).toLocalDateTime()
               );
               pageBoardList.add(pageResponseDto);
           }
           return new PageImpl&lt;&gt;(pageBoardList, pageable,total);
       },params.toArray());
   }</code></pre>
<br />

<blockquote>
<p>JDBCtemplate으로 구현한 페이지네이션</p>
</blockquote>
<p>이를 구현하면서도 고민했던 부분이 있다.</p>
<p>🤔 Page 객체? Slice 객체?</p>
<blockquote>
<p>Page 객체에 공부하던 도중 Slice 객체에 대해서도 접하게 되었다
SNS 프로젝트이기 때문에 각 페이지 정보를 제공하는 Page보다는 무한 스크롤에 적합한 Slice객체가 적합하지 않을까 했지만
프로젝트 취지 자체가 Page에 익숙해지기 위함이고, 우리는 웹 백엔드 부트캠프이기 때문에 취지에 어긋난다 생각하여 Page 객체를 구현하기로 했다.
<del>그건 생각해냈으면서 왜 JDBC로 구현해서 시간낭비를 막진 못했는지..</del></p>
</blockquote>
<p>❌ 튜터님께 찾아봬서 동적 쿼리 때문에 JDBC로 페이징을 구현했다하니 당황하심이 물씬 느껴져서 아 이거 QueryDsl로 구현해야겠다 하고 바로 ...구현에 들어갔다.</p>
<br />

<hr />
<br />

<h2 id="3-querydsl로-페이징-구현---채택">3. QueryDsl로 페이징 구현 - 채택</h2>
<br />

<p>QueryDsl을 사용하기 위해선 먼저 기초작업이 필요하다</p>
<hr />
<p>build.gradle dependencies에 의존성 주입</p>
<pre><code class="language-java">//QueryDsl
implementation 'com.querydsl:querydsl-jpa:5.0.0:jakarta'
annotationProcessor &quot;com.querydsl:querydsl-apt:${dependencyManagement.importedProperties['querydsl.version']}:jakarta&quot;
annotationProcessor &quot;jakarta.annotation:jakarta.annotation-api&quot;
annotationProcessor &quot;jakarta.persistence:jakarta.persistence-api&quot;</code></pre>
<hr />
<p>QueryConfig 클래스 생성</p>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/07f65712-db9c-4d98-a977-40cd610e0d19/image.png" /></p>
<p>의존성 주입을 해야 사용 가능하다</p>
<hr />
<p>QueryDsl 인터페이스 생성, 메서드 정리를 한다</p>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/da951edb-0a53-4b08-9d67-4e14cf68bb97/image.png" /></p>
<p>✅ &quot;QueryDSL 인터페이스를 따로 만드는 이유&quot;
📌 사용자 정의 레포지토리 기능(Custom Repository)
→ Spring Data JPA는 기본 Repository 외에 직접 QueryDSL로 구현한 메서드를 넣으려면
Custom 인터페이스 + 구현 클래스 구조를 따라야 함</p>
<pre><code class="language-java">// 1. 사용자 정의 인터페이스
public interface BoardRepositoryCustom {
    Page&lt;BoardPageResponseDto&gt; findBoardsPage(...);
}

// 2. 인터페이스 구현체
@Repository
public class BoardRepositoryImpl implements BoardRepositoryCustom {
    @Override
    public Page&lt;BoardPageResponseDto&gt; findBoardsPage(...) {
        // QueryDSL 로직 작성
    }
}

// 3. JPA Repository에서 상속
public interface BoardRepository extends JpaRepository&lt;Board, Long&gt;, BoardRepositoryCustom {
    // 기본 JPA + QueryDSL 메서드 둘 다 사용 가능
}</code></pre>
<table>
<thead>
<tr>
<th>이유</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><strong>역할 분리</strong></td>
<td><code>JPA 기본 기능</code>과 <code>복잡한 커스텀 쿼리(QueryDSL)</code>를 <strong>명확히 나눌 수 있음</strong></td>
</tr>
<tr>
<td><strong>Spring Data JPA 규칙</strong></td>
<td>직접 구현한 쿼리는 <code>RepositoryImpl</code>이란 <strong>정해진 네이밍 규칙</strong>을 따라야 인식됨</td>
</tr>
<tr>
<td><strong>확장성</strong></td>
<td>나중에 QueryDSL → MyBatis 바꿀 때도 구조 변경 없이 구현체만 바꾸면 됨</td>
</tr>
</tbody></table>
<blockquote>
<p>요약:
Spring Data JPA에서 QueryDSL을 사용하려면,
Custom 인터페이스 + 구현 클래스 구조를 따르는 것이 표준 방식이다.</p>
</blockquote>
<br />

<hr />
<br />

<p>실제 QueryDsl을 구현할 <code>BoardRepositoryCustom</code>에서 사용할 Q클래스들을 import 해줘야한다</p>
<h2 id="✅-querydsl-q클래스-import-이유-정리">✅ QueryDSL Q클래스 import 이유 정리</h2>
<h3 id="q클래스란">Q클래스란?</h3>
<ul>
<li>QueryDSL이 자동으로 생성해주는 <strong>Entity 전용 Query 객체</strong></li>
<li>보통 <code>Q + Entity명</code> 형태로 만들어짐<br />(ex) <code>QBoard</code>, <code>QUser</code>, <code>QComment</code> 등</li>
</ul>
<hr />
<h3 id="왜-import-해서-써야함">왜 import 해서 써야함?</h3>
<table>
<thead>
<tr>
<th>이유</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>1. 타입 안정성</td>
<td>Entity 필드를 문자열이 아닌 객체 기반으로 사용 → 컴파일러가 검증해줌</td>
</tr>
<tr>
<td>2. 자동완성 지원</td>
<td>필드 이름 오타 방지, 개발 편의성 증가</td>
</tr>
<tr>
<td>3. 가독성 ↑</td>
<td>복잡한 join이나 조건문 작성 시 SQL-like한 문법 지원</td>
</tr>
</tbody></table>
<hr />
<h3 id="예시">예시</h3>
<pre><code class="language-java">import static com.example.sns_feed.domain.board.entity.QBoard.board;

queryFactory
    .select(board)
    .from(board)
    .where(board.id.eq(1L))
    .fetch();</code></pre>
<p align="center"><img src="https://velog.velcdn.com/images/mo00ai/post/801da7a0-dfdc-4369-bc1f-714d0f294259/image.png" width="60%" /></p>

<blockquote>
<p>프로젝트 build 에서 import 후 Q클래스들이 생긴 것을 확인할 수 있다</p>
</blockquote>
<hr />
<br />

<p>해당 메서드가 반환할 responseDto도 Q 클래스로 등록해줘야한다.</p>
<pre><code class="language-java">@Getter
public class BoardPageResponseDto {

    private final Long id;

    private final String userName;

    private final String title;

    private final Long commentCount;

    private final Long likeCount;

    @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = &quot;yyyy-MM-dd HH:mm:ss&quot;)
    private final LocalDateTime updatedAt;

    @QueryProjection
    public BoardPageResponseDto(Long id, String userName, String title, Long commentCount, Long likeCount, LocalDateTime updatedAt) {
        this.id = id;
        this.userName = userName;
        this.title = title;
        this.commentCount = commentCount;
        this.likeCount = likeCount;
        this.updatedAt = updatedAt;
    }
}
</code></pre>
<p>사용할 dto의 생성자에 @QueryProjection을 달아준다
DTO에 @QueryProjection을 붙이면
→ QueryDSL이 컴파일 타임에 Q클래스를 생성해줌
→ 이걸 통해 DTO를 타입 안정성 있게 select new 대신 사용 가능하다</p>
<br />

<hr />
<br />

<h3 id="실제-querydsl-코드">실제 QueryDsl 코드</h3>
<pre><code class="language-java">@RequiredArgsConstructor
public class BoardRepositoryImpl implements BoardRepositoryCustom{

    private final JPAQueryFactory queryFactory;

    @Override
    public Page&lt;BoardPageResponseDto&gt; findBoardsPage(Long id, String titleSearch, Boolean isFollowingBoard, Pageable pageable) {


        //전체 페이지 조회 sql
        List&lt;BoardPageResponseDto&gt; boardPageResponseDtoList = queryFactory
                .select(new QBoardPageResponseDto(
                        board.id,
                        user.userName,
                        board.title,
                        JPAExpressions.select(comment.count())
                                .from(comment)
                                .where(comment.board.id.eq(board.id)),
                        JPAExpressions.select(boardLike.count().coalesce(0L))
                                .from(boardLike)
                                .where(boardLike.board.id.eq(board.id)),
                        board.updatedAt
                ))
                .from(board)
                .innerJoin(board.user, user)
                .leftJoin(follow).on(board.user.id.eq(follow.receiver.id))
                .where(
                    titleLike(titleSearch),
                    isFollowing(isFollowingBoard, id)
                )
                .groupBy(board.id,board.user.id,user.userName,board.title,board.updatedAt)
                .orderBy(board.updatedAt.desc())
                .offset(pageable.getOffset())
                .limit(pageable.getPageSize())
                .fetch();


        //전체 페이지 게시글 개수
        Long total = queryFactory
                .select(board.countDistinct())
                .from(board)
                .leftJoin(board.user, user)
                .leftJoin(follow).on(board.user.id.eq(follow.receiver.id))
                .where(
                    titleLike(titleSearch),
                    isFollowing(isFollowingBoard, id)
                )
                .fetchOne();

        if (total == null) {
            total = 0L;
        }

        return new PageImpl&lt;&gt;(boardPageResponseDtoList,pageable,total);
    }

    //검색 where조건
    private BooleanExpression titleLike(String titleSearch) {
        return titleSearch != null ? board.title.like(&quot;%&quot;+titleSearch+&quot;%&quot;) : null;
    }

    //팔로우 where boolean 조건
    private BooleanExpression isFollowing(boolean isFollowingBoard, Long id) {
        System.out.println(&quot;booleanExpression &quot;+isFollowingBoard);
        if(!isFollowingBoard) {
            System.out.println(&quot;booleanExpression 조건문 &quot;+isFollowingBoard);
            return null;
        }
        return follow.sender.id.eq(id).and(follow.followStatus.eq(FollowStatus.ACCEPTED));
    }

}</code></pre>
<br />

<ul>
<li><code>JPAQueryFactory</code>는 QueryDSL에서 쿼리를 작성하고 실행할 수 있게 도와주는 핵심 객체다.</li>
<li>스프링에선 <code>EntityManager</code>를 주입받아 <code>JPAQueryFactory</code>를 생성하고, 이를 통해 쿼리를 날릴 수 있다</li>
</ul>
<hr />
<h3 id="하나씩-뜯어먹어보자">하나씩 뜯어먹어보자!</h3>
<p>기본 메서드는 일반 sql dml과 똑같기 때문에 설명하지 않겠다.</p>
<hr />
<p><code>JPAExpressions</code></p>
<blockquote>
<p>서브쿼리를 작성할 때 사용하는 QueryDSL 전용 도구 (ex. <code>SELECT (subquery)</code>)</p>
</blockquote>
<pre><code class="language-java">JPAExpressions.select(comment.count())
                                .from(comment)
                                .where(comment.board.id.eq(board.id))</code></pre>
<hr />
<p><code>BooleanExpressions</code></p>
<blockquote>
<p><code>where()</code> 절에서 조건을 조합할 때 사용하는 불리언 조건 객체 (ex. <code>조건1.and(조건2)</code>)</p>
</blockquote>
<pre><code class="language-java">    //검색 where조건
    private BooleanExpression titleLike(String titleSearch) {
        return titleSearch != null ? board.title.like(&quot;%&quot;+titleSearch+&quot;%&quot;) : null;
    }

    //팔로우 where boolean 조건
    private BooleanExpression isFollowing(boolean isFollowingBoard, Long id) {
        System.out.println(&quot;booleanExpression &quot;+isFollowingBoard);
        if(!isFollowingBoard) {
            System.out.println(&quot;booleanExpression 조건문 &quot;+isFollowingBoard);
            return null;
        }
        return follow.sender.id.eq(id).and(follow.followStatus.eq(FollowStatus.ACCEPTED));
    }</code></pre>
<pre><code class="language-java">//실제 사용
                .select(new QBoardPageResponseDto(
                        board.id,
                        user.userName,
                        board.title,
                        JPAExpressions.select(comment.count())
                                .from(comment)
                                .where(comment.board.id.eq(board.id)),
                        JPAExpressions.select(boardLike.count().coalesce(0L))
                                .from(boardLike)
                                .where(boardLike.board.id.eq(board.id)),
                        board.updatedAt
                ))
                .from(board)
                .innerJoin(board.user, user)
                .leftJoin(follow).on(board.user.id.eq(follow.receiver.id))
                .where(
                    titleLike(titleSearch),
                    isFollowing(isFollowingBoard, id)
                )</code></pre>
<blockquote>
<p>Boolean객체는 return값이 null일땐 아예 조건이 사라진다</p>
</blockquote>
<pre><code class="language-java">.where(
    titleLike(titleSearch),
    isFollowing(isFollowingBoard, id)
)</code></pre>
<blockquote>
<p>두 조건이 null이 아닐 땐 이렇게 두 개 다 들어오지만 
⚠️만약에 titleLike return 값이 null 이라면?</p>
</blockquote>
<pre><code class="language-java">.where(
    isFollowing(isFollowingBoard, id)
)</code></pre>
<blockquote>
<p>요래됩니다?</p>
</blockquote>
<hr />
<p><strong>내가 저지른 뻘짓2..</strong></p>
<pre><code class="language-java">        //전체 페이지 게시글 개수
        Long total = queryFactory
                .select(board.countDistinct())
                .from(board)
                .leftJoin(board.user, user)
                .leftJoin(follow).on(board.user.id.eq(follow.receiver.id))
                .where(
                    titleLike(titleSearch),
                    isFollowing(isFollowingBoard, id)
                )
                .fetchOne();

        if (total == null) {
            total = 0L;
        }

        return new PageImpl&lt;&gt;(boardPageResponseDtoList,pageable,total);</code></pre>
<br />

<p>메인 쿼리 밑에 있는 다른 쿼리이다
페이지 객체에 넣어줄 목록 조회 데이터의 토탈 개수를 구하는 쿼리인데 여기서 완전 바보같은 실수를 했다.</p>
<br />

<pre><code class="language-java">    @Transactional(readOnly = true)
    public PageResponseDto findAllPage(Long id, String titleSearch, Boolean isFollowingBoard, int page) {


        int adjustedPage = (page &gt; 0) ? page - 1 : 0;
        Pageable pageable = PageRequest.of(adjustedPage, 10);

        Page&lt;BoardPageResponseDto&gt; allPage = boardRepository.findBoardsPage(id,titleSearch,isFollowingBoard,pageable);

        //사용자에게 반환할 페이지 객체 정보
        int nowPage = allPage.getNumber() + 1; // 1부터 시작
        int pageRange = 5;
        int totalPages = allPage.getTotalPages();
        int startPage = ((nowPage - 1) / pageRange) * pageRange + 1;
        int endPage = Math.min(startPage + pageRange - 1, totalPages);
        boolean hasPrevious = startPage &gt; 1;
        boolean hasNext = endPage &lt; totalPages;


        return new PageResponseDto (
                allPage.getContent(),
                nowPage,
                allPage.getSize(),
                totalPages,
                hasNext,
                hasPrevious,
                startPage,
                endPage);
    }</code></pre>
<br />

<p>게시글 목록 조회 service 메서드이다.</p>
<p>그냥 페이지 객체를 딸랑 반환하면 안될 것 같았다.
왜냐면 우리가 설계한 와이어프레임에서는</p>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/82791eb0-827d-49b1-8c2c-df2636ac93ff/image.png" /></p>
<p>이런 식으로 페이지 범위를 5로 정하고 
화살표를 통해 페이지 범위 이동이 가능하도록 설계했기 때문이다.
그래서 프론트 엔드에 줄 객체 정보들을 위 로직과 같이 설계했는데</p>
<p>분명히 db에 저장된 게시글 데이터는 42개인데
postman으로 실제로 테스트를 하면 자꾸 80개가 나오고 위에 나온
hasNext 변수나 startPage, endPage 값들이 다 이상하게 나왔다..</p>
<p>내 알고리즘 실력을 철저히 의심한 나는 죄 없는 위 알고리즘만 이렇게 저렇게 뜯어고쳤고
몇 시간을 고생하다 튜터님께 여쭤봤는데
문제는... 토탈 게시글 개수를 구하는 쿼리에서 group by를 안써줬기 때문이라는 문제를 발견했다,,,,,,</p>
<p>메인 쿼리에선 group by를 했으면서 해당 쿼리의 개수를 구하는 쿼리엔 group by를 안쓰니 서로 출력하는 결과값들이 달라 이상한 결과값이 나온 것이었다..^^</p>
<p>정말 실수는 예상치도 못한 곳에서 나온다는 것을 또 깨달았다..^^ 내 시간..</p>
<br />

<p>그래도 다른 팀 발표 중 튜터님이 페이징 객체를 바로 반환하기 보다는 page 전용 dto를 반환하는 것을 추천하시는 것 보고 뿌듯했다~~</p>
<br />

<hr />
<h2 id="✅-jpa-repository-vs-jpql-vs-jdbc-vs-querydsl-비교표">✅ JPA Repository vs JPQL vs JDBC vs QueryDSL 비교표</h2>
<table>
<thead>
<tr>
<th>항목</th>
<th>JPA Repository</th>
<th>JPQL (@Query)</th>
<th>QueryDSL</th>
<th>JDBC</th>
</tr>
</thead>
<tbody><tr>
<td><strong>쿼리 방식</strong></td>
<td>메서드 이름 기반 자동 생성</td>
<td>JPQL 문자열 직접 작성</td>
<td>타입 안전한 쿼리 DSL</td>
<td>SQL 직접 작성</td>
</tr>
<tr>
<td><strong>복잡한 쿼리</strong></td>
<td>어려움</td>
<td>유연함 (문자열 기반)</td>
<td>매우 유연 (조건 조립 용이)</td>
<td>가능 (하지만 수동 처리 많음)</td>
</tr>
<tr>
<td><strong>타입 안정성</strong></td>
<td>O</td>
<td>X (문자열 기반이라 컴파일 미검증)</td>
<td>O (컴파일 시점 검증)</td>
<td>X</td>
</tr>
<tr>
<td><strong>자동완성 지원</strong></td>
<td>제한적</td>
<td>없음</td>
<td>O</td>
<td>없음</td>
</tr>
<tr>
<td><strong>유지보수</strong></td>
<td>쉬움</td>
<td>문자열이라 다소 불편</td>
<td>가장 쉬움</td>
<td>어렵고 오류 유발 가능</td>
</tr>
<tr>
<td><strong>학습 난이도</strong></td>
<td>낮음</td>
<td>중간</td>
<td>중간~높음</td>
<td>낮음</td>
</tr>
<tr>
<td><strong>사용 목적</strong></td>
<td>단순 CRUD</td>
<td>복잡한 조회 쿼리</td>
<td>복잡한 조회 + 동적 쿼리</td>
<td>성능 최적화, 로우레벨 제어</td>
</tr>
<tr>
<td><strong>장점</strong></td>
<td>코드 간결, 생산성↑</td>
<td>SQL-like, 자유로운 조합</td>
<td>타입 안정성, 동적 쿼리</td>
<td>성능, 세밀한 제어</td>
</tr>
<tr>
<td><strong>단점</strong></td>
<td>복잡한 쿼리에 약함</td>
<td>타입 안정성 없음</td>
<td>설정과 코드 양 많음</td>
<td>생산성 낮고 유지보수 어려움</td>
</tr>
</tbody></table>
<hr />
<p>페이징 트러블슈팅 끝<del>~</del></p>
<br />

<p>느낀 점:
그래도 새로운 기능도 추가해서 구현해보고
그 속에서 알고리즘, sql dml을 직접 조작해보면서 스스로 성장함을 느꼈던 기능이었다!</p>