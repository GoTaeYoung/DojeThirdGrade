# JavaScript [&#128209;](https://www.w3schools.com/)


- ### 웹페이지를 동적으로 변경해주는 언어
- ### 파일의 확장자로 js 를 갖는다

-----

- ### HTML 문서에서 JavaScript 를 사용하는 3가지 방법
  1. ##### HTML 태그 내에 작성
     - 태그 내에 직접 작성하는 방식
     - 장점 : 태그에 연관된 스크립트가 분명히 드러난다
     - 단점 : 정보( HTML )와 제어( JavaScript )가 섞여 있어 정보의 가치가 떨어짐
       ~~~html
       <input type="button" onclick="alert('Hello World')" value="Hello World" />
       ~~~
  2. ##### 내부 JavaScript 사용
     - HTML 문서 내에 <script> 태그와 </script> 태그 사이에 JavaScript 작성
     - 장점 : HTML 태그와 JavaScript 코드를 분리
       ~~~html
       <script>
          JavaScript 작성
       </script>
       ~~~
  3. ##### 외부 JavaScript 사용
     - JavaScript 를 js 파일로 만들고 <script> 태그를 사용하여 HTML 문서에 가져오는 방법
     - js 파일의 내용이 <script> 태그 안으로 들어간다
     - 엄격하게 정보( HTML )와 제어( JavaScript )를 분리할 수 있다
     - JavaScript 의 재활용성을 높일 수 있다
     - 캐쉬를 통해서 속도의 향상, 전송량의 경량화를 도모함
     - js 파일은 <body> 의 최하단에 위치하는게 좋다
       ~~~html
       <script src="js 파일경로/js 파일명.js"></script>
       ~~~