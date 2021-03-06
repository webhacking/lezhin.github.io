---
title: 'Kotlin의 빛과 그림자'
author: robin
date: 2017-08-03 11:10
tags: [kotlin]
---

[핀터레스트](http://pinterest.com)의 안드로이드 개발팀이 코틀린을 도입하면서 겪은 어려움과 해결책을 소개한
[The Case Against Kotlin](https://medium.com/@Pinterest_Engineering/the-case-against-kotlin-2c574cb87953)을 ~~foot~~번역하고 자의적으로 해석하고 요약했습니다.
저자 라이언 쿡(Ryan Cooke)은 현재 코틀린이 [가트너의 하이프 사이클](https://en.wikipedia.org/wiki/Hype_cycle)에서 "뻥튀기된 기대감의 산(Peak of Inflated Expectations)" 쯤에 있다고 말합니다.
레진시 개발동에서는 이미 코틀린을 부분적으로 도입했고, 현재는 범위를 넓혀가는 중인데요... 정말 괜찮은 걸까요?
<!--more-->

![](/files/2017-08-03-the-case-against-kotlin/kotlin_in_hype_cycle.png)

## 문제: 학습 곡선

* 자바 개발자로서 문법에 익숙해지는 데 1주일 정도 걸립니다.
* 코틀린을 이미 잘하는 사람이 없으면 베스트 프랙티스들을 찾아보면서 해야하는 데 시간이 듭니다.
* 코틀린 사용을 가속화 시키는 데 팀 트레이닝을 계속 해야합니다. -> 기회비용 많이 듭니다.
	* 하기 싫어 하는 사람도 있고...
	* 혼자서 알아서 잘 배우는 사람도 있고...

## 해결책: 학습 곡선

* 코틀린은 아직 ~~말년병장~~성숙한 언어가 아닙니다! 지금도 자라나고 있습니다! ~~그게 제일 무서워..~~
* 책도 있고 인터넷 리소스도 있지만, 코틀린 신봉자가 하나 있어서 다 가르쳐주는 게 짱입니다.
* 필자가 코틀린을 하고 싶었던 이유는 생산성인데요, 동료들 중에는 그렇게 느꼈던 사람들이 많지 않은 것 같습니다. 정착이 되면 보이겠죠.

## 문제: 빌드 속도

* Gradle 빌드 속도는 보통 30초, 클린 빌드는 75초 까지 걸립니다.
* 코틀린은 보통 빌드 속도의 25%, 클린 빌드의 40% 밖에 안나옵니다.

## 해결책: 빌드 속도

* ~~알아서 하셈 ㅋ~~
* 코틀린 파일 하나 변환 -> 클린 빌드 시 조금 시간이 더 걸립니다. 파일을 많이 변환할수록 느려지긴 하지만 체감하긴 어렵습니다.
* 보통 빌드할 때는 코틀린 파일 많아도 상관 없습니다.
* 결론: 클린 빌드할 때 느려진다는 걸 체감할 겁니다.

![](/files/2017-08-03-the-case-against-kotlin/kotlin_deal_with_it.gif)

## 문제: 개발 안정성

* 코틀린의 문법이나 특성이 문제가 아니라, 코드를 생산성 있게 작성하는 자신을 막는 새로운 문제들 때문이라고 생각합니다.
	* 사실 그냥 코틀린 배우기 싫은 거 같아요.
* 예를 들면, 코틀린 애노테이션 프로세서 툴(`kapt`) 때문에 빌드가 안 되고, 무조건 클린 빌드로만 개발을 했던 적이 있습니다.
	* 이거... 코틀린 때문 아니야?!?!?! 하는 의심들 많았죠.
	* 고치느라 시간이 많이 흘렀습니다.
	* 또 어떤 문제가 튀어나올지에 대한 두려움이 커지네요.

## 해결책: 개발 안정성

* 그냥 IDE 나 언어의 stable 버전만 업데이트 하세요.
	* 안정된 버전들만 사용하면 그나마 힘든 일 없을거예요.~~정말?~~

## 문제: 정적 분석

* FindBugs, PMD, Error Prone, Checkstyles and Lint
	* Java 는 이와 같은 툴들로 인해 Code Review에 쓸데없는 걸 줄이거나 룰을 적용할 수 있는데,
	* 코틀린에는... 이런 게 없... 분석을 위한 게 아직... 없습니다... 사람들이 알아서 다 찾아야 합니다.

## 해결책: 정적 분석

* 그냥 ~~손가락빨고~~ 기다려야 합니다. 아니면, 직접 만드세요!

## 문제: 나 돌아갈래~ 

* 돌아가기 쉽지 않습니다. 자바를 코틀린으로 옮기기에는 쉬운데, 반대는... 어렵습니다!
	* 코드가 깨지고, 변수명부터, 이런 저런 부분들을 다시 구현해야합니다.
	* 코틀린스럽거나, 코틀린의 고유한 기능들을 사용했다면, 여기서부터 헬이죠.

![](/files/2017-08-03-the-case-against-kotlin/seol_in_peppermint_candy.jpg)

## 해결책: 나 돌아갈래~ 

* 되돌아오는 건 쉽지 않기 때문에 잘 생각해야 합니다.
* 유닛 테스트가 정말 잘 된 파일들부터 바꾸세요.
* 간단하고 재사용 가능한 잘 모듈화된 파일들을 먼저 바꾸세요.

## 결론

* 이 글은 고려해야 할 리스크에 대해서 나열했습니다.
* 단점들은 구글과 젯브레인과 스택오버플로우가 차차 해결해 줄 겁니다.
* TL;DR 코틀린으로 작성하는 건 쉽지만, 되돌리기는 어렵습니다.

![](/files/2017-08-03-the-case-against-kotlin/seol_in_silmido.jpg)

> 그래서 말인데... [레진코믹스에서 코틀린 삽질을 함께 할 개발자를 모십니다!](/recruit)

