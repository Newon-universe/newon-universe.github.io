---
layout: post
title: 객체 지향 프로그래밍(Object Oriented Programming)
author: Newon
categories: Kotlin
tags: [Kotlin, CS]
sidebar: []
---

## 컴파일러와 객체 지향 프로그래밍
객체(Object) 를 지향(Oriented) 하는 프로그래밍은 코딩을 작성할 때 사용할 수 있는 하나의 패러다임, 더 일반적으로는 하나의 글쓰기 장르라고 볼 수 있다.

잠시 객체 지향 프로그래밍을 접어두고, 코딩이 어떻게 동작하는지부터 생각해보자. 어떤 프로그래밍 언어를 쓰더라도 코드는 컴파일러를 거쳐서 수행된다.  
사람이 작성한 코드를 기계어로 번역하는 작업이 필요한 것인데, 이때 코드는 위에서부터 아래로 한 줄씩 코드를 읽고, 번역하고, 내용을 수행한다.

화가가 그림을 그려서 파는 작업을 위의 문단의 내용만 갖고서 코드로 표현하면 다음과 같다.

```Kotlin
var 화가 지갑 = 0
var 화가가 갖고 있는 그림 = 1

var 손님 지갑 = 20000
var 손님이 갖고 있는 그림 = 0
var 손님은 그림을 갖고 싶다 = true

if (10000 >= 손님 지갑 && 손님은 그림을 갖고 싶다) {
    손님 지갑 -= 10000
    화가 지갑 += 10000
    손님이 갖고 있는 그림 += 1
    화가가 갖고 있는 그림 -= 1

    손님은 그림을 갖고 싶다 = false
}  
```

Kotlin 컴파일러는 위에서부터 읽으며 모든 내용을 절차대로 수행할 것이다.  
이때, 만약 손님이 1명이 아니라 여러 명이라면 코드는 계속해서 저 코드를 부분적으로 반복하며, 많은 줄을 작성해야할 것이다.


![](https://memegenerator.net/img/instances/58100671/no-way.jpg)

그렇다. 굉장히 귀찮은 작업이며, 이것을 해결하기 위해 나온 것이
절차적 프로그래밍과 객체 지향 프로그래밍이다.


> 잠깐, 절차적 프로그래밍 ?
> 절차적 프로그래밍은 함수의 재호출을 이용해 코드를 재활용하는 방법을 의미한다.
>
>  즉, 컴파일러가 위에서부터 아래로 순서대로 읽는 것과는 별개로 (애초에 모든 코드는 절차적이다.) , 함수같은 Procedural 를 재활용하자는 의미에서 Procedural Programming 인 것이다.

> 이 글에서 절차적 프로그래밍은 함수를 통해 코드를 재활용한다는 의미로만 사용하고, 그 이상의 내용은 다루지 않는다.

<br/>
<br/>

## 객체 지향 프로그래밍(Object Oriented Programming)
객체(Object) 를 지향(Oriented) 하는 프로그래밍은 코딩을 작성할 때 사용할 수 있는 하나의 패러다임, 더 일반적으로는 하나의 글쓰기 장르라고 볼 수 있다.

객체를 지향한다고 하니, 객체가 무엇인지 알아보자.  
여기서 말하는 `객체` 란 하나로써 존재할 수 있는 무언가를 의미한다.
사람, 고양이, 우주, 자동차 등이 될 수 있다.

언급된 객체들의 특징은 자신이 `주체` 가 될 수 있다는 점이다.  
고양이는 고양이로서 존재할 수 있고, 우주는 우주로서 존재할 수 있다.  
고양이를 이루는 것 중에는 털이 있지만, 털이 조금 빠진다고 고양이가 고양이가 되진 않는다.
털이 빠진 고양이가 될 순 있지만.  

굉장히 관념적이지만, 여기서 말하는 `객체` 가  
하나로서 존재할 수 있는 어떤 `추상적인 무언가` 로 이해했다면 완벽하다.  


객체 지향 프로그래밍은 프로그래밍을 짤 때 `객체` 단위로 코드를 작성하기를 `지향` 한다는 것이다.

![](https://lh3.googleusercontent.com/OaYdR_8N0Q0jB3trpJ7zugia-hB9YCVNnp-hf7AvFZaTjiu76PKW_PuZO7k8CsIX1hiO9eHwnJs6hs64fsQaJ8vf6TDq1f0uLctRTv8vE-4G9R2VYKL2SfCDXLHbnJIFRyEroQPyvgi6pkTIk9rck-Zix5S2iXIAAga7U7WeXYVWXufOITFEsU8m-ONs1ZRjlBZMmo8dokFvH8wazRPYUPYXQDjjFhKgCYaDFKWd7Pi_9y_p-GQbqJW1N_Xk4SptGKm0U-_LWbQaj4sqmJ3ylfafXLCm6euydvwN31B_HNRA8Sr7Klf_J0SyUh7vo3u-CDFgZ8ufpyZnAtaS7cwu3Y3WLPJTKss4yUlrCkKsWLkYha6TPn6MGlzPgXLY8LIRNlHCsvHCRn53YCNVztBT57SO7SbFnhOJqqk4u_Aq3QCUC160MmmsG7SgWGQpao2trGzLjS87_wsvwGBDO1weDEK9BmLi81jtVmEoKv3eJkqbqT-6V44WqY9OubcopDvE3N_v7jb-3XQTpqLcTuZd4zwYyzoimNOHsS7WCc4h_2fLZ72Uf_go8e2oGKkXohlx0XNFLU0_eqHscepPzlKWF32gH9otbYcrPJoNYm6PflFH0c-U8XIbXOlPDH08FnOV0No5-4_uD-Eo895IxfVbfkD_kyAiwKpHCGn_FJE-GjJY3JBIkuJ5LkuywqAP3rkz2YvaLfQHQWLCzv_6T1s2eEY=w1132-h1063-no?authuser=0)

고양이라는 하나의 객체에는 성격, 근육, 털, 행동 등등 여러가지 것들이 포함될 수 있다.  
어떠한 것들은 있을 수도 있고, 없을 수도 있지만 `고양이` 라는 객체는 존재하며,

이 같은 생각을 바탕으로 코드를 작성하겠다는 패러다임이 바로 객체 지향 프로그래밍(Object Oriented Programming) 이다.

<br/>


## Kotlin 과 객체 지향 프로그래밍
코틀린으로 실제 객체, 고양이를 작성을 해보자.

위에서 언급한 하나로서 존재할 수 있는 `객체`, 즉 고양이는 `Class` 로 정의되며, 그 내부의 털, 성격, 근육 등은 `변수` 혹은 `함수` 로 정의할 수 있다.


```Kotlin
fun main(){
  val cat = Cat()
  
  println("눈동자는 ${cat.눈동자}, 털은 ${cat.털}, 성격은 ${cat.성격}")
  
  cat.털 = "깎아버리기!"
  cat.눈동자 = "까망색"
  println("${cat.털}, ${cat.눈동자}")

  cat.밥과 관련된 행동(true)
}

class Cat(){
   val 눈동자: String = "Blue"
   var 털: String = "너무 많아"
   val 성격: String = "커여워"

   fun 밥과 관련된 행동(밥: Boolean){
      if(!밥){
         println("냥냥펀치!!")
      } else {
         println("와구와구")
      }
   }
}
```
```Kotlin
결과
눈동자는 Blue, 털은 너무 많아, 성격은 커여워
눈동자는 Blue, 털은 깎아버리기!, 성격은 커여워
와구와구
```

- 클래스는 다음과 같이 미리 class 를 만들어 놓은 후, 변수로 선언하여 사용할 수 있다. 클래스의 내부 변수 접근은 `.` 으로 할 수 있다.


- class 로 정의된 변수 중, var 변수는 외부에서도 변경이 가능하지만 val 변수는 변경이 되지 않기 때문에 털은 변하되 눈동자는 변하지 않는다.


- 클래스 내부 함수 접근 역시 `.` 로 할 수 있다.


<br/>


한편, 클래스도 매개변수를 받을 수 있다. 같은 내용을 매개변수를 받는 형태로 바꾼다면 다음과 같다.

 ```Kotlin
fun main(){
  val cat = Cat()
  
  println("눈동자는 ${cat.눈동자}, 털은 ${cat.털}, 성격은 ${cat.성격}")
  
  cat.털 = "깎아버리기!"
  cat.눈동자 = "까망색"
  println("${cat.털}, ${cat.눈동자}")

  cat.밥과 관련된 행동(false)
}

class Cat( val 눈동자: String = "Blue", 
           var 털: String, 
           val 성격: String = "커여워") 
{
      fun 밥과 관련된 행동(밥: Boolean){
           if(!밥){
              println("냥냥펀치!!")
           } else {
              println("와구와구")
           }
      }
}
```
```Kotlin
결과
Error --> 매개변수 값을 선언해주세요.
눈동자는 Blue, 털은 깎아버리기!, 성격은 커여워
냥냥펀치!!
```

- 클래스의 매개변수는 val, var 타입이 올 수 있으며 val 은 변경 불가, var 은 변경 가능이다.

- 클래스의 매개변수는 Cat 의 눈동자와 같이 기본값을 줄 수도 있고, 털처럼 기본값을 안줄 수도 있다. 기본값을 주지 않은 매개변수는 선언 시 반드시 매개변수값을 넣어주어야 한다. 기본값이 있는 곳에 새로운 매개변수 값을 넣으면 새로운 값으로 덮어쓴다.

  <br/>

이렇게 작성된 코드는 반복작업도 굉장히 간편하다. 밥과 관련된 행동을 반복하고 싶다면 다음과 같이, 코드 한 줄이면 반복 작업을 수행할 수 있다.


```Kotlin
fun main(){
  val cat = Cat()

  cat.밥과 관련된 행동(false)
  cat.밥과 관련된 행동(true)
  cat.밥과 관련된 행동(true)
  cat.밥과 관련된 행동(true)
}

class Cat( val 눈동자: String = "Blue", 
           var 털: String, 
           val 성격: String = "커여워") 
{
      fun 밥과 관련된 행동(밥: Boolean){
           if(!밥){
              println("냥냥펀치!!")
           } else {
              println("와구와구")
           }
      }
}
```  

```Kotlin
결과
냥냥펀치!!
와구와구
와구와구
와구와구
```

  <br/>


한편 같은 객체이지만, 서로 다른 존재를 부르고 싶을때도 간편하다.
 ```Kotlin
fun main(){
  val catBlue = Cat("Blue", "너무많아!", "도도해!")
  val catBlack = Cat("Black", "조금있어!")
  val catOdd = Cat("Odd", "깍어비리기!!", "나른해")

  println("${catBlue.눈동자}, ${catBlue.털}, ${catBlue.성격}")
  println("${catBlack.눈동자}, ${catBlack.털}, ${catBlack.성격}")
  println("${catOdd.눈동자}, ${catOdd.털}, ${catOdd.성격}")
}

class Cat( var 눈동자: String, 
           var 털: String, 
           val 성격: String = "커여워") 
{
      fun 밥과 관련된 행동(밥: Boolean){
           if(!밥){
              println("냥냥펀치!!")
           } else {
              println("와구와구")
           }
      }
}
```  
```Kotlin
결과
Blue, 너무많아!, "도도해!
Black, 조금있어! 커여워
Odd, 깍어비리기!!, 나른해
```

<br/>

> 참고로 Class 를 직접 부르면 컴파일러는
>
>![](https://w.namu.la/s/d85d3c39fd3b225bc05fd8d64fb4f334200644f7154148283e6dc731e25f9ac20a52aafd3de51e7e88dcb35cf7582cfcea9c9b65e530ec41178ea063f131fcc70d0e3d5932c702d06310796913a7a2e7)
>
> 클래스는 직접 호출하지 않고, 반드시 변수 등에 선언을 하고서 사용해야 한다. 클래스는 수치만 들어간 설계도이기에 설계도를 직접 호출하면 당연히
실제 사용자는 ? 를 띄울 뿐이다.

  <br/>
  <br/>

### 정리
객체 지향 프로그래밍은 하나의 객체를 관점으로 프로그래밍을 작성하는 것을 의미한다. 반복적인 작업을 피하고, 이해와 효율성을 높이기 위해 사용된다.

Class 는 하나의 객체를 담는 그릇이다. 실제 치수, 내용 등을 포함하고 있지만 기본적으로 설계도이기에 사용 시 다른 변수에 선언을 하고서 사용해야 한다.

모듈화를 통해 코드 전체의 이해와 재사용으로 효율성이 높아진다.
단, 모듈화로 인해 컴파일러는 더 많은 코스트를 요구하여 성능에는 더 안 좋다. 또한 설계 자체에 시간이 오래 걸릴 수 있다.



감사합니다 :)
![](https://user-images.githubusercontent.com/80164141/138802009-f777c0cc-d1d1-4cde-8702-9c5e52329e74.gif)


<br/>
<br/>>

> 참고
> Udemy # [Android Jetpack Compose: The Comprehensive Bootcamp [2022]](https://www.udemy.com/course/kotling-android-jetpack-compose-/)
>
> Blog # [객체 지향 프로그래밍이 뭔가요? (꼬리에 꼬리를 무는 질문 1순위, 그놈의 OOP)](https://st-lab.tistory.com/151)