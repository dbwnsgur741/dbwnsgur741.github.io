---
layout: archive
title:  "React Native 동작 원리"
categories:
    - React Native
tags:
    - React Native
---

[React Native] 동작 원리

---

### 가상 DOM

<details>
<summary>DOM이란?</summary>
<div markdown="1">
- 문서 객체 모델(Document Object Model)은 HTML문서나 XML문서에 접근하기 위한 일종의 인터페이스이다.<br>
- 문서 내의 모든 요소의 목적과 특징을 정의하고, 각각의 요소에 접근하는 방법을 제공한다.
</div>
</details>

>_화면이 어떤 모습이어야 하는지 개발자가 작성한 내용과 실제 화면에 렌더링되는 것 사이에 존재하는 레이어_

리액트에서는 과도한 DOM의 수정을 막기 위하여 페이지의 변화를 바로 렌더링하지 않고 메모리에 존재하는 가상 DOM에서 변화가 필요한 곳을 계산하고 필요한 최소한의 변경사항만 렌더링 한다.

<figure style="width: 70%" class="align-center">
  <img src="../../assets/images/react_1.png" alt="">
  <figcaption class="text-center">state 변경 -> 차이점 계산 -> 다시 렌더링</figcaption>
  <figcaption class="text-center"><a>출처 : https://ssollacc.tistory.com/14</a></figcaption>
</figure>

---

### 리액트 네이티브 동작원리

리액트 네이티브는 브라우저의 DOM으로 렌더링하는 대신 objective-c API호출하여 iOS 컴포넌트로 렌더링하고, 자바 API를 호출하여 안드로이드 컴포넌트로 렌더링한다.<br><br>
웹 기반의 화면으로 최종 렌더링되는 대부분의 크로스 플랫폼 앱 개발 방법들과 구별되는 리액트 네이티브의 특징이다.

<figure style="width: 100%" class="align-center">
  <img src="../../assets/images/react_2.jpg" alt="">
  <figcaption class="text-center">다른 타깃으로 렌더링</figcaption>
  <figcaption class="text-center"><a>출처 : https://ssollacc.tistory.com/14</a></figcaption>
</figure>

---

### 리액트 네이티브 앱 4 가지 스레드

###### UI Thread ( Main Thread )
- 기본 안드로이드 또는 iOS UI 렌더링에 사용<br>
- 예를 들어, 안드로이드에서 이 스레드는 안드로이드 measure/layout/draw에 사용

###### JS Thread
- JS 스레드 또는 Javascript 스레드는 로직이 실행될 스레드 
- 예를 들어 애플리케이션의 자바스크립트 코드가 실행되고, API 호출이 이루어지고, 터치 이벤트가 처리되는 등의 스레드가 존재
- 네이티브 뷰에 대한 업데이트는 일괄 처리되어 JS 스레드의 각 이벤트 루프 끝에서 네이티브 측으로 전달되며 마지막에 UI 스레드에서 실행

###### Native Modules Thread
 
- 때때로 앱이 플랫폼 API에 액세스 해야하는 경우의 사용

###### Render Thread 
- Android L (5.0)에서만 리액트 네이티브 렌더링 스레드가 UI를 그리는데 사용되는 실제 OpenGL 명령 생성에 사용

---

### 리액트 네이티브 동작 순서

1) 앱 시작 시 메인 스레드 실행, JS 번들 로드

2) 자바스크립트 코드가 성공적으로 로드되면 메인 스레드는 다른 JS 스레드로 전송
   
3) React가 렌더링을 시작할 때 Reconciler는 "diffing"을 시작하고 새로운 가상 DOM(layout)을 생성하면 변경 사항을 다른 스레드로 전송 (Shadow Thread)

4) Shadow 스레드는 레이아웃을 계산한 다음 레이아웃 매개변수/객체를 메인(UI) 스레드로 전송 
   
* Shadow Thread 는 Shadow nodes 를 만든다.

5) 메인 스레드만 화면에 무언가를 렌더링할 수 있기 때문에 Shadow 스레드는 생성된 레이아웃을 메인 스레드로 보내야 UI가 렌더링된다.