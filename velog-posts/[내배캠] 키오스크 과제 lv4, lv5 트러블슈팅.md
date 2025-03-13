<pre><code class="language-java">package com.example.kiosk;

import javax.swing.*;
import java.util.ArrayList;
import java.util.InputMismatchException;
import java.util.List;
import java.util.Scanner;

public class Kiosk {
    MenuItem menuItem;

    Menu menu;

    private List&lt;Menu&gt; menus;

    public List&lt;Menu&gt; getMenus() {
        return menus;
    }

    public void setMenus(List&lt;Menu&gt; menus) {
        this.menus = menus;
    }

    public void start() {

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


        boolean mainMenuPrinting = true;
        boolean categoryMenuPrinting =true;
        boolean backButton = true;

        boolean exitKiosk = false;
        boolean exitCategory = false;

        int mainNum=0;
        int menuItemNum = 0;
        Menu pickedCategory = null;

        //메뉴 고르기
        while (!exitKiosk) {

            mainNum=0;
            menuItemNum = 0;
            pickedCategory = null;
            exitCategory = false;


            //메인 메뉴 출력
            if(mainMenuPrinting) {
                System.out.println(&quot;\n🍔 맘스터치 메뉴 🍔&quot;);
                for(int i=0; i&lt;this.menus.size(); i++) {
                    String menuCategory = this.menus.get(i).getMenuCategory();
                    System.out.println((i+1)+&quot;. &quot; + menuCategory);
                }
                System.out.println(&quot;0. 종료\n&quot;);
            }


            //메인 메뉴 입력
            mainNum = checkingInput(scanner, pickedCategory);

            if (mainNum &gt;= 1 &amp;&amp; mainNum &lt;= this.menus.size()) {
                pickedCategory = this.menus.get(mainNum - 1);
            } else if (mainNum == 0) {
                System.out.println(&quot;키오스크를 종료합니다.&quot;);
                exitKiosk = true;
                //break;
            }



            while (!exitCategory) {
                //선택한 카테고리 메뉴 출력
                if (categoryMenuPrinting) {
                    pickedCategory.printMenuItemList();
                }

                //선택한 카테고리 내 메뉴 선택
                menuItemNum = checkingInput(scanner, pickedCategory);

                if (menuItemNum &gt;= 1 &amp;&amp; menuItemNum &lt;= 5) {
                    pickedCategory.printPickedMenu(menuItemNum);
                    break;
                } else if (menuItemNum == 0) {
                    System.out.println(&quot;메인메뉴로 돌아갑니다.&quot;);
                    exitCategory = true;
                } else {
                    //꼭 다시 확인하기
                    //System.out.println(&quot;\n❌ 1~5 사이에서 다시 입력해주세요.\n&quot;);
                    categoryMenuPrinting = false;
                }

            }


        }
        scanner.close();
    }

    //입력값 예외 처리 로직
    public int checkingInput(Scanner scanner, Menu pickedCategory) {

        int input = 0;

        while (true) {

            try {
                if (pickedCategory == null) {

                    System.out.print(&quot;1~&quot; + this.menus.size() + &quot; 사이의 숫자를 입력해주세요: &quot;);
                    input = scanner.nextInt();

                    if (input &gt;= 1 &amp;&amp; input &lt;= this.menus.size()) {
                        return input;
                    } else if (input == 0) {
                        return input;
                    } else {
                        System.out.println(&quot;\n❌ 1~&quot; + this.menus.size() + &quot;사이에서 다시 입력해주세요.\n&quot;);
                    }

                } else {

                    System.out.print(&quot;1~5 또는 0을 입력하세요: &quot;);
                    input = scanner.nextInt();

                    if (input &gt;= 1 &amp;&amp; input &lt;= 5) {
                        return input;
                    } else if (input == 0) {
                        return input;
                    } else {
                        System.out.println(&quot;\n❌ 1~5 사이에서 다시 입력해주세요.\n&quot;);
                        //categoryMenuPrinting = false;
                    }

                }

            } catch (InputMismatchException e) {
                System.out.println(&quot;\n❌ 숫자만 입력해주세요\n&quot;);
                scanner.next();//버퍼비우기
            }

        }


    }

}
</code></pre>
<p>//중간과정</p>
<p>트러블 슈팅 적을거</p>
<ol>
<li>input 검사 메서드로 추출 
메서드 내엔 input 입력 검사 담당 try-catch문과 오입력시 안내문만 , 올바르게 입력하면 숫자를 return하도록 설정
start 메서드(호출하는 쪽)엔 숫자를 받아와서 그 숫자로 어떤 로직을 이어갈건지를 정리함</li>
</ol>
<p>-&gt; 이 분리과정이 힘들었음 어디까지 메서드로 넣어야할지 고민함
-&gt; 계산기는 숫자의 로직이 동일하니 ㄱㅊ았지만
-&gt; 키오스크는 두 숫자의 로직이 연결되다 보니(메인 입력 - 카테고리 입력) 분리가 힘들었음</p>
<ul>
<li>숫자 입력만 따로 메서드로 추출하니 편해졌다</li>
</ul>
<ol start="2">
<li>while문 빠져나가기</li>
</ol>
<ul>
<li>갑자기 에러가 떠서 당황</li>
<li>while문이 꼬인거였고 그리고 exitKiosk = true로 둬도 그게 다음 while문으로 리셋될 때 나타나는 거지 그 밑 로직들이 수행됨 그래서 break을 해줘야함</li>
</ul>