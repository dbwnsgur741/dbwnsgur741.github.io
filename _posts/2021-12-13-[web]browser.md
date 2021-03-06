---
layout: archive
title:  "[Web] - 브라우저의 동작원리"
categories:
    - Web
tags:
    - Web
    - Browser
---

주소창에 URL 또는 도메인을 입력하였을때 어떤 과정을 통해 웹 페이지가 보여지는지에 대하여 찾아보았다.<br>
(ex. 크롬, 사파리, 파이어폭스 등)

---
<br>
<strong>1. 브라우저란?</strong>
<br>

> 웹 브라우저는 동기(Synchronous)적으로 (HTML + CSS), Javascript 언어를 해석하여 내용을 화면에 보여주는 응용 소프트웨어입니다.
<br>

##### 동기적 vs 비동기적 ?

| 구분 | 방식 |
| :-----------:| :-----------|
| 동기적<br>(Synchronous) | 어떤 작업을 요청했을 때 그 작업이 종료될때 까지 기다린 후 다음 작업을 수행하는 방식||
| 비동기적(Asynchronous) | 어떤 작업을 요청했을 때 그 작업이 종료될때 까지 기다리지 않고 다른 작업을 하고 있다가, 요청했던 작업이 종료되면 그에 대한 추가 작업을 수행하는 방식||

<details>
<summary>브라우저가 동기적인 이유 ?</summary>
<div markdown="1">

> _script 태그를 body 태그 하단에 위치시키는 아이디어에서 찾을 수 있다._

- HTML 요소들이 script 로딩 지연으로 인해 렌더링에 지장 받는 일이 발생하지 않아 페이지 로딩 시간이 단축된다.
- DOM이 완성되기 전에 script가 DOM을 조작한다면 에러가 발생한다. 
- 자바스크립트는 렌더링 엔진이 아닌 자바스크립트 엔진이 처리한다.

</div>
</details>

---------

<br>
<strong>2. 브라우저의 주요기능</strong>

1. 사용자 인터페이스 
- 주소 표시줄, 이전/다음 버튼, 북마크 메뉴 등. 요청한 페이지를 보여주는 창을 제외한 나머지 모든 부분이다.
   
 2. 브라우저 엔진 
 - 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어.

3. 렌더링 엔진 
- 요청한 콘텐츠를 표시
  
4. 통신 
-  HTTP 요청과 같은 네트워크 호출에 사용

5. UI 백엔드 
-  콤보 박스와 창 같은 기본적인 장치를 그림. 플랫폼에서 명시하지 않은 일반적인 인터페이스로서, OS 사용자 인터페이스 체계를 사용.

6. 자바스크립트 해석기 
- 자바스크립트 코드를 해석하고 실행.

7. 자료 저장소 
- 이 부분은 자료를 저장하는 계층이다. (쿠키,스토리지 등..)
  
<figure class="align-center" style="width:500px">
  <img src="../../assets/images/browser-1.png" alt="">
  <figcaption class="align-center"><a>출처 : https://d2.naver.com/helloworld/59361</a></figcaption>
</figure>

---------

##### 렌더링 엔진이란?

>_렌더링 엔진의 역할은 요청 받은 내용을 브라우저 화면에 표시하는 일이다._
>>렌더링 엔진은 HTML 및 XML 문서와 이미지를 표시할 수 있다. 
>>플러그인이나 브라우저 확장 기능을 이용해 PDF와 같은 다른 유형도 표시할 수 있다. 

<details>
<summary>브라우저 렌더링 엔진들</summary>
<div markdown="1">

| 브라우저 | 렌더링 엔진 |
| :-----------:| :-----------|
| 파이어폭스 | 게코(Gecko) ||
| 사파리,크롬 | 웹킷(Webki) ||

</div>
</details>

##### 렌더링 엔진의 동작과정

<figure class="align-center" style="width:500px">
  <img src="../../assets/images/browser-2.png" alt="">
  <figcaption><a>출처 : https://d2.naver.com/helloworld/59361</a></figcaption>
</figure>

1. HTML 문서를 파싱하고 "콘텐츠 트리" 내부에서 태그를 DOM 노드로 변환하고 외부 CSS 파일과 함께 포함된 스타일 요소도 파싱한다. 스타일 정보와 HTML 표시 규칙은 "렌더 트리"라고 부르는 또 다른 트리를 생성한다.

2. 렌더 트리는 색상 또는 면적과 같은 시각적 속성이 있는 사각형을 포함하고 있는데 정해진 순서대로 화면에 표시된다.

3. 렌더 트리 생성이 끝나면 배치가 시작되는데 이것은 각 노드가 화면의 정확한 위치에 표시되는 것을 의미한다.

4. 렌더링 엔진은 좀 더 나은 사용자 경험을 위해 가능하면 빠르게 내용을 표시하는데 모든 HTML을 파싱할 때까지 기다리지 않고 배치와 그리기 과정을 시작한다.

##### 파싱(parsing)

>_문서 파싱은, 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것을 의미_

파싱 결과는 보통 문서 구조를 나타내는 노드 트리인데 파싱 트리(parse tree) 또는 문법 트리(syntax tree)라고 부른다.

파싱은 어휘 분석과 구문 분석이라는 두 가지로 구분할 수 있다.

1. 어휘 분석
- 자료를 토근으로 분해하는 과정
- 토큰은 유효하게 구성된 단위의 집합체 (사전에 등장하는 모든 단어)
  
1. 구문 분석
- 언어의 구문 규칙을 적용하는 과정

<figure class="align-center">
  <img src="../../assets/images/react_3.png" style="width:10%" class="align-center" alt="">
  <figcaption class="text-center">문서 소스로부터 파싱 트리를 만드는 과정</figcaption>
</figure>


<details>
<summary>파싱과정</summary>
<div markdown="1">

- 파싱 과정은 반복된다. 
- 파서는 보통 어휘 분석기로부터 새 토큰을 받아서 구문 규칙과 일치하는지 확인한다. 
- 규칙에 맞으면 토큰에 해당하는 노드가 파싱 트리에 추가되고 파서는 또 다른 토큰을 요청한다.
- 규칙에 맞지 않으면 파서는 토큰을 내부적으로 저장하고 토큰과 일치하는 규칙이 발견될 때까지 요청한다. 
- 맞는 규칙이 없는 경우 예외로 처리하는데 이것은 문서가 유효하지 않고 구문 오류를 포함하고 있다는 의미다.

</div>
</details>

##### 변환

<figure class="align-center">
  <img src="../../assets/images/react_4.png" style="width:10%" class="align-center" alt="">
  <figcaption class="text-center">컴파일 과정</figcaption>
</figure>

<details>
<summary>변환과정</summary>
<div markdown="1">

- 파서 트리는 최종 결과물이 아니다. 
- 파싱은 보통 문서를 다른 양식으로 변환하는데 컴파일이 하나의 예가 된다. 
- 소스 코드를 기계 코드로 만드는 컴파일러는 파싱 트리 생성 후 이를 기계 코드 문서로 변환한다.

</div>
</details>

<br>

[참고자료]

- <a>https://gyoogle.dev/blog/web-knowledge/</a>

- <a>https://d2.naver.com/helloworld/59361</a>

