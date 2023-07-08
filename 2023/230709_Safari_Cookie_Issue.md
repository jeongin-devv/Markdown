<div align="right">Created : 2023.07.09</div>

## **Safari Cookie Issue**
<br>

`Mobx`나 `Context API`와 같은 상태관리 라이브러리나 <br>
`Local Storage`, `Session Storage`, `IndexedDB`와 같은 저장소 말고 <br>
`Next.js` 에서 데이터를 보관하고 관리할 수 있을까? 하는 고민이 있었다. <br>

Response Data 를 클라이언트 사이드에서 직접적으로 노출시키고 싶지 않았고, <br>
어떤 방법이 있을까 고민하던 와중, `Severless API`와 `iron-session`을 <br>
이용해서 Response 를 선택적으로 보여줄 계획을 짜게 되었다. <br>

실제로 구현했고, 크로스 브라우징 자체 테스트 중에 <br>
`Safari` 에서 `iron-session` 을 이용해서 저장한 데이터를 불러오지 못하는 이슈를 발견했다. <br><br>

## **Why?**
<br>

왜 이런 문제가 일어났는가? 에 대해 소스와 로그를 뒤져보던 와중, <br>
`Cookie` 에서 원인을 발견 할 수 있었다.<br>

`iron-session` 은 브라우저에 키값과 32자리의 비밀번호를 이용해 암호화한 토큰을 <br>
`Cookie`로 전달하는 방식으로 클라이언트 사이드에 세션을 유지하고 있다. <br>

이때 `Cookie` 에 대한 Options 를 지정해 줄수 있는데, <br>
여기서 `Secure`의 값에 따라, `Safari` 에서 동작하지 않는 것을 확인했다. <br>

찾아보니, `Secure Cookie`는  HTTPS 환경에서만 저장되는데 <br>
브라우저들은 대체로 `localhost` 에서는 `Secure` 값에 상관없이 `Cookie`를 저장 한다. <br>
하지만 `Safari` 에서는 `Secure Cookie`를 `localhost`에서 저장하지 않는다.<br>

## **How**
<br>

`localhost` 와 배포 되어있는 서비스 환경에 따라 Secure 값을 다르게 줌으로서, <br>
개발 단계에서의 크로스 브라우징 테스트에서 같은 쿠키값을 받아올 수 있게 조치했다. <br>

하나의 패키지에 클라이언트와 서버가 존재 하는 서비스에서는 이러한 문제에 부딫힌 적이 없는데, <br>
클라이언트 사이드에서 많은 것을 처리하게 되면서 경험하게 되는 것들이 웹 서비스에 대한 이해에 <br>
많은 도움이 되고 있다. <br>

이렇게 하나씩 하나씩 또 알아가게 되면, 언젠가 이 경험을 활용할 기회가 오겠지.
