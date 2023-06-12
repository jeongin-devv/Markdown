<div align="right">Created : 2023.06.12</div>

## **First Half Memoir**

2023년 전반기는 그 어느때보다 바쁘게 보냈다.<br>
잊어버리지않게 전반기 회고록을 간단하게 작성하려 한다.<br><br><br>

### 1. BackOffice & Storybook 

&ensp; 주력 서비스가 앱인 지금의 회사에서 Frontend 팀은 <br>
&ensp; 몇몇 경우를 제외하면 대부분 BackOffice Service 를 개발하고 있다. <br>

&ensp; 점점 앱의 크기가 커지고, 기능이 다양화가 되면서 <br>
&ensp; BackOffice 의 크기도 함께 늘어나고 있는 상황이다. <br>

&ensp; 우리 팀은 Micro Service Architecture 를 표방하고 있기에, <br>
&ensp; 앱의 주요 서비스 기능 단위로 콘솔을 나누어 개발을 하고 있다. <br>

&ensp; BackOffice Service 를 개발할 때 가장 중요한 것은 <br>
&ensp; 서비스에 대한 이해도라고 생각한다. <br>

&ensp; **어떠한 서비스를** <br>
&ensp; **어떻게 컨트롤하고** <br>
&ensp; **어떻게 보여지는지** <br>

&ensp; 관리자 페이지에서의 내용이 <br> 
&ensp; 실제 사용자에겐 어떻게 제공되고, <br> 
&ensp; 어떠한 데이터를 수집하여 우리가 활용할 수 있는가 <br>

&ensp; 이러한 이해도가 부족할 경우, <br>
&ensp; 아무리 간단한 기능일 지라도 어딘가 부족한 관리자 콘솔이 만들어 지게 되더라. <br>

&ensp; 서비스에 대한 이해의 중요성을 조금씩 체감할 때 쯤, <br>
&ensp; 효율적인 퍼블리싱 작업에 대한 필요성도 조금씩 수면 위로 떠올랐다. <br>
    
&ensp; 우리 팀은 같은 테마의 관리자 페이지를 별도의 코드 공통화 없이 작업하고 있는데, <br>
&ensp; 이러한 개발이 가능한 이유가 몇가지 있다.<br>

- 콘솔을 나누는 조각의 크기가 아주 작다.
- 한 개의 콘솔을 복수의 작업자가 작업하지 않는다. 
- 팀원들이 스마트하고 경력이 다양하기에 유지 보수에 큰 어려움이 없다.

&ensp; 안타깝게도 나는 세번째 사항에 해당되지 않아, <br> 
&ensp; 처음 입사하고 만든 콘솔을 재작업하는데 무척 애를 먹게 되었다. <br>

&ensp; 한번 어려움을 겪고 나니 Code Quality, Design Pattern 에 대해 <br>
&ensp; 중요성을 느끼게 되었고, 이에 따라 가장 보편화되어있는 도구인 Storybook 을 사용하게 되었다. <br>

&ensp; Storybook 은 사용하기 크게 어려움이 없는 라이브러리다. <br>

&ensp; JavaScript 를 사용할 줄 알고, Component 와 Properties 에 대한 이해만 있다면 <br>
&ensp; 누구나 쉽게 작성 할 수 있고, Storybook 은 이를 시각화 해준다.

&ensp; Storybook 은 어떻게 보면, 제한된 기능을 제공하는 라이브러리지만 <br>
&ensp; 개발자의 입장에서 코드에 대해 다시 생각하게되고, <br>
&ensp; 서비스 차원에서의 Design Guide Line 수립에 대한 방향성을 어느정도 제시해준다. <br>

&ensp; Storybook 을 당분간은 유지보수 하면서, 코드 품질과 생산성에 대해 꾸준히 피드백 하고자 한다. <br>
&ensp; 나중에는 Storybook 보다 더 나은 Design Guide 를 만들기 위해. <br><br>

### 2. User Service & Next.js

&ensp; 지난 1년에 가까운 시간동안 위에 서술 했다시피, <br> 
&ensp; 나는 주로 BackOffice 를 개발하고 있었다. <br>

&ensp; 그러한 와중에 일반 사용자들이 직접 사용하는 공식 홈페이지의 <br> 
&ensp; 추가 기능을 담당하게 되었다. <br>

&ensp; Search Engine Optimization 을 위해 Next.js 를 사용하게 되었는데, <br>
&ensp; SEO 뿐만 아니라, 정말 여러가지 기능을 제공하고 있어서 <br>
&ensp; 라이브러리와 프레임워크의 차이에 대해 다시 한번 더 체감을 하게 되었다.<br>

&ensp; 이전 회사에서 Vue.js 를 사용할 때는 이것저것 조각모음 하느라 정신 없었는데 <br>
&ensp; 이번에는 더 나은 성능과 유지보수 용이성을 갖추는데 집중 하고자 한다. <br><br>

### 3. 그리고 결혼

&ensp; 그리고 올해 5월에 결혼식을 올렸다. 지금의 나를 만들어준 소중한 배우자와 함께. <br>
&ensp; 내가 더 공부하고, 열심히 일할 수 있게 응원해주는 덕분에 나는 더 나은 사람이 되어야 할 이유가 추가 되었다. <br><br>

### **앞으로...**

&ensp; 5월 내내 브라우저 내에서의 API 테스트를 진행하고, 기능 프로세스를 정리해놓은 덕분에 <br>
&ensp; 6월은  Storybook 을 활용한 퍼블리싱에 집중하면서 Next.js 에 대한 학습을 틈틈히 진행 할 예정이다. <br><br>

&ensp; 나태해지지 않고, 언제나 간절하게 <br><br>
