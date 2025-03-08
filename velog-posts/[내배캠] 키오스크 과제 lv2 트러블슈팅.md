<p>lv...2...  금방 끝날 줄 알았는디 
갑자기 메뉴 출력문에 집착해버려서 따흑.. 시간 다 버림</p>
<pre><code class="language-java">        while(true) {
            try {

                //메뉴들 출력
                System.out.println(&quot; 🍔 맘스터치 메뉴 🍔 &quot;);

                for(int i = 0; i&lt;menuItems.size(); i++) {

                    String menuName = menuItems.get(i).getMenuName();
                    double menuPrice = menuItems.get(i).getMenuPrice();
                    String menuInfo = menuItems.get(i).getMenuInfo();

                    //영어는 한 글자당 1byte
                    //한글은 한 글자당 2byte

                    int menuSize = 20;

                    int length = menuSize - menuName.length();

                    System.out.printf(&quot;%-2d. %-&quot;+ length + &quot;s | W %3.1f | %s%n&quot;, i+1, menuName, menuPrice, menuInfo);

                }

                System.out.println(&quot;0 . 종료               |  종료&quot;);
                System.out.println();


                System.out.print(&quot;1~5 또는 0을 입력하세요: &quot;);
                int num = scanner.nextInt();

                if (num == 1) {
                    System.out.println(&quot;\n-------- 선택한 메뉴 --------&quot;);
                    String menuName = menuItems.get(num-1).getMenuName();
                    double menuPrice = menuItems.get(num-1).getMenuPrice();
                    String menuInfo = menuItems.get(num-1).getMenuInfo();
                    System.out.printf(&quot;%-2d. %-15s| W %5.1f | %s%n&quot;, num, menuName, menuPrice, menuInfo);

                    System.out.println(&quot;\n0. 종료&quot;);
                    System.out.println(&quot;9. 이전으로&quot;);

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
        }</code></pre>
<blockquote>
<p>완성 코드
1번 누를 때만 선택한 메뉴 보여주고 이전,종료 할 수 있도록 설정했다
왜냐면..어차피 메서드로 다 추출할건데 너무 길어지니깐^^..</p>
</blockquote>
<hr />
<h3 id="❌-트러블-1">❌ 트러블 1</h3>
<pre><code class="language-java">        while(true) {
            try {
                if (num == 1) {
                    System.out.println(&quot;1. 싸이버거&quot;);
                    break;
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
                    continue;
                }
            } catch (InputMismatchException e) {
                System.out.println(&quot;\n❌ 숫자만 입력해주세요\n&quot;);
            }
        }</code></pre>
<blockquote>
<ol>
<li>try 블록에 입력도 넣었어야함. 입력 안넣으니 무한루프 발생 </li>
<li>else문에 continue 안해도 됨 어차피 break; 안했으니 while 반복문때문에 실행됨</li>
<li>catch문에 버퍼가 안비워져 있어서 숫자가 아닌 문자를 넣으면 무한 루프 발생</li>
</ol>
</blockquote>
<pre><code class="language-java">        while(true) {
            try {
                System.out.print(&quot;1~5 또는 0을 입력하세요: &quot;);
                int num = scanner.nextInt();

                if (num == 1) {
                    System.out.println(&quot;2. 불싸이버거&quot;);
                    break;
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
        }</code></pre>
<blockquote>
<p>요래 됐습니다</p>
</blockquote>
<br />

<h3 id="❌-트러블-2">❌ 트러블 2</h3>
<pre><code class="language-java">        while(true) {
            try {

                //메뉴들 출력
                System.out.println(&quot; 🍔 맘스터치 메뉴 🍔 &quot;);

                for(int i = 0; i&lt;menuItems.size(); i++) {

                    String menuName = menuItems.get(i).getMenuName();
                    double menuPrice = menuItems.get(i).getMenuPrice();
                    String menuInfo = menuItems.get(i).getMenuInfo();

                    //영어는 한 글자당 1byte
                    //한글은 한 글자당 2byte

                    int menuSize = 20;

                    int length = menuSize - menuName.length();

                    System.out.printf(&quot;%-2d. %-&quot;+ length + &quot;s | W %3.1f | %s%n&quot;, i+1, menuName, menuPrice, menuInfo);

                }

                System.out.println(&quot;0 . 종료               |  종료&quot;);
                System.out.println();


                System.out.print(&quot;1~5 또는 0을 입력하세요: &quot;);
                int num = scanner.nextInt();

                if (num == 1) {
                    System.out.println(&quot;\n-------- 선택한 메뉴 --------&quot;);
                    String menuName = menuItems.get(num-1).getMenuName();
                    double menuPrice = menuItems.get(num-1).getMenuPrice();
                    String menuInfo = menuItems.get(num-1).getMenuInfo();
                    System.out.printf(&quot;%-2d. %-15s| W %5.1f | %s%n&quot;, num, menuName, menuPrice, menuInfo);

                    System.out.println(&quot;\n0. 종료&quot;);
                    System.out.println(&quot;9. 이전으로&quot;);

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
        }</code></pre>
<blockquote>
<ol>
<li>사용자가 메뉴를 선택하면 선택한 메뉴를 보여주고 <code>9. 이전</code>을 눌러서 메뉴화면으로 다시 돌아갈지 <code>0.종료</code>를 눌러서 종료할지 흐름을 짜야함</li>
<li>그래서 메뉴 화면도 <code>while문</code>안에 넣어서 이전으로 돌아가고 싶을 때 9를 눌러 <code>break</code>을 하면 다시 메뉴화면이 보일 수 있도록 설정</li>
</ol>
</blockquote>