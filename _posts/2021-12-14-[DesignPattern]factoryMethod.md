---
layout: archive
title:  "[Design Pattern] - Factory method pattern"
categories:
    - Design Pattern
tags:
    - Design Pattern
---

팩토리 메서드 패턴(Factory method pattern)

---

<br>
<strong>팩토리 메서드 패턴이란?</strong>

>객체지향 디자인 패턴이다. <br>
>Factory method는 부모(상위) 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴<br>

<details>
<summary>특징</summary>
<div markdown="1">
- 객체 생성을 위한 인터페이스를 정의하지만 인터페이스를 구현하는 클래스가 인스턴스화할 클래스를 결정하도록 하는 디자인 패턴이다.<br>
- 팩토리 패턴을 사용하면 클래스의 인스턴스화를 하위 클래스로 연기할 수 있다.<br>
- 팩토리 패턴은 클래스 생성자를 대체하는 데 사용되며, 객체 생성 프로세스를 추상화하여 인스턴스화된 객체의 유형이 런타임에 결정될 수 있도록 한다.<br>
- 즉, 생성하는 객체를 별도로 두고 그 객체에 넘어오는 값에 따라서 다른 객체를 만들어 낸다.
</div>
</details>

---

<strong>팩토리 메소드 패턴을 사용하는 이유</strong>

클래스의 생성과 사용의 처리로직을 분리하여 결합도를 낮추기 위해 사용된다.
<br> 
팩토리 메소드 패턴을 사용할 경우 직접 객체를 생성해 사용하는 것을 방지하고 서브 클래스에 생성 로직을 위임함으로써 보다 효율적인 코드 제어를 할 수 있고 의존성을 제거 한다.

<details>
<summary>결합도란?</summary>
<div markdown="1">
결합도는 간단히 말해서 클래스의 처리 로직에 대한 변경점이 생겼을 때 얼마나 사이드 이펙트를 주는가를 뜻한다.
</div>
</details>

---

<strong>구조</strong>
<br>

<figure style="width: 70%" class="align-center">
  <img src="../../assets/images/factory_method_2.png" alt="">
  <figcaption class="text-center">펙토리 메소드 패턴 구조</figcaption>
  <figcaption class="text-center"><a>출처 : https://johngrib.github.io/wiki/factory-method-pattern/</a></figcaption>
</figure>

###### Product
 
팩토리 메소드가 생성하는 객체의 인터페이스를 정의한다.

###### ConcreteProduct
 
Product 인터페이스를 구현하는 클래스

###### Creator
 
추상 클래스이며 Product 유형의 객체를 반환하는 팩토리 메서드를 선언한다.<br>
ConcreteCreator 객체를 반환하는 팩토리 메소드의 기본 구현을 정의할 수도 있다.<br>
Product 객체를 생성하기 위해 팩토리 메서드를 호출 할 수도 있다.

###### ConcreteCreator
 
Creator 클래스를 구현하고 팩토리 메서드를 재정의하여 ConcreteProduct의 인스턴스를 반환하는 클래스

---

<strong>예시</strong>

MoneyBack, Titanium, Platinum 3가지 클래스가 있고 모두 추상 클래스 CreditCard를 구현한다.<br>
클래스 중 하나를 인스턴스화해야 하지만 클래스가 사용자에 따라 달라진다.

<figure style="width: 100%" class="align-center">
  <img src="../../assets/images/factory_method_3.png" alt="">
  <figcaption class="text-center">펙토리 메소드 패턴 예제</figcaption>
  <figcaption class="text-center"><a>출처 : https://www.c-sharpcorner.com/article/factory-method-design-pattern-in-c-sharp/</a></figcaption>
</figure>

* Product 
   - CreditCard
* ConcreteProduct
   - MoneyBackCreditCard, TitaniumCreditCard, PlatinumCreditCard
* Creator
   - CardFactory
* ConcreteCreator
   - MoneyBackCardFactory, TitaniumCardFactory, PlatinumCardFactory

---

<strong>코드 예시</strong>

###### Product

팩토리 메소드가 생성하는 객체의 인터페이스 정의 (CreditCard)

```c#
/// The 'Product' Abstract Class  
abstract class CreditCard  
{  
    public abstract string CardType { get; }  
    public abstract int CreditLimit { get; set; }  
    public abstract int AnnualCharge { get; set; }  
}     
```

###### ConcreteProduct

CreditCard를 구현하는 클래스 (MoneyBackCreditCard, TitaniumCreditCard, PlatinumCreditCard)

```c#
using System;  
  
/// A 'ConcreteProduct' class  
class MoneyBackCreditCard : CreditCard  
{  
    private readonly string _cardType;  
    private int _creditLimit;  
    private int _annualCharge;  

    public MoneyBackCreditCard(int creditLimit, int annualCharge)  
    {  
        _cardType = "MoneyBack";  
        _creditLimit = creditLimit;  
        _annualCharge = annualCharge;  
    }  

    public override string CardType  
    {  
        get { return _cardType; }  
    }  

    public override int CreditLimit  
    {  
        get { return _creditLimit; }  
        set { _creditLimit = value; }  
    }  

    public override int AnnualCharge  
    {  
        get { return _annualCharge; }  
        set { _annualCharge = value; }  
    }  
}  
```

```c#
using System;  
  
/// A 'ConcreteProduct' class  
class TitaniumCreditCard : CreditCard  
{  
    private readonly string _cardType;  
    private int _creditLimit;  
    private int _annualCharge;  

    public TitaniumCreditCard(int creditLimit, int annualCharge)  
    {  
        _cardType = "Titanium";  
        _creditLimit = creditLimit;  
        _annualCharge = annualCharge;  
    }  

    public override string CardType  
    {  
        get { return _cardType; }  
    }  

    public override int CreditLimit  
    {  
        get { return _creditLimit; }  
        set { _creditLimit = value; }  
    }  

    public override int AnnualCharge  
    {  
        get { return _annualCharge; }  
        set { _annualCharge = value; }  
    }      
}
```

```c#
using System;  
  
/// A 'ConcreteProduct' class  
class PlatinumCreditCard : CreditCard  
{  
    private readonly string _cardType;  
    private int _creditLimit;  
    private int _annualCharge;  

    public PlatinumCreditCard(int creditLimit, int annualCharge)  
    {  
        _cardType = "Platinum";  
        _creditLimit = creditLimit;  
        _annualCharge = annualCharge;  
    }  

    public override string CardType  
    {  
        get { return _cardType; }  
    }  

    public override int CreditLimit  
    {  
        get { return _creditLimit; }  
        set { _creditLimit = value; }  
    }  

    public override int AnnualCharge  
    {  
        get { return _annualCharge; }  
        set { _annualCharge = value; }  
    }  
}  
```

###### Creator

CreditCard 유형의 객체를 반환하는 팩토리 메서드를 선언한다.

```c#
using System;  
  
/// The 'Creator' Abstract Class  
abstract class CardFactory  
{  
    public abstract CreditCard GetCreditCard();  
}
```

###### ConcreteCreator

CardFactory 클래스를 구현하고 팩토리 메서드를 재정의하여 ConcreteProduct의 인스턴스를 반환하는 클래스

```c#
using System;  
  
/// A 'ConcreteCreator' class  
class MoneyBackFactory : CardFactory  
{  
    private int _creditLimit;  
    private int _annualCharge;  

    public MoneyBackFactory(int creditLimit, int annualCharge)  
    {  
        _creditLimit = creditLimit;  
        _annualCharge = annualCharge;  
    }  

    public override CreditCard GetCreditCard()  
    {  
        return new MoneyBackCreditCard(_creditLimit, _annualCharge);  
    }  
}  
```

```c#
using System;  
  
class TitaniumFactory: CardFactory      
{      
    private int _creditLimit;      
    private int _annualCharge;      
  
    public TitaniumFactory(int creditLimit, int annualCharge)      
    {      
        _creditLimit = creditLimit;      
        _annualCharge = annualCharge;      
    }      
  
    public override CreditCard GetCreditCard()      
    {      
        return new TitaniumCreditCard(_creditLimit, _annualCharge);      
    }      
}          
```

```c#
using System;  
  
/// A 'ConcreteCreator' class  
class PlatinumFactory: CardFactory      
{      
    private int _creditLimit;      
    private int _annualCharge;      
  
    public PlatinumFactory(int creditLimit, int annualCharge)      
    {      
        _creditLimit = creditLimit;      
        _annualCharge = annualCharge;      
    }      
  
    public override CreditCard GetCreditCard()      
    {      
        return new PlatinumCreditCard(_creditLimit, _annualCharge);      
    }      
}      
```

---

<strong>결과</strong>

```c#

using UnityEngine;

public class NewBehaviourScript : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        CardFactory factory = null;  

        string car = "moneyback"; //titanium, platinum

        switch (car.ToLower())  
        {  
            case "moneyback":  
                factory = new MoneyBackFactory(50000, 0);  
                break;  
            case "titanium":  
                factory = new TitaniumFactory(100000, 500);  
                break;  
            case "platinum":  
                factory = new PlatinumFactory(500000, 1000);  
                break;  
            default:  
                break;  
        }  

        CreditCard creditCard = factory.GetCreditCard();  
        Debug.Log("Card Type : " + creditCard.CardType + "\n");
        Debug.Log("Credit Limit : " + creditCard.CreditLimit + "\n"); 
        Debug.Log("Annual Charge : " + creditCard.AnnualCharge + "\n");  
    }
}
```

<figure style="width: 100%" class="align-center">
  <img src="../../assets/images/factory_method_4.png" alt="">
  <figcaption class="text-center">로그</figcaption>
</figure>

---

###### 참고 

[팩토리 메소드 패턴](https://johngrib.github.io/wiki/pattern/factory-method/)<br>
[Factory Method Design Pattern In C#](https://www.c-sharpcorner.com/article/factory-method-design-pattern-in-c-sharp/)