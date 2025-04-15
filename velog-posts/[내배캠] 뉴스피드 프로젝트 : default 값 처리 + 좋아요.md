<h2 id="1-게시글-수정시-입력값-null-일-때-default-처리">1. 게시글 수정시 입력값 null 일 때 default 처리</h2>
<pre><code class="language-java">    @PatchMapping(&quot;/{id}&quot;)
    public ResponseEntity&lt;BoardUpdateResponseDto&gt; updateBoard(
            @SessionAttribute(name = Const.LOGIN_USER, required = false) UserResponseDto loginUser,
            @PathVariable Long id,
            @Valid @RequestBody BoardUpdateRequestDto dto) {

        return new ResponseEntity&lt;&gt;(boardService.updateBoard(loginUser.getId(), id, dto), HttpStatus.OK);
    }</code></pre>
<p>updtae controller</p>
<p><img alt="" src="https://velog.velcdn.com/images/mo00ai/post/1228da67-2fa7-4eda-b62e-aa208584c2d2/image.png" /></p>
<p>사용자는 title, content를 수정할 수 있다
하지만 둘 다 필수값은 아니며, 사용자가 수정하지 않을시(입력값 필드가 null일 시) db엔 null인 필드가 수정되지 않으며, 수정 전 데이터가 유지된다</p>
<p>default처리는 저번 과제에서부터 고민하던 것
저번 과제는 service에서 처리했지만
이번 프로젝트에선 </p>
<pre><code class="language-java">@Getter
@Entity
@Table(name=&quot;boards&quot;)
@DynamicUpdate
public class Board extends BaseEntity{

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String title;

    @Column(nullable = false)
    private String content;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = &quot;user_id&quot;)
    private User user;

    @OneToMany(mappedBy = &quot;board&quot;)
    @OnDelete(action = OnDeleteAction.CASCADE)
    private List&lt;Comment&gt; comments = new ArrayList&lt;&gt;();

    public Board() {

    }

    public Board(String title, String content, User user) {
        this.title = title;
        this.content = content;
        this.user = user;
    }

    public void update(String title, String content) {
        if(title != null) {
            this.title = title;
        }
        if(content != null) {
            this.content = content;
        }
    }

}</code></pre>
<ol>
<li>entity의 updated setter내에서 null값일 경우 조건처리를 해줌</li>
<li>그리고 클래스 어노테이션 @DynamicUpdate</li>
</ol>
<blockquote>
<p>JPA Repository hibernate는 entity 내 모든 필드들을 자동으로 insert함
비효율적임, 그래서 원하는 필드만 넣게해주는 어노테이션이 바로 <code>@DynamicUpdate</code>
입력값이 null값일 경우 그 값은 제외하고 넣어주는 듯..?
설명을 잘 못하겠네 공부하고 수정함</p>
</blockquote>
<hr />
<h2 id="2-좋아요-토글-처리">2. 좋아요 토글 처리</h2>
<p>우선 BoardLike은 Board 도메인 내에 있음 
하지만 컨트롤러, 서비스 등은 안에서 분리처리함</p>
<h3 id="컨트롤러">컨트롤러!</h3>
<p>처음엔 좋아요/ 좋아요 삭제 처리를 나눠서 
PostMapping과 DeleteMapping 컨트롤러를 따로따로 둠</p>
<p>하지만 여기서 고민함</p>
<p>🤔 과연 따로따로 둬야할까?
좋아요 취소할시 response로 좋아요가 취소되어있습니다 응답을 주고
프엔이라면 새로고침을 할텐데 이거 완전..비효율 아님?</p>
<ul>
<li>우리는 트위터 기반의 SNS를 구현함</li>
<li>트위터는 좋아요 등록/삭제가 바로바로 이루어짐(따로 response없음)</li>
</ul>
<blockquote>
<p>Post 컨트롤러 하나만 두고, service에서 좋아요/삭제 처리를 한꺼번에 Post 컨트롤러에서 하는게 자연스럽다 생각</p>
</blockquote>
<blockquote>
<p>service에선 좋아요 삭제 서비스가 있음!
➡️ 이는 좋아요 등록 서비스에서 조건절로 좋아요 삭제 시 사용될 거임
➡️ 서비스에서 서비스를 호출하면 안된다고 생각했음 하지만, 현재 서비스에서 현재 서비스 메서드 호출하는 건 ㄱㅊ, 
➡️ boardService에서 commentService를 호출하는 등 다른 도메일 서비스를 호출하는 건 안됨!!</p>
</blockquote>
<pre><code class="language-java">    @Transactional
    public BoardLikeResponseDto likeBoard(Long id, Long boardId) {

        Board board = boardRepository.findById(boardId).orElseThrow(() -&gt; new BoardNotFoundException(ErrorCode.BOARD_NOT_FOUND));

        User user = userRepository.findById(id).orElseThrow(() -&gt; new UserNotFoundException(ErrorCode.USER_NOT_FOUND.getCode()));

        //본인 게시글에 좋아요 못 누름
        if(board.getUser().getId().equals(user.getId())) {
            throw new BoardLikeFailedException(ErrorCode.BOARD_LIKE_FAILED);
        }

        Long likeCount = boardLikeRepository.countByBoard_Id(board.getId());

        boolean isLiked = boardLikeRepository.existsByBoard_IdAndUser_Id(boardId,id);

        //이미 좋아요를 누른 경우 : 좋아요 취소
        if(isLiked) {
            unlikeBoard(id,boardId);

            return new BoardLikeResponseDto(
                    board.getId(),
                    likeCount-1,
                    user.getId(),
                    user.getUserName(),
                    false
            );
        }


        BoardLike boardLike = new BoardLike(board, user);

        boardLikeRepository.save(boardLike);

        return new BoardLikeResponseDto(
                board.getId(),
                likeCount+1,
                user.getId(),
                user.getUserName(),
                true
        );
    }</code></pre>
<blockquote>
<p>이런 식으로 메서드 호출함</p>
</blockquote>
<hr />
<h2 id="좋아요-연관관계양방향-단방향">좋아요 연관관계(양방향? 단방향)</h2>
<p>Board Entity </p>
<pre><code class="language-java">@Getter
@Entity
@Table(name=&quot;boards&quot;)
@DynamicUpdate
public class Board extends BaseEntity{

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String title;

    @Column(nullable = false)
    private String content;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = &quot;user_id&quot;)
    private User user;

    @OneToMany(mappedBy = &quot;board&quot;)
    @OnDelete(action = OnDeleteAction.CASCADE)
    private List&lt;Comment&gt; comments = new ArrayList&lt;&gt;();

    public Board() {

    }

    public Board(String title, String content, User user) {
        this.title = title;
        this.content = content;
        this.user = user;
    }

    public void update(String title, String content) {
        if(title != null) {
            this.title = title;
        }
        if(content != null) {
            this.content = content;
        }
    }

}</code></pre>
<p>comment는 board에서도 조회를 해야함.
comment를 활용해야하니까!
그래서 양방향 관계로 설정하고 이는 ㄱㅊ음</p>
<p>근데 여기서 고민</p>
<p>게시글을 삭제하려니까 comment만 있을 땐 괜찮았는데
후에 boardLike도 만드니까 삭제가 안됨!!!!!!
-&gt; boardLike도 삭제처리 해줘야함</p>
<p>여기서 문제!</p>
<ol>
<li><p>BoardLike 엔티티도 comment처럼 board에 양방향 처리를 해준 뒤 @ondelete 어노테이션 등으로 cascade 삭제 처리를 해줘야하는가?</p>
<ul>
<li>근데 board는 boardlike 정보가 딱히 필요없는데?.. 불필요한 정보를 엔티티 내에 포함시키는 건 비효율적 아닌가..</li>
</ul>
</li>
<li><p>아님 board 삭제 서비스에서 boardLike 삭제 리포지터리를 호출해서 삭제할까?</p>
<ul>
<li>너무 수작업 아닌가..</li>
</ul>
</li>
</ol>
<blockquote>
<p>튜터님 피드백
이건 취향 차이
하지만 선생님 생각도 1번으로 양방향 하는 건 너무 정보의 낭비? 라고 생각한다고 하심
나도 이 의견이 맞다고 생각해서 엔티티 연관관계는 단방향으로 유지하고 수작업으로 삭제 리포지터리를 호출하기로 함!</p>
</blockquote>
<hr />