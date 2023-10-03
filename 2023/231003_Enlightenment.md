<div align="right">Created : 2023.10.03</div>

# **Enlightenment**

홍익대학교 정보전산팀에 온지 벌써 3주가 지났다. <br>

첫 회사에서 주로 사용했던 `Java` 를 다시 만나게 되었고, <br>
`React` 와 `Next.js` 를 사용하면서 잊고 있던 `Jsp`를 사용하게 됬다. <br>

그리고 처음 웹 개발을 공부 했을때 잠깐 접해보았던 `Model 1`의 구조를 <br>
실무 단계에서 처음 사용하게 되었다. <br>

이전에 사용해보았던 언어와 환경이지만, <br>
그때와 지금의 느낌이 너무도 다르고, 새롭게 알게된 것들이 많아서 <br>

이에 대해 기록하고자 한다. <br><br>


## **서버 사이드 렌더링**

이전까지는 주로 `Rest API` 와 사용하기 위해 <br>
서버사이드와 독립적인 클라이언트 사이드를 구축해서 사용했다. <br>

여기서 인증과 보안, 민감 정보를 서버 사이드에서 관리할 필요를 느끼고 <br>
양 사이드를 모두 사용할 수 있는 `Next.js` 를 도입해서 사용했다. <br>

그때 가장 힘들게 느껴진건, <br>
독립적인 클라이언트 환경에 익숙해진 상태에서 <br>
어디까지 서버 사이드에서 처리하고, 어디까지 의존해야하는가? 에 대한 <br>
고민이 가장 많았고, 그것이 팀에서 주로 다루는 문제였다. <br>

하지만 여기서 접한 `Model 1`은 그동안 해왔던 모든 고민들이 <br>
전혀 의미가 없었다. <br>

최소한의 코드로 최소한의 기능을 구현하면서, <br>
모든 것을 서버사이드에서 처리하는 구조에서 작업을 진행하면서 <br>

이런 부분은 클라이언트 사이드에서 처리하면 서버의 부하를 줄일 수 있을 것 같은데 <br>

라는 생각을 하다보니, 자연스레 `Next.js` 에서 고민했던 문제들이 해소되었다. <br>

예를 들면 배열의 완전 탐색이나 리모델링의 경우, <br>
`Java`에서 처리하는 것 보다, `Javascript`에서 제공하는 배열 관련 메서드가 <br>
처리속도가 빠르기 때문에 이런 부분에 대해서는 클라이언트 사이드에서 데이터를 처리하고, <br>
민감 정보나 서버 세션에서 관리하는 데이터의 경우, 서버사이드에서 처리를 하는 등의 <br>
방법들이 있다.<br><br>

지금 환경에서나 추후 다시 프레임워크를 사용할 때, <br>
클라이언트와 서버의 기능을 확신을 가지고 분리할 수 있을 것이라는 생각이 들었다. <br><br>


## **프레임워크가 꼭 필요한가?**

개발에는 수많은 언어들이 있고, 이에 대응하는 수많은 라이브러리와 프레임워크가 있다. <br>

많은 사람들이 필요로 하는 기능들이 라이브러리로 구현되어있고, <br>
이러한 라이브러리들이 모여 하나의 프레임워크를 제공하면서 개발의 편의성을 제공하고 있다. <br>

나는 그동안 `Spring`, `Spring Boot` 와 같은 자바 프레임워크를 사용해왔고, <br>
`Vue.js`, `React`를 기반으로 한 `Next.js` 와 같은 자바스크립트 프레임워크를 사용했다. <br>

이전에도 제목과 같은 생각을 한 적은 있다. <br>
`Micro Service Architecture` 에서 여러개의 작은 서비스들을 구현할때 <br>
매번 같은 번들러로 똑같이 환경을 구축해서 서비스를 하나씩 만들어야 하는가? <br>

이곳에서 그에 대한 해답을 찾았다. <br>
프레임워크는 필수가 아닌 선택이다. <br>

금융권이나, 공공기관에서는 폐쇄망에서 개발을 진행하는 경우가 많다. <br>
이 때 Maven 이나 Gradle 을 사용하는 프레임워크의 경우, 보안을 위협 받을 수 있고, <br>
오픈 소스로 구현되어있고, 누구나 수정 / 개발에 참여할 수 있는 `npm` 내의 라이브러리들은 <br>
문제가 생겼을 경우, 책임소재가 불명확해진다. <br>

특히나 내부에서 사용하는 `BackOffice Service`를 `MSA`의 형태로 구현하게 될 경우에는 <br>
빠른 개발 속도와 작은 크기의 소스 파일이 요구되는데, <br>
여기서 프레임워크는 굳이 필요하지 않을 수도 있겠다. 라는 생각이 들었다. <br><br>


## **정리**

진작 깨달았어야 되는 것인데, 이제서야 생각이 들었다. <br>
개발은 결국 서비스를 개발하고 제공되는 기업의 특성을 얼마나 이해할수 있는지가 중요하다. <br>

결국 개발자는 어떤 언어나 기술을 사용하는가가 아닌, 어떠한 서비스를 만드는 사람이니까. <br>

타이핑 기계나 코더가 아닌, 개발자가 되기 위해 어떻게 생각하면서 업무를 해야하는지, <br>
가장 개발에 보수적인 집단이라고 생각했던 학교에서 깨닫게 되었다. <br><br>

기본에 집중하기. <br>