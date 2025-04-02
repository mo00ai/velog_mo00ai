<p>lv1 트러블 슈팅</p>
<p>기능 1:  일정 생성시 contents를 입력 안해도 db엔 default값으로 &quot;내용없음&quot;이 들어갈 수 있도록</p>
<p>시도1. schedule entity에 @DynamicInsert
-&gt; 단점 있음 그리고 안됨</p>
<p>시도2. schedule entity 필드에 columnDefault(&quot;내용없음&quot;)와 @DynamicInsert</p>
<ul>
<li>또는 @Column(nullable = true, columnDefinition = &quot;VARCHAR(255) DEFAULT '내용 없음'&quot;)
-&gt; 단순히 테이블 ddl에 default를 명시하는 용도, jpa를 사용해서 insert 시 jpa는 모든 필드(컬럼)을 한 꺼번에 insert하기 때문에, 사용자가 안 쓴 값들은 null로 인식돼서 db엔 결국  null이 들어감</li>
</ul>
<p>시도 3. schedule entity 필드에 초기값 주기
private String contents = &quot;내용 없음&quot;;
-&gt; 어차피 dto의 null값으로 대체 되어서 의미없어짐</p>
<p>결국 &gt; service단에서 직접 null값을 &quot;내용없음&quot;으로 수정<img alt="" src="https://velog.velcdn.com/images/mo00ai/post/86d9fbd7-f1b7-42f5-9030-ab26f02b0c0d/image.png" /></p>
<p>참고한 블로그</p>
<blockquote>
<p><a href="https://velog.io/@minji/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%EC%97%94%ED%8B%B0%ED%8B%B0-%EC%BB%AC%EB%9F%BC-default-value-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-ColumnDefault-Builder.Default-%EC%B0%A8%EC%9D%B4">https://velog.io/@minji/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%EC%97%94%ED%8B%B0%ED%8B%B0-%EC%BB%AC%EB%9F%BC-default-value-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-ColumnDefault-Builder.Default-%EC%B0%A8%EC%9D%B4</a>
<a href="https://sundries-in-myidea.tistory.com/91">https://sundries-in-myidea.tistory.com/91</a>
<a href="https://velog.io/@minju0426/JPARepository%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90%EC%82%AC%EC%9A%A9%EB%B2%95-Method">https://velog.io/@minju0426/JPARepository%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90%EC%82%AC%EC%9A%A9%EB%B2%95-Method</a>
<a href="https://frhyme.github.io/others/DB_NOT_NULL_vs_default/">https://frhyme.github.io/others/DB_NOT_NULL_vs_default/</a>
<a href="https://eocoding.tistory.com/71">https://eocoding.tistory.com/71</a>
<a href="https://jaehee1007.tistory.com/16">https://jaehee1007.tistory.com/16</a></p>
</blockquote>
<hr />
<p>기능 2 : 일정 수정시 사용자가 수정한 값은 바뀌고, 안적은 값들은 원본 일정 (수정전) 내용 유지</p>
<p>고민1. DTO에 수정을 해야하나?
-&gt; DTO는 단순 데이터를 담는 박스같은 용도인데 그걸 맘대로 수정(setter사용)해도 되나?</p>
<p>고민2. 강의 내용에선 requestDTO의 필드들에 모두 final이 주입되어있음</p>
<ul>
<li>이는 개발자마다 다른 듯...함? 어떤 사람은 final을 사용해서 초기화(생성자)로 값을 주입할 때만 사용가능하고 수정하지 못하도록 하고</li>
<li>어떤 사람은 그냥 final 없이 private String name 처럼 기본만 적어서 setter 수정 자유롭게 하고...</li>
</ul>
<p>해결 &gt; 결국엔 걍 이 또한 service 딴에서 null인지 확인한 후 값을 바꿔준다~default값으로</p>