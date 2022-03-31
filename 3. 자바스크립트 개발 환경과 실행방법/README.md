# 💻 자바스크립트 실행 환경

 개인적으로 되게 중요하다고 생각되어서 정리하였다.
 
 ## 자바스크립트 실행환경은 크게 **두가지**이다.
   - 브라우저 환경
     - html, css, javascript를 실행해 웹페이지를 브라우저 화면에 렌더링하는 것이 주된 목적
     - html 파일에 <script>태그로 들어간 코드, 개발자 도구 console 창.

  - Node.js 환경
     - 브라우저 외부에서 javascript 실행 환경을 제공하는 것이 주된 목적.

   * **이 때 브라우저와 node.js는 용도가 다르다.** 
   * 두개다 자바스크립트 코어인 ECMAScript를 실행할 수 있지만<br/>브라우저와 node.js 에서 **ECMAScript 이외에 추가로 제공하는 기능은 호환되지 않는다!**
   * ex) 브라우저 - DOM API 제공, nodejs - DOM API 제공하지 않음.
   ![image](https://user-images.githubusercontent.com/53414542/161101544-02a1f2ad-baa4-480a-bbb6-4614f8316035.png)
