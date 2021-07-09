---
title : "Android Studio에서 Manifest 란?"
category :
    - Kotlin
tag : 
    - Kotlin
    - Android Studio
    - TIL
use_math : true
use_mermaid : true
toc : true
author_profile: true
sidebar:
    nav: "sidebar"
---

## 앱 매니페스트(Manifest)란 
매니페스트 (Manifest) 를 영어사전에 검색하면 '명백한' 의미를 가진 형용사라고 나온다. 더 정확하게, 영어 사전의 의미에서는 동사로 사용될 땐 `표시나 행동을 통해 무언가를 명확하게 보여주는 것을 의미한다.` ~~사실 전문용어(terminology)로 분류되어 관계자 외엔 잘 안쓰인다고 한다.~~
<img width="550" alt="Manifest 사전적 의미" src="https://user-images.githubusercontent.com/80164141/125058672-7af5e500-e0e5-11eb-8049-a209cb612a1a.png">  

안드로이드 스튜디오에서 사용되는 Manifest 는 특별한 설정이 없다면 무조건 생성되는 파일로, 의미 그대로 안드로이드 스튜디오에서 `빌드`를 명확하게 보여주는 파일이다.  

빌드를 왜 설명할까? Visual studio나 어떤 IDE를 사용하더라도 C언어나 Java script 코드를 작성한 후에 "어떻게 컴파일을 하세요, 어떻게 빌드를 하세요."와 같은 내용을 작성한 기억은 없는데 안드로이드 스튜디오는 빌드에 관한 설명이 필요한걸까?  

그 이유는 안드로이드 스튜디오는 코드 작성과 빌드가 구분되어 있기 때문이다. 더 정확하게는 안드로이드 스튜디오는 코드 편집만 기능하는 IDE 일 뿐이고, 빌드는 gradle 파일에서 설정을 하고 AAR(Android ARchive) libraries 나 JAR(Java ARchive) libraries 등을 받아서 수행하기 때문이다. 더 자세한 [설명은 여기로]().  

매니페스트 파일은 이렇게 분리되어 있는 코드와 빌드에 대한 연관 관계 및 코드 수행 시 알아야할 필수 정보들을 모아놓은 파일이다. `이 코드들을 빌드하기 위해선 이런 설정과 정보들을 알아야 한다고` 라고 말하는 것이 Manifest 파일이니, `표시나 행동을 통해 무언가를 명확하게 보여주다.`라는 의미를 한 껏 살린 참으로 긱스들스러운 표현이다.  

한 줄 요약하면 Manifest = 안드로이드 스튜디오 빌드 설정 파일

---
## 매니페스트(Manifest) 의 구성
매니페스트는 `AndroidManifest.xml` 명칭으로 프로젝트 내부에 있어야 한다. _별도의 지정을 하지 않으면 src/main 으로 간다고 하지만, manifest 디렉토리에 있기도 한다._ 매니페스트 파일은 Android 빌드 도구, Android 운영체제 및 Google Play 에 앱에 관한 필수 정보를 설명하게 된다.  
<br/>
매니페스트 파일은 다음 4개의 내용이 반드시 선언되어야 하는데,
* 앱의 패키지 이름  
* 앱의 구성 요소 (모든 액티비티, 서비스, Broadcast Receiver, 콘텐츠 제공자 포함)  
* 앱이 시스템 또는 다른 앱의 보호된 부분에 액세스하기 위해 필요한 권한.  
* 앱에 필요한 하드웨어 및 소프트웨어 기능  

###### 앱의 패키지 이름 (APK name)

앱의 패키지 이름, APK(Android aPplication Package) 이름에 대한 선언이 필요하다.
다음은 매니페스트 파일의 일부로, \<manifest\> 내부에 package = "com.example.flip"으로 된 부분이 APK의 선언에 해당한다.

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.flip">                 // APK 이름 선언
...
    <activity
        android:name=".MainActivity"
        android:exported="true">
...
```

매니페스트 내에서 선언된 APK는 2개의 역할을 수행한다.  

첫째로, 매니페스트에서 선언한 패키지 이름은 App Resource 에 접속하는데 사용되는 R 클래스의 네임 스페이스 (_개체를 구분할 수 있는 범위, 변수명, 함수명 등이 해당된다._) 로 적용된다.  
` TMI 1. R 클래스에는 R.Java 가 있는데, 리소스 접근을 위한 ID 들을 모아놓은 파일로 이처럼 R클래스는 리소스에 접속할 때 사용되는 클래스이다.`
` TMI 2. 위의 manifest 코드대로라면 com.example.flip.R 로 생성된다. `

둘째로, 매니페스트에서 선언한 패키지 이름은 파일 내에서 선언된 다른 코드들의 상대경로가 된다. 위의 코드에서 MainActivity 의 최종 경로는 com.example.flip.MainActivity"가 된다.

###### 앱의 구성 요소 (App Components)
앱의 구성 요소 (액티비티, 서비스, Broadcast Receiver, 콘텐츠 제공자를 포함) 들을 사용하고 싶다면 매니페스트 파일에서 선언해주어야 한다. 매니페스트 파일 내부에서 각각 다음과 같이 사용할 수 있다.
```
<activity> : Activity 이름 및 내용
<service>  : Service 이름 및 내용
<receiver> : Broadcast Receiver 이름 및 내용
<provider> : Provider 이름 및 내용
```

위의 컴포넌트들은 인텐트에 의해서 활성화된다. 인텐트란 메세지 객체로, 어떤 행동을 수행할지에 대한 명령이나 작업에 필요한 데이터를 포함합니다. 다음은 프로젝트 명을 flip으로 생성한 후 설정을 건드리지 않은 매니페스트의 코드이다.
```
...
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        
...
```
_\<activity\> 태그 내부에 \<intent\> 태그로 액션과 카테고리를 지정해주는 모습을 알 수 있다._  
<br/>
앱이 인텐트를 시스템에 발행하면 시스템은 각 앱의 매니페스트에 선언된 intent-filter 에 기초하여 처리할 수 있는 인텐트를 컴포넌트를 찾게 된다.  만약 여러 개의 앱이 인텐트를 다룰 수 있다면, 사용자가 해당 인텐트를 어떤 앱에게 넘길지 선택할 수 있게 된다.
 
그리고 매니페스트에 선언된 컴포넌트들과 <application> 은 유저에게 보여줄 수 있는 icon 과 label 속성을 갖고 있다. 그리고 xml 로 구성하다보면 트리 구조기 때문에 부모-자식 관계가 생기되는데, 이때 자식 element에 icon 과 label 이 설정되어있지 않다면 부모에 설정된 값이 기본 값으로 설정되게 된다. 그렇기 때문에 각 컴포넌트마다 설정하지 않고 앱 전체에 기본 값을 설정하려면 <application> 에 설정하면 된다.
