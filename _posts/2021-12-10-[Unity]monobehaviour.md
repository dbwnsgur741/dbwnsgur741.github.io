---
layout: archive
title:  "Monobehaviour LifeCycle"
categories:
    - Unity
tags:
    - Unity
---

유니티에서 C# class를 생성하게 되면 자동으로 Monobehaviour를 상속받게 된다.  
이 Monobehaviour가 어떤 클래스이고 생명주기는 어떻게 되는지 정리해보았다.

---
<br>
<strong>1. Unity 공식문서</strong>

>**_Description_**<br>
>MonoBehaviour는 모든 스크립트가 상속받는 기본 클래스입니다.<br>
>Javascript를 사용하는 경우에, 자동으로 MonoBehaviour를 상속받습니다. C# 또는 Boo언어를 사용하는 경우에는 명시적으로 MonoBehaviour를 상속받아야 합니다.<br>

즉, MonoBehaviour 클래스는 유니티 스크립트를 사용하기 위해서 반드시 <strong>상속받아야하는</strong> 클래스이다.<br>
MonoBehaviour 또한 클래스의 상속을 받는데 계속 찾아들어가면 결국 최상위 클래스는 Object 클래스임을 알 수 있다.
<br>
* Object > Component > Behaviour > MonoBehaviour 순서로 상속

```c#
...
namespace UnityEngine
{
    public class MonoBehaviour : Behaviour
    {
        public MonoBehaviour();
...
```

[object 클래스](https://docs.unity3d.com/kr/530/ScriptReference/Object.html)

---
<strong>2.생명주기(LifeCycle)</strong>
<br>

<figure style="width: 70%" class="align-center">
  <img src="../../assets/images/monobehaviour.png" alt="">
  <figcaption><a>출처 : https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=zparkx&logNo=220324890387</a></figcaption>
</figure>

이 'Monobehaviour'가 Scene에서 살아가는 일정한 흐름이 있다. 
<br>
엔진에서 자동으로 호출해주는 함수들인데 이 패턴의 흐름을 모아 '생명 주기(Life cycle)'라고 한다.
<br>

주요 메소드 몇 가지만 추려서 정리해보았다.

| name | 기능 |
| :---------| :-----------:|
| Awake() | Awake는 스크립트 인스턴스가 로딩될 때 호출됩니다.
| Start() | 	Start는 Update메소드가 처음 호출되기 바로 전에 호출됩니다.
| Update() | Update는 MonoBehaviour가 활성화 되어 있는 경우에, 매 프레임마다 호출됩니다.
|Destroy() | 게임오브젝트, 컴포넌트나 애셋을 삭제합니다.
|DontDestroyOnLoad() | 새로운 Scene이 로드될때 자동으로 파괴되지 않는 target 오브젝트를 만듭니다.

[MonoBehavior](https://docs.unity3d.com/kr/530/ScriptReference/MonoBehaviour.html)

