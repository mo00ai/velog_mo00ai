<h3 id="optional">Optional</h3>
<ul>
<li>Optional 객체는 null 을 안전하게 다루게 해주는 객체입니다.</li>
<li>null 을 직접 다루는 대신 Optional 을 사용하면 NullPointerException 을 방지할 수 있습니다.</li>
</ul>
<br />

<hr />
<br />

<h3 id="optional의-필요성">Optional의 필요성</h3>
<br />

<h4 id="예시">예시</h4>
<p><strong><code>Optional</code> 이 왜 필요한지 <code>Student</code> 와 <code>Camp</code> 예시를 통해 학습해 봅시다.</strong></p>
<ul>
<li><code>camp.getStudent()</code> 는 <code>null</code> 을 반환할 수 있는 메서드입니다.</li>
<li>학생이 없는 경우 <code>null</code>을 반환하면 <code>NPE(NullPointerException)</code>가 발생합니다.</li>
<li><code>null</code>인 객체에서 <code>student.getName()</code>을 호출하는 것은 존재하지 않는 객체의 메서드를 실행하려는 것입니다.</li>
</ul>
<p><code>NullPointerException</code>  을 방지해야 하는 이유</p>
<ul>
<li><code>NPE</code> 예외는 런타임 예외이고 컴파일러가 잡아주지 못합니다. -&gt; 프로그램 종료됨</li>
<li>예외가 발생했을 때 처리해 주지 않으면 프로그램이 종료됩니다.</li>
</ul>
<br />

<p>Student</p>
<pre><code class="language-java">public class Student {

    // 속성
    private String name;

    // 생성자

    // 기능
    public String getName() {
        return this.name;
    }
}</code></pre>
<p>Camp - student란 객체를 담음</p>
<pre><code class="language-java">public class Camp {

    // 속성
    private Student student;

    // 생성자

    // 기능: ⚠️ null 을 반환할 수 있는 메서드
    public Student getStudent() {
        return student;
    }

    public void setStudent(Student student) {
            this.student = student;    
    }
}</code></pre>
<p>Main</p>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        Camp camp = new Camp();
        Student student = camp.getStudent(); // ⚠️ student 에는 null 이 담김
        // ⚠️ 아래 코드에서 NPE 발생! 컴파일러가 잡아주지 않음
        String studentName = student.getName(); // 🔥 NPE 발생 -&gt; 프로그램 종료
        System.out.println(&quot;studentName = &quot; + studentName);
    }
}</code></pre>
<blockquote>
<p>처음에 이 코드가 낯설었음 왜 이렇게 활용하지? 싶음
근데? 원래 객체(camp) 내에 객체(student)를 담는 경우는 이렇게 활용됨
camp로 student를 관리하고 싶을 때 사용하잖음</p>
</blockquote>
<br />
<br />

<hr />
<br />

<pre><code>public class Student {
    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}


import java.util.ArrayList;
import java.util.List;

public class Camp {

    private List&lt;Student&gt; students = new ArrayList&lt;&gt;();

    // 학생 추가
    public void addStudent(Student student) {
        students.add(student);
    }

    // 학생 전체 출력
    public void showAllStudents() {
        if (students.isEmpty()) {
            System.out.println(&quot;등록된 학생이 없습니다.&quot;);
            return;
        }

        System.out.println(&quot;학원에 등록된 학생 목록:&quot;);
        for (Student student : students) {
            System.out.println(&quot;이름: &quot; + student.getName() + &quot;, 나이: &quot; + student.getAge());
        }
    }
}


public class Main {
    public static void main(String[] args) {

        // 학원 객체 생성
        Camp camp = new Camp();

        // 학생 객체 생성
        Student student1 = new Student(&quot;홍길동&quot;, 20);
        Student student2 = new Student(&quot;김자바&quot;, 23);
        Student student3 = new Student(&quot;이코딩&quot;, 25);

        // 학생들을 학원에 등록
        camp.addStudent(student1);
        camp.addStudent(student2);
        camp.addStudent(student3);

        // 학원에 등록된 모든 학생 정보 출력
        camp.showAllStudents();
    }
}


학원에 등록된 학생 목록:
이름: 홍길동, 나이: 20
이름: 김자바, 나이: 23
이름: 이코딩, 나이: 25</code></pre><blockquote>
<p>이렇게 객체 내에 list로 학생을 저장하는 경우를 더 많이봄 
암튼 본론으로 돌아와서</p>
</blockquote>
<br />
<br />

<hr />
<br />


<p>Main</p>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        Camp camp = new Camp();
        Student student = camp.getStudent(); // ⚠️ student 에는 null 이 담김
        // ⚠️ 아래 코드에서 NPE 발생! 컴파일러가 잡아주지 않음
        String studentName = student.getName(); // 🔥 NPE 발생 -&gt; 프로그램 종료
        System.out.println(&quot;studentName = &quot; + studentName);
    }
}</code></pre>
<ul>
<li>camp 객체 생성</li>
<li>Student 객체 생성된 적 없음 <ul>
<li>그래서 null 값이 camp 호출시 출력되는 거임 student가 없으니까</li>
</ul>
</li>
</ul>
<p>현업에선 이같은 상황을 방지하기 위해</p>
<pre><code class="language-java">public class Student {
    private String name;
    private int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

// Camp.java
public class Camp {
    private Student student;

    // 내부에서 student 객체 생성
    public Camp(String studentName, int studentAge) {
        this.student = new Student(studentName, studentAge);
    }

    public Student getStudent() {
        return student;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {

        Camp camp = new Camp(&quot;김자바&quot;, 23);

        System.out.println(&quot;학생 이름: &quot; + camp.getStudent().getName());
        System.out.println(&quot;학생 나이: &quot; + camp.getStudent().getAge());
    }
}
</code></pre>
<p>애초에 이런 식으로 camp 내부에서 student 객체를 만들도록 생성자를 구현함.
camp 객체 생성시 자동으로 student 객체도 만들 수 있도록
이 방식이 실무에서 가장 많이 쓰이고 추천되는 방식임</p>
<blockquote>
<p>but 우리가 배우는건 Optional 이잖아?</p>
</blockquote>
<br />
<br />


<hr />
<br />


<h4 id="어쨋든-null이-발생하는-문제를-해결해보자">어쨋든 null이 발생하는 문제를 해결해보자</h4>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        Camp camp = new Camp();
        Student student = camp.getStudent(); // ⚠️ student 에는 null 이 담김
        // ⚠️ 아래 코드에서 NPE 발생! 컴파일러가 잡아주지 않음
        String studentName = student.getName(); // 🔥 NPE 발생 -&gt; 프로그램 종료
        System.out.println(&quot;studentName = &quot; + studentName);
    }
}</code></pre>
<p>Student student = camp.getStudent();</p>
<ul>
<li>Student student = null</li>
<li>변수에 null 이 담기는 건 충분히 가능한 거임! 에러 날 상황 아님, 자바 허용</li>
</ul>
<p>String studentName = student.getName();</p>
<ul>
<li>String studentName = null.getname();</li>
<li>but null인 객체에서 메서드를 호출하는 일 -&gt; <strong><em>NullPointerException(NPE)</em></strong> 예외 발생 - 프로그램 강제 종료</li>
</ul>
<br />

<p>이와 같은 상황을 방지하고자 null을 직접 처리해봄</p>
<ul>
<li>if문을 활용해서 null 처리를 할 수 있지만 모든 코드에서 null 이 발생할 가능성을 미리 예측하고 처리하는 것은 현실적으로 어렵습니다.</li>
</ul>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        Camp camp = new Camp();
        Student student = camp.getStudent();

        String studentName;
        if (student != null) { // ⚠️ 가능은하지만 현실적으로 어려움
            studentName = student.getName();
        } else {
            studentName = &quot;등록된 학생 없음&quot;; // 기본값 제공
        }

        System.out.println(&quot;studentName = &quot; + studentName);
    }
}</code></pre>
<p>방대한 양의 코드가 쌓이면 개발자가 일일이 체크하면서 조건문을 달아주기 힘듦. 분명히 빼먹는게 생길거임</p>
<br />
<br />
<br />

<h4 id="그래서-optional-활용함">그래서 Optional 활용함!!</h4>
<ul>
<li><code>Optional</code> 객체는 값이 있을 수도 있고 없을 수도 있는 컨테이너라고 생각하시면 됩니다.</li>
<li><code>Optional</code> 객체를 메서드 반환 자료형에 선언해서 해당 메서드가 <code>null</code> 이 반환될 가능성을 명확하게 전달할 수 있습니다.</li>
<li><code>Optional.ofNullable()</code> 을 사용하여  <code>null</code> 이 반환될 수 있는 객체를 감쌉니다.</li>
<li>활용할 때는 <code>isPresent()</code> 와 같은 Optional API 를 통해 안전하게 <code>null</code> 처리를 할 수 있습니다.</li>
<li>Optional 객체가 제공하는 메서드로 더 가시성이 높은 코드를 작성할 수 있음</li>
</ul>
<br />

<ol>
<li>isPresent() 활용 방법</li>
</ol>
<ul>
<li><code>Optional</code> 내부의 값이 존재할 경우에 <code>true</code> 반환합니다.</li>
<li>내부 값이 <code>null</code> 일 경우 <code>false</code> 를 반환합니다.</li>
</ul>
<pre><code class="language-java">import java.util.Optional;

public class Camp {

    // 속성
    private Student student;

    // 생성자

    // 기능
    // ✅ null 이 반환될 수 있음을 명확하게 표시
    public Optional&lt;Student&gt; getStudent() {
        return Optional.ofNullable(student);
    }

    public void setStudent(Student student) {
            this.student = student;    
    }
}</code></pre>
<p>게터에 Optional&lt;스튜던트&gt; 를 붙인 건 가시성을 높이기 위해서
null을 반환할 수 있는 객체를 감싸서 개발자가 쉽게 확인할 수 있도록
어차피 스튜던트 객체를 반환하는 게터인 건 똑같음</p>
<pre><code class="language-java">public class Main {

    public static void main(String[] args) {

        Camp camp = new Camp();

        // isPresent() 활용시 true 를 반환하고 싶을때 활용
        // Student newStudent = new Student();
        // camp.setStudent(newStudent);

        //  Optional 객체 반환받음
        Optional&lt;Student&gt; studentOptional = camp.getStudent();

        // Optional 객체의 기능 활용
        boolean flag = studentOptional.isPresent(); // false 반환
        if (flag) {
            // 존재할 경우
            Student student = studentOptional.get(); // ✅ 안전하게 Student 객체 가져오기
            String studentName = student.getName();
            System.out.println(&quot;studentName = &quot; + studentName);

        } else {
            // null 일 경우
            System.out.println(&quot;학생이 없습니다.&quot;);
        }
    }
}</code></pre>
<br />

<p> boolean flag = studentOptional.isPresent(); // false 반환</p>
<ul>
<li><code>.isPresent()</code> : Optional 내부 메서드 - boolean 반환</li>
<li>객체가 존재하면 (<code>null</code>이 아니면) <strong>true 반환</strong></li>
<li>객체가 <code>null</code>이면 <strong>false 반환</strong></li>
</ul>
<br />

<p>Student student = studentOptional.get(); // ✅ 안전하게 Student 객체 가져오기 </p>
<ul>
<li><p><code>.get()</code> : Optional 내부 메서드, Optional이 가진 객체를 반환함.</p>
</li>
<li><p>isPresent가 true, 즉 객체가 있는 경우이니 객체 가져올 수 있음</p>
</li>
<li><p>⚠️ 단, 내부 객체가 <code>null</code>이면 NoSuchElementException이 발생하므로, </p>
</li>
<li><p>반드시 <code>.isPresent()</code>나 <code>.orElse()</code> 등으로 체크한 후 사용하는 것이 권장됨.</p>
<br />

<blockquote>
<p>이처럼 Optional을 통해서 쉽고 가시적이게 null처리를 할 수 있다</p>
</blockquote>
<blockquote>
<p><strong><em>null을 반환할 수도 있을 것 같은 게터에 Optional&lt;객체&gt;를 달아두면 너무 좋음</em></strong></p>
</blockquote>
</li>
</ul>