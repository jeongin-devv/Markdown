<div align="right">> Created : 2022.09.14</div>

## Overview
모바일 웹페이지에 Firebase Dynamic Link 를 이용하게 되었는데,
작업 하기에 앞서 딥링크에 대한 기본 내용을 정리한다.

## DeepLink?
> 앱의 특정 기능 또는 특정 화면에 도달할 수 있는 링크 정보(URL)이다.

즉, 특정 컨텐츠에 직접 도달하는 모든 링크를 의미한다.
<br>일반적으로 `Scheme://Path` 형태를 가지는데, 여기서 Scheme 은 특정 앱을 가르키고 Path 는 Uri 를 담고 있다.
<br>(ex. `kinemaster://detail?no=1`)

## Distinction of Deep Link
DeepLink는 크게 세 가지의 방식으로 구분된다.
> 1. URI Schemes - iOS
> 2. Universal Links - iOS
> 3. Android App Links - AOS

### 1. URI Schemes
애플의 iOS-9 이전까지의 표준 딥링크 형식이다.
<br><br>URI Scheme은 커스터마이징을 지원하여 딥링크를 구현할 수 있는데,
예를 들어 `kinemaster://detail?no=1`와 같이 특정 컨텍스트 데이터로 앱을 실행할 수 있다.
<br><br>
하지만, **앱이 설치되지 않은 경우**에는 에러 페이지로 이동하게 되며, 
고유한 값이 아니기 때문에 여러가지 앱이 동일한 링크인 `kinemaster://`에 응답하려 하는 경우가 발생한다. 
<br><br>
URL과 달리 중앙 등록 시스템이 존재하지 않기 때문에 이에 대한 문제를 해결하고자 
애플은 2세대 표준 딥링크 형식인 유니버셜 링크(Universal Links)를 제공한다.

### 2. Universal Links
애플의 iOS-9부터 그 이후의 표준 딥링크 형식이다. 
<br><br>URI Schemes 와는 다르게 웹페이지와 내부의 특정 컨텐츠를 가리키는 표준 웹 링크이며, 
도메인 주소를 딥링크의 실행 값으로 사용하게 되어 `kinemaster.com/detail?no=1`을 입력하면 앱이 바로 오픈한다. 
<br><br>
즉, 웹페이지 주소를 사용한 딥링크이며,
<br> AOS의 Android App Links도 Universal Links 와 같은 원리로 작동한다.

하지만 딥링크 방식들이 **모든 앱에서 작동하지는 않는다.**
<br>결국 원활한 광고 운영을 위해서는 모든 딥링크 연동이 필요하다.

### 3. Dynamic Link
**Google Firebase** 에서 제공하는 서비스이며, 
<br>Dynamic Link 또한 Deep Link 이다.
기존의 Deep Link의 경우 안드로이드, iOS에 따라 각각 구현해야 했지만, Dynamic Link 는 **플랫폼 관계 없이** 
링크를 만들면 앱이 있으면 해당 콘텐츠로 바로 이동하고 없으면 마켓으로 이동하여 설치 후 해당 컨텐츠로 이동할 수 있게 하는 기술이다.

### 4. 마치며
지난 경험 동안은 애플리케이션 개발자들과 수직적인 구조로 일을 했다보니, 앱과 연관된 웹 기술들에 대해 탐구할 여력이 없었다.
주니어와 시니어의 차이는 이런 작은 경험들이 얼마나 모이는가의 차이가 아닐까? 
