# CSS [&#128209;](https://www.w3schools.com/)


- ### Cascading Style Sheet
- ### CSS 는 웹페이지가 사용자에게 어떻게 보여지는지 기술하는 언어

-----

- ### HTML 문서에서 CSS를 사용하는 3가지 방법
	1. ##### 외부 스타일 시트 ( External Style Sheet )
	2. ##### 내부 스타일 시트 ( Internal Style Sheet )
	3. ##### HTML 태그 내에 스타일 지정 ( Inline Styles )

-----

- #### 외부 스타일 시트
  - css 를 확장자로 가지고 있는 파일을 HTML 문서에 연결하여 사용
    ~~~html
    <head>
    	<link rel="stylesheet" type="text/css" href="파일명.css">
    </head>
    ~~~

- #### 내부 스타일 시트
  - HTML 문서 내의 <head> 와 </head> 사이에 스타일을 정의
  	~~~html
    <head>
        <style type="text/css">
        	스타일 작성
        </style>
    </head>
    ~~~

- #### HTML 태그 내에 스타일 지정
  - 스타일을 적용하고 싶은 태그 안에 정의
    ~~~html
    <태그명 style="속성명:속성값; 속성명:속성값;"></태그명>
    ~~~

-----

