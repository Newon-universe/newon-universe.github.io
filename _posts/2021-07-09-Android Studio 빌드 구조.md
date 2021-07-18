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

안드로이드 스튜디오에서 사용되는 Manifest 는 특별한 설정이 없다면 무조건 생성되는 파일로, 의미 그대로 안드로이드 스튜디오에서 어떤 빌드를 명확하게 보여주는 파일이다.  
빌드를 왜 설명할까? Visual studio나 어떤 IDE를 사용하더라도 C언어나 Java script 코드를 작성한 후에 컴파일이나 빌드에 관한 설명을 한 기억은 없는데 안드로이드 스튜디오는 빌드에 관한 설명이 필요한걸까?  
그 이유는 안드로이드는  