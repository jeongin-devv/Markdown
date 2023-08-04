<div align="right">Created : 2023.08.04</div>

# **Next.js Serverless API**

최근 메인 서비스의 Account 쪽 기능을 설계하고 구현하느라 정신이 없었다. <br>

써보지 않은 기술 스택으로 구현하다보니, 여러가지 고민을 많이 하게 되었는데, <br>
`Next.js` 를 사용하면서 고민한 문제들에 대해 정리하고자 한다. <br><br>

이번 글은 `Nextjs Serverless API`에 대한 내용이다. <br><br>

## **첫번째. &nbsp;&nbsp; Secure**

우리 회사의 Production API 는 Mobile Application 을 기반으로 만들어져 있어, <br>
Web Service 에서 사용하기엔 몇가지 취약점이 있다.<br>

취약점의 문제가 그렇게 크지 않고, 서버 팀의 업무 리소스를 줄이기 위해서<br>
이를 Next.js 의 Server Side 에서 보완하고 관리하기로 했다. <br>

`CORS`, `Rate Limiting` 등의 API 접근 관리와 <br>
`iron-session`, `next-auth` 등의 데이터 암호화를 <br> 
우리 팀에서 `Serverless API` 애 적용하여 일종의 미들웨어처럼 사용했는데 <br>
Production API 의 부족한 부분을 보완하고, 개선하게 되었다. <br><br>

## **두번째. &nbsp;&nbsp; Server Side Communication**

팀에서 요구한 사항은 Client Side 에서 Request, Response Parameter 를 <br>
최대한 노출 시키지 않는 것이였다. 이를테면 Token 이나 개인 정보와 같은 민감한 내용들. <br>

이를 Server Side 에서 관리하고 사용하면서, 정보의 노출을 최소화 하려고 노력했다. <br>
로그인 관련 정보는 `next-auth` 의 Server Side Session 에서 관리하고, <br>
기타 페이지에서 관리하는 정보들은 `iron-session` 의 Server Side Session 에서 관리하고 있다. <br>

Production API의 Reqest, Response 값 들중 원하는 값들을 <br>
Client Side 에 노출시키지 않고, Server Side 내에서 사용하면서, 정보 노출을 최소화 했다. <br><br>

## **세번째. &nbsp;&nbsp; Error Control**

개발이 어느정도 진행되고나면 QA 팀에서 검증을 거치게 되는데, <br>
이때 가장 껄끄러운 것은 QA 팀에서 Client 상의 문제인지, Server 상의 문제인지 <br>
구분이 어려울 때가 있다. <br>

이를 조금 더 편하게 관리하고자, Production API 에서 응답하는 에러를 판단하여 <br>
`Serverless API` 에서 한번 정제하여 클라이언트에 에러를 전달하게 구현했다. <br>

프론트엔드와 백엔드가 구분되어 있고, QA 팀도 따로 존재하는 개발그룹의 특성 상 <br>
에러에 대한 책임여부가 나뉘어야하는데 이를 도입하면서 확실히 디버깅도 용이해졌다. <br><br>

## **네번째. Reduce Server Dependence**

개발 그룹 내에서 Client 와 Server 담당 팀이 확실히 나뉘어져있다보니 <br>
자연스레 Client 담당 팀에서는 Server 담당 팀에 의존도가 높다. <br>

정말 중요하거나 민감한 데이터의 경우, 당연히 Server 팀에서 맡는게 맞지만 <br>
사소하거나, 회사 내부에서만 쓰는 가벼운 데이터도 Server 팀을 거치다 보니 <br>
Server 팀의 리소스는 안그래도 부족한데, 일이 늘어나서 병목 현상이 생기게 됬다. <br>

이를 조금이라도 완화하고자, 우리 팀에서 작은 부분의 Server Side 를 담당하면서 <br>
우리 팀의 Server 쪽 이해도와 업무 진행 속도가 증대됬다.<br><br>

## **마치며**

오랜만에 Server Side 쪽 작업을 진행하게되면서 가장 힘들었던 것은 <br>
작업 방향에 대해 생각하는 마인드의 차이 였다. <br>

한동안 Client Side 쪽만 개발을 했다보니 자연스럽게 Client 위주로 생각했고, <br>
생각해보면 부딫혔던 고민들은 Server Side 의 기본적인 내용이였고, <br>
이전에 대부분 해본 작업 임에도 불구하고 번뜩번뜩 생각나지 않고 시간이 조금 걸렸다.<br>

Server Side 도 같이 개발을 하다보니 좀더 자유도도 높아졌고 <br>
구현할 수 있는 범위가 넓어져서, 좀더 괜찮은 서비스가 구현된 것이 아닌가 생각한다. <br>

다음 글은 Next.js 의 Server Side 에서 사용한 라이브러리들에 대해 정리할 예정이다.<br>

물론 지금 하고 있는 일에 지장이 없는 선에서 시간이 나면.<br><br>
