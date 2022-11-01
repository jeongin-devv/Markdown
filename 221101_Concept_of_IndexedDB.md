<div align="right">Created : 2022.11.01</div>

## **Overview**

`Web API` 에서 제공하는 `Web Storage`를 사용하여 웹 페이지에서 보존 해야 할 정보들을 저장해놓고 불러와서 사용하는 형태의 기능을 많이 구현했었다.

모바일 웹에서 Step by Step 형식의 페이지, 보편적인 웹에서 검색 기록, 페이지 이동, 컨텐츠 탐색 등의 기록을 저장하는 형태의 기능들을 예시로 들 수 있다.
<br>
하지만 최근 들어 `Web Storage`를 사용하는 데에 있어 **용량 제한, 데이터 타입의 강제성, 보안 이슈 등**과 같은 몇가지 문제에 부딫히게 되었다. 
<br><br>
실제로 이와 같은 문제들로 인해 `Google`의 `Chrome Browser` 개발 팀에서는 `Web Storage` 이외의 다른 스토리지 메커니즘을 권유한다. 
<br><br>
| - | 저장 용량 | 모델 | 트랜잭션 | 통신 | 비고 |
|:-:|:-------:|:---:|:-----:|:-----------:|:---:|
|IndexedDB|대용량|하이브리드|O|비동기|-|
|Session<br>Storage|5,10MB<br>Only String|Key-value|X|동기|동일 탭 내에서<br>유효|
|Local<br>Storage|5,10MB<br>Only String|Key-value|X|동기|-|
|Cookies|Only String|구조적|X|비동기|패킷이 한번에<br>전달되면서<br>데이터 비대화 
|File<br>System|-|Byte Stream|X|비동기|Chronium 기반<br> 브라우저에서만<br>동작
|Cache API|-|Key-value|X|비동기|-|
|Web SQL|-|-|-|-|버전 관리 중단|
<br>

이 중에서 최근 들어 사용률이 높아지고 있는, 범용성이 넓고 데이터 저장에 용이한 `IndexedDB` 에 대해 조사하고 정리한다. `IndexedDB`에 대해 정리를 하고나서 여력이 된다면 `Cache API`에 대해 정리해 볼 생각이다.
<br><br>
이 마크다운에는 `IndexedDB`의 개념에 대해 정리하고, 다음 글에서는 사용 방법과 예시 코드를 정리할 예정이다.
<br><br>

## **Indexed DB?**

`IndexedDB`는 파일이나 블롭 등 많은 양의 **구조화된 데이터를 클라이언트에 저장하기 위한 로우 레벨 API** 이다. `IndexedDB` API는 인덱스를 사용해 데이터를 고성능으로 탐색할 수 있다. `Web Storage`는 적은 양의 데이터를 저장하는데 유용하지만 많은 양의 구조화된 데이터에는 적합하지 않은데, 이런 상황에서 `IndexedDB`를 사용할 수 있다. 이 페이지는 `MDN`에서 `IndexedDB`에 대한 내용을 다루는 시작 문서로 전체 API 참고서, 사용 안내서, 세부적인 브라우저 지원 상황, 그리고 핵심 개념에 대한 설명을 제공하는 링크를 찾을 수 있다.
<br><br>

 > `IndexedDB` 는 많은 기능을 지원하지만, 간단하게 사용하기는 복잡 할 수 있다. 보다 편하게 사용하기 위해서는 라이브러리를 사용하는 것을 추천 한다.

 - `IndexedDB`는 [Web Workers][] 에서 사용 가능하다.

[Web Workers]: https://developer.mozilla.org/ko/docs/Web/API/Web_Workers_API

<br>

## **Key Concept**

`IndexedDB`는 SQL을 사용하는 `관계형 데이터베이스(RDBMS)`와 같이 **트랜잭션을 사용하는 데이터베이스 시스템이다.** 그러나 `IndexedDB`는 RDBMS의 고정컬럼 테이블 대신 `JavaScript` 기반의 `객체지향 데이터베이스(OODB)`이다. 
<br><br>
`IndexedDB`의 데이터는 **인덱스 키를 사용해 저장하고 검색**할 수 있으며, **구조화된 복사 알고리즘을 지원하는 객체라면 모두 저장**할 수 있다. 사용하려면 데이터베이스 스키마를 지정하고, 데이터베이스와 통신을 연 후에, 일련의 트랜잭션을 통해 데이터를 가져오거나 업데이트해야 한다.
<br><br>
> 대부분의 웹 저장소처럼, `IndexedDB` 도 `SOP`를 따른다. 그렇기 때문에, 저장한 데이터는 같은 도메인에서만 접근할 수 있으며 다른 도메인에서는 접근할 수 없다.
- `SOP` : Same-Origin Policy 의 약자로, Origin에서 로드된 문서 또는 스크립트가 다른 Origin의 리소스와 **상호 작용**할 수 있는 방법을 제한하는 중요한 보안 메커니즘이다. 쉽게 말하면 "**웹 브라우저에서 동작하는 프로그램은 로딩된 위치에 있는 리소스만 접근 할 수 있다**" 는 정책이다.
<br><br>

## **Features**

- **동기와 비동기** <br>
애플리케이션 블록을 방지하기 위해 모두 **비동기**로 이루어진다.

- **저장 용량 한도와 제거 기준** <br>
브라우저가 얼마만큼의 공간을 Web Data Storage에 할당할지 그리고 용량이 한계에 도달했을 때 무엇을 지울지의 프로세스는 간단하지 않고, 브라우저마다 다릅니다.

<br>

## **Substitute**

`IndexedDB` 는 일반적으로 사용하기에는 접근성이 떨어 질 수 있다. 개발자의 쉬운 사용을 위해, `IndexedDB`를 이용한 라이브러리들이 존재한다. 
기초부터 구현하고 학습할 시간적 여유가 없다면, 이러한 라이브러리들을 사용하는 것이 도움이 될 수 있다.

 - [LocalForage][]
 - [Dexie.js][]
 - [ZangoDB][]

[LocalForage]: https://localforage.github.io/localForage/

[Dexie.js]: https://dexie.org/

[ZangoDB]: https://github.com/erikolson186/zangodb
