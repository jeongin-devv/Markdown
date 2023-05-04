<div align="right">Created : 2023.05.04</div>

## **React-Cookie**
<br>

내가 만든 쿠키... 너를 위해 구웠지...<br><br>
기존 사내 서비스에서는 브라우저 데이터를 관리하기 위해 <br>
`Mobx`, `Web Storage`, `IndexedDB`를 용도에 맞게 사용하고 있었다. <br><br>
`Web Storage`를 이용한 기능들을 `Cookie`를 활용하여 마이그레이션 하게 되었는데,<br>
이에 대한 이유를 간단하게 정리한다.<br><br>

### **Why ?**
<br>

기능을 마이그레이션 하게 된 이유는 아래와 같다.
<br><br>

1. 관리해야하는 데이터가 많아짐에 따라 체계적인 구조로 저장/관리 해야한다고 판단
2. `IndexedDB`보다 조금 더 자유로운 형태로 사용할 수 있음
3. 비슷한 기능들을 결합하고, 추후 Service Integrate 를 대비한 모듈화
4. 많은 예제와 다큐먼트를 참조할 수 있음
5. 간단하고, 민감하지 않은 정보들은 `Web Storage`로 사용

<br>

서비스의 갯수가 점점 늘어나고 복잡해지면서 방대해진 `Web Storage`로 만든 기능들을 <br>
`Cookie`를 이용해서 조금더 체계적으로 정리하여 사용하는 것을 궁극적인 목표로 삼았다.<br><br>

### **react-cookie?**
<br>

npm 에는 쿠키에 쉽게 접근하기위한 여러가지 라이브러리가 있지만 <br>
우리 팀은 `react-cookie` 를 사용하기로 했다.<br><br>
거창한 이유는 없고, 팀에서 관리하는 서비스들이 <br>
`React(CRA)` 와 `Next.js` 로 이루어져 있기 때문<br><br>
<br><br>

### **Result**
<br>

코드를 마이그레이션 하고난 후, 당장은 기능 상으로는 크게 달라진 점은 없다.<br>
그저 `Web Storage` 에서 관리하던 데이터들을 `Cookie` 로 옮겼을 뿐.<br><br>

대신 코드 가독성은 높아졌고, `TypeScript`로 조금 더 Static 하게<br>
Data Type 을 관리하게 되었고, 비슷한 프레임에서 데이터를 관리하니까 <br>
추후 유지 보수에 편리하게 되었다는 생각이 있다.<br><br>

그리고, XSS 공격에 조금 더 안전하다.. 라는 이론적인 장점이 있다.<br>
이미 CSRF 대비는 별도의 토큰과 Referer 에 대한 검증을 따로 취하고 있기 때문에<br>
보안에는 조금 더 좋아지지 않았나.. 하는 생각도 있다.
<br><br>

### **Reference**

https://www.npmjs.com/package/react-cookie
