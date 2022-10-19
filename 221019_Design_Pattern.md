<div align="right">Created : 2022.10.19</div>

> ## Overview

예전에는 서비스를 구성할 때 대부분 이미 짜여진 프레임워크의 구조에 맞춰서 구성하거나,
타 플랫폼의 아키텍쳐를 보고 어느 정도 답습하는 식으로 구성했었다. 아는게 많지도 않았고, 생각할 겨를 없이 코드짜기에 바빴으니까.
<br><br>
하지만 프론트엔드가 주 직무가 되면서 디렉토리 구조나 디자인 패턴에 대한 고민이 생겼다.
<br>
각 프레임워크마다 지향하는 점이 다르고, 변화의 속도가 빠르다 보니 기준점을 삼을 만한 자료가 없었다.
<br><br>
막연하게 객체 지향 프로그래밍, 함수형 프로그래밍 등과 같은 이론적인 부분을 공부하다보니 
더 막연하게 느껴지고 조금은 지쳐갈 무렵에 괜찮은 글을 발견했다.
<br><br>
2021년에 작성된 글이지만, 내가 리액트를 사용하면서 마주하게된 고민들을 어느정도 해결해줬다.
<br><br>
추후 다시 보기 위해 정리도 할 겸, 번역하고 요약 한다.
<br>
글이 길어서 아마 여러번 커밋 할 것 같다.
<br><br>

> ## 5 Advanced React Patterns
<br>
많은 리액트 개발자들은 아래의 예시를 생각해보았을 것이다.

- 다양한 케이스에 적용 할 수 있도록 __재사용 가능한__ 컴포넌트
- __사용하기 쉬운__ 간단한 API를 가진 컴포넌트
- UI 나 기능적인 측면에서 __확장성이 넓은__ 컴포넌트

위의 고민들이 많은 사람들에게 반복되면서, React 커뮤니티에서 몇가지의 `Advanced Patterns` 가 등장하게 되었다.
<br>
그 중에서 다섯 가지의 패턴을 아래의 구조로 설명한다.

a. 패턴 소개<br>
b. 예시 코드 (간단한 `Counter` 구현)<br>
c. 장점과 단점<br>
d. 해당 패턴을 사용하는 라이브러리 예시
<br><br>

## 1. Compound Components Pattern

이 패턴을 사용하면 불필요한 `Prop Drilling` 없이 `Expressive`하고 `Declarative`한 컴포넌트를 만들 수 있다. 커스터 마이징이 용이하고 관심을 분리하여 이해가 쉬운 API를 갖춘 컴포넌트를 원한다면 이 패턴을 사용 할 수 있다.

### (1) Example
```javascript
import React from "react";
import { Counter } from "./Counter";

function Usage() {
  const handleChangeCounter = (count) => {
    console.log("count", count);
  };

  return (
    <Counter onChange={handleChangeCounter}>
      <Counter.Decrement icon="minus" />
      <Counter.Label>Counter</Counter.Label>
      <Counter.Count max={10} />
      <Counter.Increment icon="plus" />
    </Counter>
  );
}

export { Usage };
```
### (2) 장점

 - 복잡성 감소 <br>하나의 부모 컴포넌트에 모든 `Props`를 집어넣고 하위 UI 컴포넌트로 향해 내려가는 것이 아닌, 각 `Prop`는 **가장 적합한 Sub Component**에 연결되어 있다.

```javascript
// Bad Case
return (
  <Counter
    label="label"
    max={10}
    iconDecrement="minus"
    iconIncrement="plus"
    onChange={handleChangeCounter}
  />
);

// Better Case
return (
  <Counter onChange={handleChangeCounter}>
    <Counter.Decrement icon={"minus"} />
    <Counter.Label>Counter</Counter.Label>
    <Counter.Count max={10} />
    <Counter.Increment icon={"plus"} />
  </Counter>
);

```

- 유연한 구조<br>
컴포넌트의 UI가 **높은 유연성**을 가지고 있고, **하나의 컴포넌트로부터 다양한 케이스를 생성**할 수 있다. 예를 들어, 사용자는 Sub Component의 순서를 변경하거나 이 중에서 무엇을 나타낼 지 정할 수 있다.

- 관심사의 분리<br>
대부분의 로직은 기본 Counter 컴포넌트에 포함되며, `React.Context`는 모든 자식 컴포넌트의 `state`와 `handler`를 공유하는 데 사용된다. 이를 통해 책임을 명확히 분리할 수 있다.

### (3) 단점

- 과도한 UI 유연성<br> 
유연성이 높다는 것은 **예기치 않은 동작을 유발할 가능성이 크다는 것**을 의미한다. 예를 들어, 불필요한 자식 컴포넌트가 존재하거나, 필요한 자식 컴포넌트가 없을 수도 있고, 자식 컴포넌트의 순서가 잘못되어 있을 수 있다. <br>또한, 개발자는 사용자가 컴포넌트를 어떻게 사용하기를 원하는지에 따라, 유연성에 어느 정도 제한을 두고 싶을수도 있다.

- JSX의 비대화<br>
 **패턴을 적용하면 코드의 행 수가 증가한다.** 특히 `EsLint`나 `Prettier`와 같은 코드 포맷터를 사용하는 경우 더욱 심각해진다. 단일 컴포넌트에서는 큰 문제가 없지만, 규모가 커질수록 그 차이가 확연하게 드러난다.

 ### (4) 이 패턴을 사용하는 라이브러리
 
- [React BootStrap](https://react-bootstrap.github.io/components/dropdowns/) 
- [Reach UI](https://reach.tech/accordion/)
