<div align="right">> Created : 2022.08.25</div>

> ## Overview
- 회사에서 어쩌다보니, 크로스 브라우징에 대해 세미나를 진행하게 되었는데,
<br> 정리해두면 좋을 것 같아서 마크다운의 형태로 기록합니다.
- 웹 서비스는 다양한 브라우저에서 제공되고 있는데, 
<br> 브라우저 엔진에 따라 다른 레이아웃과 렌더링 방식을 갖고 있습니다.
<br>

- 이에 따라 개발 언어를 다르게 해석하여 화면에 렌더링 하게 되는데 
<br> 해석 방법에 따라 같은 코드가 화면에 다르게 표현 될 수 있습니다.
<br>

- 이러한 상황에 대응하기 위해 등장한 Cross-Browsing에 대해 
<br> 간단하게 정리합니다.
<br><br>

> ## What is Cross-Browsing ? 

- W3C에서 채택된 표준 웹 기술을 적용해 모든 브라우저에 다른 기종의 OS나 <br> HTML 렌더링 기술로 비슷하게 만들어 어떤 환경에서도 이상없이 작동되게 <br> 하는 웹페이지를 제작하는 방법론 입니다.

- **"크로스 브라우징은 동일성이 아니라 동등성(등가성)을 의미한다."**

- 동일하게 만드는 것이 아닌 각자의 브라우저로 웹사이트에 방문했을 때 
<br> 정보 공유에서 소외감을 느끼지 않도록 하는 것이 크로스 브라우징이 
<br> 추구하는 방향 입니다.
<br><br>
> ## Considerations

- 크로스 브라우징을 고려하기 위한 방법들을 몇가지 정리하였습니다.
<br><br>

  ### **1. 고려 해야 할 브라우저를 선별** 
      모든 브라우저를 대응하여 개발하는 것은 사실 상 어렵습니다. 
      주로 대응할 브라우저 들, 이외의 브라우저 정도로 나누어 개발 하는 것이 현실적인 방법 입니다.

  - [세계 브라우저 사용 통계율](https://gs.statcounter.com/) <br><br>

  ### **2. Javscript 의 Class 함수 사용에 유의**
      Javascript 에서 제공하는 Date 등의 일부 객체를 생성하는 클래스 함수가 
      브라우저 별로 사용 방법이 다른 경우가 있습니다. 지원 여부를 꼭 확인 하고 사용해야 합니다.

  - [Classes - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes) <br><br> 


  ### **3. W3C, MDN 등에서 웹 표준 규칙을 참고하여 속성들을 분류**  
      W3C 에서는 웹 표준 규칙을 정의하고, 가이드 라인을 제시하고 있습니다.
      MDN 에서는 사용 문법 별 지원 브라우저의 버전, 종류를 상세히 나타내주고 있습니다.
      이를 참고하여 규칙을 정한 후 개발하면 크로스 브라우징 대응에 조금 더 수월 할 것 입니다.
  - [World Wide Web Consortium (W3C)](https://www.w3.org/)
  - [MDN Web Docs](https://developer.mozilla.org/ko/) <br><br>

  ### **4. CSS Framework 를 사용**  
      BootStrap, Mui 등의 사용률이 높은 CSS Framework 들은 
      Cross Browsing을 고려하여 만들어졌습니다.
      각 프레임 워크에서 제공하는 속성들을 이용해 CSS를 적용 시킨다면 어느정도 대응이 가능합니다.
  - [Bootstrap](https://getbootstrap.com/)
  - [MUI: The React component library you always wanted](https://mui.com/)
<br><br>

  ### **5. 브라우저 분석 도구를 이용하여 분기처리**
      javascript 에서는 navigator 객체로 어느정도 브라우저 환경을 유추할 수 있습니다.
      Modernizr 는 현재 이용중인 웹 브라우저에서 HTML5와 CSS3의 명세에 정의된 기능 중 어떤 기능을 
      지원하는지를 알아볼 때 사용하는 오픈 소스 라이브러리 입니다.
      위와 같은 브라우저 분석 도구를 사용하여 각 브라우저에 맞게 개발을 하는 방법이 있습니다.
  - [Window.navigator](https://developer.mozilla.org/ko/docs/Web/API/Window/navigator)
  - [Modernizr: the feature detection library for HTML5/CSS3](https://modernizr.com/)
<br><br>

  ### **6. 테스트**
      한 가지의 브라우저 환경에서 개발을 진행하게되면 크로스 브라우징을 놓치기 쉽습니다.
      개발 중간중간 다양한 디바이스, 브라우저 환경에서 테스트를 하며 개발을 진행하면 좋습니다.
      여러 디바이스를 가지고 있지 않은 경우, 웹 미러링 기반의 테스트 툴을 사용하여 
      테스트를 진행 할 수 있습니다.
  - [TestGrid](https://www.testgrid.io/)
  - [LambdaTest](https://www.lambdatest.com/)

> ## 마무리

- 방법이야 여러가지 있지만, 결국은 개발자의 꼼꼼함이 더 나은 결과물을 만드는 것 같습니다.
- 사소한 것도 그냥 지나치지 않는 검토 습관을 들이는 것이 중요합니다.
