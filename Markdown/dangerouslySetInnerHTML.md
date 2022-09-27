<div align="right">> Created : 2022.09.27</div>

> ## Overview
회사에서 몇몇 레거시코드들을 둘러보면 데이터베이스에서 데이터를 가져오는데, 
몇몇 데이터는 html 태그들을 포함한 String Data로 이루어져있다.

이를 React 내에서 직접 HTML 문을 변경 시킬 때 
JavaScript 함수인 `innerHTML` 대신 DOMElement의 일종인 `dangerouslySetInnerHTML` 를 사용하게 되는데,
'이러한 DOM 접근은 위험합니다' 의 내용을 `eslint` 에서 띄워준다.

이 이유에 대해 가볍게 정리하고, 처리 방법에 대해 기술한다.
<br><br>

> ## dangerouslySetInnerHTML?
HTML을 Interactive 하게 접근하여 변경해야 할 때, 
JavaScript의 innerHTML 등의 함수를 사용하여 일반적으로 코드를 작성 하는 것은 위험하다.

`XSS` 라고 불리는 `Cross Site Scripting` 공격에 취약해지게 되기 때문에
React에서는 JavaScript의 innerHTML 함수에 대한 대안을 제공하는데,
`dangerouslySetInnerHTML` 라는 `DOM Element` 속성이다.

하지만 이 속성을 사용한다고 해서 XSS 공격을 방지할 수 있는 것은 아니다. 
React에서 `dangerouslySetInnerHTML`를 사용 할 경우, esLint에서 XSS에 대한 경고 메시지를 띄워주며,
위험성에 대해 알려 주는 것에 불과하다.
<br><br>

> ## Sanitizer ? 
`XSS`를 방지하기 위해 `Sanitizer` 라고 불리는 전처리기를 많이 사용하고 있다.

`Sanitizer`는 전달 받은 String을 HTML 구문으로 분석하여 위험성이 존재하는 Script, 속성 등을 제거함으로 
악의적인 스크립팅 공격을 방지하고, 표준 문법을 사용할 수 있게 한다.

여러 라이브러리들이 있는데, 필자는 `dompurify`를 사용하여 데이터를 Sanitizing 후 활용 하였다.
<br><br>

> ## Example

짧은 코드로 예를 든다.

```javascript
  ...
  
  const exampleData : string = '<span>test</span>';
  
  const exampleFunction = (text : string) => {
    return <div dangerouslySetInnerHTML={{__html: exampleData}} />
  };
```
데이터베이스에서 가져온 String Data를 `exampleData` 로 가정하고, 
`<div>`태그 내에 innerHTML을 사용하기 위해 함수 예시를 들었다.

일반적으로 React 내에서 innerHTML을 사용하는 방법인데, 여기서 `XSS`를 방지하기 위해 `Sanitizer`를 사용한다.

```javascript
  ...
  import dompurify from 'dompurify';
  
  const exampleData : string = '<span>text</span>';
  
  const sanitizer = dompurify.sanitize;
  
  const exampleFunction = (text : string) => {
    return <div dangerouslySetInnerHTML={{__html: sanitizer(exampleData)}} />
  };
```

`dompurify` 에서 제공하는 `sanitize`함수 는 String 타입의 데이터를 입력받아, 전처리 후 String을 내뱉는다.

`dangerouslySetInnerHTML`에 전달할 String Data를 `sanitize` 함수를 거쳐 입력한다.

이러한 텍스트 전처리기를 이용하면 DOM 접근 방식의 `XSS` 방지에 효과적이다.
<br><br>

> ## Review

React, TypeScript와 더불어 `eslint` 를 사용할 때 

개발 상의 편의를 위해 `Strict Mode` 를 해제하거나 `warning` 수준의 메시지는 무시하는 경우가 많은데, 
메시지를 잘 뜯어보면 개발하면서 도움이 되는 내용들이 상당히 많다.

일반적인 프론트엔드 개발자들과의 차별점을 둘 수 있는 좋은 내용이다.
