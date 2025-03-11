<h3 id="lv-3-객체-지향-설계를-적용해-순서-제어를-클래스로-관리하기">Lv 3. 객체 지향 설계를 적용해 순서 제어를 클래스로 관리하기</h3>
<ul>
<li><input disabled="" type="checkbox" /> <strong>요구사항이 가지는 의도</strong><ul>
<li><input disabled="" type="checkbox" /> 객체 지향 개념을 학습하고, 데이터를 구조적으로 관리하며 프로그램을 설계하는 방법을 익힙니다.</li>
<li><input disabled="" type="checkbox" /> <code>main</code> 함수에서 관리하던 전체 순서 제어를 <code>Kiosk</code> 클래스를 통해 관리합니다.</li>
</ul>
</li>
<li><input disabled="" type="checkbox" /> <strong><code>Kiosk</code> 클래스 생성하기</strong><ul>
<li><input disabled="" type="checkbox" /> <strong>설명</strong>: 키오스크 프로그램의 메뉴를 관리하고 사용자 입력을 처리하는 클래스입니다.</li>
<li><input disabled="" type="checkbox" /> <code>MenuItem</code>을 관리하는 리스트가 필드로 존재합니다.</li>
<li><input disabled="" type="checkbox" /> <code>main</code> 함수에서 관리하던 입력과 반복문 로직은 이제 <code>start</code> 함수를 만들어 관리합니다.</li>
<li><input disabled="" type="checkbox" /> <code>List&lt;MenuItem&gt; menuItems</code> 는 <code>Kiosk</code> 클래스 생성자를 통해 값을 할당합니다.<ul>
<li><input disabled="" type="checkbox" /> <code>Kiosk</code> 객체를 생성하고 사용하는 <code>main</code> 함수에서 객체를 생성할 때 값을 넘겨줍니다.</li>
</ul>
</li>
</ul>
</li>
<li><input disabled="" type="checkbox" /> 요구사항에 부합하는지 검토<ul>
<li><input disabled="" type="checkbox" /> 키오스크 프로그램을 시작하는 메서드가 구현되어야 합니다.<ul>
<li><input disabled="" type="checkbox" /> 콘솔에 햄버거 메뉴를 출력합니다.</li>
<li><input disabled="" type="checkbox" /> 사용자의 입력을 받아 메뉴를 선택하거나 프로그램을 종료합니다.</li>
<li><input disabled="" type="checkbox" /> 유효하지 않은 입력에 대해 오류 메시지를 출력합니다.</li>
<li><input disabled="" type="checkbox" /> <code>0</code>을 입력하면 프로그램이 ‘뒤로가기’되거나 ‘종료’됩니다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<hr />
<h3 id="1️⃣-kiosk-클래스-필드-선언-및-start-메서드-생성">1️⃣ Kiosk 클래스 필드 선언 및 start 메서드 생성</h3>
<pre><code class="language-java">public class Kiosk {
    MenuItem menuItem;

    //프로그램 순서 및 흐름 제어를 담당하는 클래스
    private List&lt;MenuItem&gt; menuItems;

    public Kiosk(List&lt;MenuItem&gt; menuItems) {
        this.menuItems = menuItems;
    }

    public List&lt;MenuItem&gt; getMenuItems() {
        return menuItems;
    }

    public void setMenuItems(List&lt;MenuItem&gt; menuItems) {
        this.menuItems = menuItems;
    }</code></pre>
<p><code>MenuItem</code>을 관리하는 리스트를 필드로 선언</p>
<pre><code class="language-java">    public void start() {

        Scanner scanner = new Scanner(System.in);

        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔   햄버거 드실라우  🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);
        System.out.println(&quot;🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔🍔&quot;);


        //메뉴 고르기
        while(true) {
            try {

                //메뉴들 출력
                System.out.println(&quot;\n🍔 맘스터치 메뉴 🍔&quot;);

                for(int i = 0; i&lt;this.menuItems.size(); i++) {

                    String menuName = this.menuItems.get(i).getMenuName();
                    double menuPrice = this.menuItems.get(i).getMenuPrice();
                    String menuInfo = this.menuItems.get(i).getMenuInfo();

                    //영어는 한 글자당 1byte
                    //한글은 한 글자당 2byte

                    int menuSize = 20;
                    int length = menuSize - menuName.length();

                    System.out.printf(&quot;%-2d. %-&quot;+ length + &quot;s | W %3.1f | %s%n&quot;, i+1, menuName, menuPrice, menuInfo);

                }

                System.out.println(&quot;0 . 종료                |  종료&quot;);
                System.out.println();

                System.out.print(&quot;1~5 또는 0을 입력하세요: &quot;);
                int num = scanner.nextInt();

                if (num == 1) {
                    System.out.println(&quot;\n-------- 선택한 메뉴 --------&quot;);
                    String menuName = this.menuItems.get(num-1).getMenuName();
                    double menuPrice = this.menuItems.get(num-1).getMenuPrice();
                    String menuInfo = this.menuItems.get(num-1).getMenuInfo();

                    System.out.printf(&quot;%-2d. %-15s| W %5.1f | %s%n&quot;, num, menuName, menuPrice, menuInfo);

                    System.out.println(&quot;\n9. 이전으로&quot;);
                    System.out.println(&quot;0. 종료&quot;);

                    System.out.print(&quot;\n입력 : &quot;);
                    num = scanner.nextInt();

                    if(num == 0) {
                        System.out.println(&quot;\n종료합니다.&quot;);
                        break;
                    } else if (num == 9) {
                        System.out.println(&quot;\n메뉴화면으로 돌아갑니다.\n&quot;);
                    }
                } else if (num == 2) {
                    System.out.println(&quot;2. 불싸이버거&quot;);
                    break;
                } else if (num == 3) {
                    System.out.println(&quot;3. 화이트갈릭버거&quot;);
                    break;
                } else if (num == 4) {
                    System.out.println(&quot;4. 통새우버거&quot;);
                    break;
                } else if (num == 5) {
                    System.out.println(&quot;5. 딥치즈버거&quot;);
                    break;
                } else if (num == 0) {
                    System.out.println(&quot;종료&quot;);
                    break;
                } else {
                    System.out.println(&quot;\n❌ 1~5 사이에서 다시 입력해주세요.\n&quot;);
                }
            } catch (InputMismatchException e) {
                System.out.println(&quot;\n❌ 숫자만 입력해주세요\n&quot;);
                scanner.next();//버퍼비우기
            }
        }

        scanner.close();

    }</code></pre>
<p>kiosk 클래스 start메서드</p>
<br />


<h4 id="등록된-메뉴-출력">등록된 메뉴 출력</h4>
<pre><code class="language-java">                for(int i = 0; i&lt;this.menuItems.size(); i++) {

                    String menuName = this.menuItems.get(i).getMenuName();
                    double menuPrice = this.menuItems.get(i).getMenuPrice();
                    String menuInfo = this.menuItems.get(i).getMenuInfo();

                    //영어는 한 글자당 1byte
                    //한글은 한 글자당 2byte

                    int menuSize = 20;
                    int length = menuSize - menuName.length();

                    System.out.printf(&quot;%-2d. %-&quot;+ length + &quot;s | W %3.1f | %s%n&quot;, i+1, menuName, menuPrice, menuInfo);
</code></pre>
<ul>
<li>printf 와 서식 지정자로 메뉴 목록을 출력<blockquote>
<p>한글은 2바이트, 영어는 1바이트로 되어있어서 메뉴출력 콘솔화면이 깨지는 현상 발생. 추후에 수정 예정. 아직 방법을 못 찾음</p>
</blockquote>
</li>
</ul>
<br />

<h4 id="메뉴고르기">메뉴고르기</h4>
<pre><code class="language-java">        //메뉴 고르기
        while(true) {
            try {

                //메뉴들 출력
                System.out.println(&quot;\n🍔 맘스터치 메뉴 🍔&quot;);

                for(int i = 0; i&lt;this.menuItems.size(); i++) {

                    String menuName = this.menuItems.get(i).getMenuName();
                    double menuPrice = this.menuItems.get(i).getMenuPrice();
                    String menuInfo = this.menuItems.get(i).getMenuInfo();

                    //영어는 한 글자당 1byte
                    //한글은 한 글자당 2byte

                    int menuSize = 20;
                    int length = menuSize - menuName.length();

                    System.out.printf(&quot;%-2d. %-&quot;+ length + &quot;s | W %3.1f | %s%n&quot;, i+1, menuName, menuPrice, menuInfo);

                }

                System.out.println(&quot;0 . 종료                |  종료&quot;);
                System.out.println();

                System.out.print(&quot;1~5 또는 0을 입력하세요: &quot;);
                int num = scanner.nextInt();

                if (num == 1) {
                    System.out.println(&quot;\n-------- 선택한 메뉴 --------&quot;);
                    String menuName = this.menuItems.get(num-1).getMenuName();
                    double menuPrice = this.menuItems.get(num-1).getMenuPrice();
                    String menuInfo = this.menuItems.get(num-1).getMenuInfo();

                    System.out.printf(&quot;%-2d. %-15s| W %5.1f | %s%n&quot;, num, menuName, menuPrice, menuInfo);

                    System.out.println(&quot;\n9. 이전으로&quot;);
                    System.out.println(&quot;0. 종료&quot;);

                    System.out.print(&quot;\n입력 : &quot;);
                    num = scanner.nextInt();

                    if(num == 0) {
                        System.out.println(&quot;\n종료합니다.&quot;);
                        break;
                    } else if (num == 9) {
                        System.out.println(&quot;\n메뉴화면으로 돌아갑니다.\n&quot;);
                    }
                } else if (num == 2) {
                    System.out.println(&quot;2. 불싸이버거&quot;);
                    break;
                } else if (num == 3) {
                    System.out.println(&quot;3. 화이트갈릭버거&quot;);
                    break;
                } else if (num == 4) {
                    System.out.println(&quot;4. 통새우버거&quot;);
                    break;
                } else if (num == 5) {
                    System.out.println(&quot;5. 딥치즈버거&quot;);
                    break;
                } else if (num == 0) {
                    System.out.println(&quot;종료&quot;);
                    break;
                } else {
                    System.out.println(&quot;\n❌ 1~5 사이에서 다시 입력해주세요.\n&quot;);
                }
            } catch (InputMismatchException e) {
                System.out.println(&quot;\n❌ 숫자만 입력해주세요\n&quot;);
                scanner.next();//버퍼비우기
            }
        }

        scanner.close();

    }</code></pre>
<ul>
<li>while문 안에 메뉴출력을 같이 두어 메뉴 선택 후 이전으로 돌아가고 싶으면 메뉴출력으로 다시 돌아갈 수 있도록 설정</li>
<li>1-5 이외의 숫자 입력시 다시 while문을 돌려 재입력</li>
</ul>
<br />

<h3 id="mainclass">Main.class</h3>
<pre><code class="language-java">package com.example.kiosk;

import java.io.UnsupportedEncodingException;
import java.util.ArrayList;
import java.util.InputMismatchException;
import java.util.List;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        //Menu들 MenuItem에 등록
        MenuItem menuItem1 = new MenuItem(&quot;싸이버거&quot;, 4.9,&quot;매콤한 통다리살 패티가 통째로~ 맘스터치 시그니처 버거&quot;);
        MenuItem menuItem2 =new MenuItem(&quot;불싸이버거&quot;, 5.1,&quot;불 맛이 살아있는 싸이버거의 진또배기&quot;);
        MenuItem menuItem3 = new MenuItem(&quot;화이트갈릭버거&quot;, 4.9,&quot;크림처럼 부드러운 화이트갈릭 소스에 통가슴살&quot;);
        MenuItem menuItem4 = new MenuItem(&quot;통새우버거&quot;, 4.9,&quot;통새우살 패티에 신선한 양상추는 덤~&quot;);
        MenuItem menuItem5 = new MenuItem(&quot;딥치즈버거&quot;, 4.9,&quot;부드러운 치즈와 한층 더 촉촉해진 닭가슴살&quot;);

        //MenuItem을 관리하는 List에 등록
        List&lt;MenuItem&gt; menuItems = new ArrayList&lt;&gt;(List.of(menuItem1,menuItem2,menuItem3,menuItem4,menuItem5));

        //kiosk 객체 생성
        Kiosk kiosk = new Kiosk(menuItems);

        //키오스크 실행
        kiosk.start();

    }
}</code></pre>
<ul>
<li>객체를 생성하고 메서드를 실행하는 main 클래스</li>
</ul>