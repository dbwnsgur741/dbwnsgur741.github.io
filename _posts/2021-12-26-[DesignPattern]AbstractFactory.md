---
layout: archive
title:  "[Design Pattern] - Abstract Factory pattern"
categories:
    - Design Pattern
tags:
    - Design Pattern
---

추상 팩토리 패턴(Abstract Factory pattern)

---

<strong>추상 팩토리 패턴이란?</strong>

>객체지향 디자인 패턴이다. <br>
>추상 팩토리 패턴은 상세화된 서브 클래스를 정의하지 않고도 서로 관련성이 있거나 독립적인 여러 객체의 군을 생성하기 위한 인터페이스를 제공한다.

---

<strong>특징</strong>
- 객체 구성을 통해 만든다.<br>
- 연관된 객체들의 집합을 만들기 위한 추상 형식을 제공한다.<br>
- 제품이 생산되는 방법은 추상 형식의 서브 클래스에 정의된다.<br>
- 여러 객체를 하나의 응집화된 군을 만들 때 사용한다.

---

<strong>구조</strong>

<figure style="width:90%" class="align-center">
  <img src="../../assets/images/abstract_factory_1.png" alt="">
  <figcaption class="text-center">추상 팩토리 패턴 구조</figcaption>
  <figcaption class="text-center"><a href="https://ko.wikipedia.org/wiki/%EC%B6%94%EC%83%81_%ED%8C%A9%ED%86%A0%EB%A6%AC_%ED%8C%A8%ED%84%B4">출처</a></figcaption>
</figure>

###### Abstract Factory (추상 팩토리)

각각의 추상 제품을 생성하기 위한 메소드들로 이루어진 인터페이스를 선언한다.

###### Abstract Products (추상 제품)

제품 객체 유형에 대한 인터페이스를 선언한다.

###### Concrete Factory (구체 팩토리)

구체적인 제품 객체를 생성하는 작업을 구현한다.

###### Concrete Products (구체 제품)

해당 구체 팩토리에서 생성할 제품 객체를 정의한다.
Abstract Product 인터페이스를 구현한다.

--- 

<strong>예시</strong>

<figure style="width: 80%" class="align-center">
  <img src="../../assets/images/abstract_factory_2.png" alt="">
  <figcaption class="text-center">추상 팩토리 패턴 예제</figcaption>
  <figcaption class="text-center"><a href="https://refactoring.guru/design-patterns/abstract-factory">출처</a></figcaption>
</figure>

* Abstract Factory
    - GUIFactory
* Abstract Product
    - Button, Checkbox
* Concrete Factory
    - WinFactory, MacFactory
* Concrete Product
    - WinButton, WinCheckbox, MacButton, MacCheckbox

---

<strong>코드 예시</strong>

###### Abstract Factory

- 다른 Abstract Product를 반환하는 메소드들을 선언한다.
- product들은 군(family)이라고 불리며 상위 수준의 개념으로 연관이 되어있다.

```c#
interface GUIFactory
{
    public abstract Button createButton();
    
    public abstract Checkbox createCheckbox();
}
```

---

###### Concrete Factory

- Concrete Factory는 products 군(family)를 만든다.
- Concrete Factory method는 추상 제품(Abstract Product)을 반환하고 내부에서는 제품(Product)이 인스턴스화된다.

```c#
class WinFactory : GUIFactory
{
    public Button createButton()
    {
        return new WinButton();
    }

    public Checkbox createCheckbox()
    {
        return new WinCheckbox();
    }
}

class MacFactory : GUIFactory
{
    public Button createButton()
    {
        return new MacButton();
    }

    public Checkbox createCheckbox()
    {
        return new MacCheckbox();
    }
}
```

---

###### Abstract Product

- 고유한 제품군(product family)의 각각의 제품(product)은 기본(base) 인터페이스가 있어야한다.
- 제품의 모든 변형은 인터페이스를 통해 구현되어야 한다.

```c#
public interface Button
{
    string UsefulFunctionA();
}

public interface Checkbox
{
    string UsefulFunctionB();

    string AnotherUsefulFunctionB(Button collaborator);
}
```

###### Concrete Product

- 구체 제품(Concrete Product)은 상응하는 구체 팩토리 (Concrete Factory)에 의해서 만들어진다.

```c#
class WinButton : Button
{
    public string UsefulFunctionA()
    {
        return "The result of the window button";
    }
}

class MacButton : Button
{
    public string UsefulFunctionA()
    {
        return "The result of the mac button";
    }
}

class WinCheckbox : Checkbox
{
    public string UsefulFunctionB()
    {
        return "The result of the window checkbox";
    }

    public string AnotherUsefulFunctionB(Button collaborator)
    {
        var result = collaborator.UsefulFunctionA();
        return $"The result of the checkbox collaborating with the ({result})";
    }
}

class MacCheckbox : Checkbox
{
    public string UsefulFunctionB()
    {
        return "The result of the product checkbox";
    }

    public string AnotherUsefulFunctionB(Button collaborator)
    {
        var result = collaborator.UsefulFunctionA();
        return $"The result of the checkbox collaborating with the ({result})";
    }
}

```
---

###### Client

- 클라이언트 코드는 추상 클래스(factory, product) 를 통해서만 작동한다.

```c#
class Client
{
    public Client(){
        Debug.Log("Client: Testing client code with the WinFactory type...");
        makeFactory(new WinFactory());

        Debug.Log("Client: Testing client code with the MacFactory type...");
        makeFactory(new MacFactory());
    }

    public void makeFactory(GUIFactory factory)
    {
        var productA = factory.createButton();
        var productB = factory.createCheckbox();

        Debug.Log(productB.UsefulFunctionB());
        Debug.Log(productB.AnotherUsefulFunctionB(productA));
    }
}
```

---

<strong>결과</strong>

```c#

using UnityEngine;

public class AbstractMethod : MonoBehaviour 
{
    void Start()
    {
        new Client();
    }
}
```

<figure style="width: 100%" class="align-center">
  <img src="../../assets/images/abstract_factory_3.png" alt="">
  <figcaption class="text-center">로그</figcaption>
</figure>

---

###### 참고

[C# Design Patterns](https://www.dofactory.com/net/design-patterns)<br>
[Abstract factory pattern example C#](https://refactoring.guru/design-patterns/abstract-factory/csharp/example)