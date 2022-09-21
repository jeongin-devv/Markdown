<div align="right">> Created : 2022.09.04</div>

> ## Overview

- 회사의 내부에서 이메일 발송 템플릿을 제공하는 서비스 개발을 맡게 되었다.
<br>

- 프론트엔드나 퍼블리싱을 담당하는 사람이라면 누구나 한번쯤은 거쳐간다는<br>
말은 들었지만, 나는 이제서야 해보게 되었는데, 생각보다 장애물이 많았다.

- Email Template은 언뜻 보면 단순한 HTML Template지만, 
<br>일반적인 HTML 양식과는 조금은 다른 양상을 보이기에 이렇게 기록한다.
<br><br>

> ## Pre-Comumnication
```
기존에는 외주 업체에 의뢰했었기에 가이드 라인이 없었다. 
따라서 업무를 진행하기 전에 협업하는 팀과 이메일 템플릿에 대한 정보를 공유하는 시간을 가졌다.
```
1. **일반적인 웹 페이지와 달라서, 웹페이지와 완벽하게 같이 개발하기 어렵다.**
2. **타 서비스의 이메일 예시가 있으면 개발이 조금 더 수월하다.**
3. **메일에는 Background-image 를 사용할 수 없습니다.**
4. **이메일 템플릿의 권장 가로 크기는 600 ~ 800px 입니다.**
5. **용량에 주의하여야 합니다. (템플릿 권장 용량 : 250kb 미만)**
<br><br>

```
위 고려사항의 배경은 이메일 클라이언트에서 시작된다.

이메일은 다양한 클라이언트에서 제공되고 있는데, 같은 서식을 발송해도,
클라이언트에 따라 다르게 화면에 렌더링 된다.

<HEAD> 를 통째로 삭제해서 meta tag를 지원하지 않기도 하고,
<style> 태그를 지원 하지 않아, 클래스 css 가 적용이 안되기도 한다.

최소한 위의 다섯가지 항목은 고려해야, 다양한 이메일 클라이언트에서도
비슷한 템플릿의 이메일을 제공 할 수 있다.
```

> ## Considerations
```
개발 시 고려했던 사항들을 정리했습니다.
```

### 1. Doctype
```
Doctype 은 이메일 클라이언트에게 HTML 유형을 알려주고 W3C Validator 같은 도구를 사용하여 HTML 품질 검사를 할 수 있다.

XHTML 1.0 Transitional doctype을 사용하면 이메일 클라이언트에서 신뢰할 수 있는 방식으로 유효성을 검사하고 이메일 렌더링에 도움이 된다.

일부 이메일 클라이언트는 제공하는 Doctype을 자신의 Doctype으로 대체하기 때문에 적용되지 않을 수 있다.
```

### 2. Container 구성 시, table 태그 이용
```
이메일의 구조를 정상적으로 제공하려면 <div>를 사용하지 않고 <table>로 작성해야 합니다.

일반적으로 ‘TABLE 코딩’이라 불리는 이 방법은 중첩된 테이블을 많이 사용하기 때문에 TABLE 구조의 마크업이 완료된 후 스타일을 입히는 것이 좋습니다.

수정이 까다롭기 때문에 레이아웃이 확정된 후 작업하는 것이 좋습니다.

<thead>, <tbody>, <colgroup>과 같은 <table>과 관련된 다른 태그들을 피하는 것이 좋습니다.

가장 가볍고 안전한 방법은 <table>, <tr>, <td> 이 3개의 태그만 활용하는 것입니다.
```

### 3. HTML 속성 및 인라인 스타일
```
일부 이메일 클라이언트는 <head>를 제거하거나 <style>를 제대로 지원하지 않습니다.

따라서 HTML 속성으로 테이블을 구조화하는 것이 좋습니다.

인라인 스타일이란 <td style="color: #ff0000;">과 같이 HTML 속성으로 스타일을 작성하는 것을 말합니다.
이를 사용하면 <style>를 제대로 지원하지 않는 경우 유용하며 추천하는 방법입니다.

편의성을 위해 일부 스타일은 <style>로 작성해 포함하거나 나중에 인라인 작성으로 옮길 수 있습니다.


만약 NPM을 사용할 수 있는 환경이라면 <link>로 연결된 CSS 파일이나 <style>로 더 쉽게 작성하고, inline-email 같은 라이브러리를 통해 추후 간단하게 인라인 방식으로 병합할 수 있습니다.
```

### 4. 색상
```
호환성을 위해 #ffffff처럼 작성하는 Hexadecimal Colors를 사용합니다.
RGB, RGBA, HSV 같은 색상은 일부 이메일 클라이언트에서 지원하지 않습니다.

#fff와 같은 축약형은 사용하지 않도록 주의합니다.

CSS background 속성보다는 HTML bgcolor 속성을 이용하세요.
```

### 5. 단일 클래스 및 CSS 단축 속성 사용금지 
```css
class 속성의 값을 다중으로 작성하지 마세요.하나의 단일 값으로 작성해야 합니다.

CSS 단축 속성의 경우, 호환이 되지 않는 경우가 많습니다. 개별적으로 사용해야 합니다.

// 단축 속성 : 지원하지 않는 케이스가 많음
td {
  font: 16px / 1.4 Arial, sans-serif;
}
// 개별 속성 
td {
  font-size: 16px;
  line-height: 1.4;
  font-family: Arial, sans-serif;
}
```


### 6. 이미지
```
HTML 이메일에 이미지를 사용할 수 있지만 몇 가지 주의사항이 있습니다.

 - 절대경로를 사용

 - 용량은 250kb 미만으로 유지

 - 가로/세로 너비(width, height)를 입력

 - 대체 텍스트(alt)를 입력

이미지를 제거하는 일부 이메일 클라이언트를 위해 width, height, alt 속성을 꼭 입력하세요.

이미지 버튼으로 사용하는 경우, 문제가 생길 수 있으므로, 사용을 지양합니다.
```

### 7. 여백
```css
CSS의 margin은 사용할 수 없습니다.
대신 padding과 셀의 너비로 여백을 생성할 수 있습니다.

padding을 사용할 경우 top, bottom, left, right 값을 모두 작성해야 합니다.

<td style="padding-top: 0; padding-right: 0; padding-bottom: 30px; padding-left: 0;"></td>
```

### 8. 조건부 주석(Conditional Comments)
mso(Microsoft Outlook) 키워드를 조건부 주석에 사용할 수 있습니다.
```css
<td>
  <!--[if mso]>
    OUTLOOK CONTENTS
  <![endif]-->
  <!--[if !mso]>
    NON-OUTLOOK CONTENTS
  <![endif]-->
  <!--[if (gte mso 9)|(IE)]>
    GREATER THAN EQUAL OUTLOOK 9 or INTERNET EXPLORER
  <![endif]-->
</td>
```

> ## Responsive Layout & Dark Mode
```
반응형 레이아웃과 다크 모드 지원에 고려해야 할 사항입니다.
```

1. 지원 사항<br>
이메일 클라이언트에 따른 지원 사항들이 다릅니다.
Media-Query, meta-tag, dark mode 사양이 모두 다르므로, 고려할 범위를 정해야 합니다.<br>
[Dark Mode Email: Your Ultimate How-to Guide - Litmus ](https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers/#)

2. 대안<br>
반응형 레이아웃을 위한 Media Query 의 대안 <br>
  width를 % 단위로 작성한다.<br>
  max-width, min-width 등의 제한 요소로 미디어쿼리를 대신한다. <br>
  table 의 크기를 %. 단위로 조절한다.<br><br> 
    다크 모드는 Media Query를 지원하지 않는 경우, 대응하기 어렵습니다.<br>
    대표적인 예로 Gmail의 경우, style 태그도 지원하지않고, Media Query를 지원하지 않습니다.

    대신 클라이언트 내부에서 어두운 색상과 밝은 색상을 색반전 시켜 보여 줍니다.<br><br>
    색상이 변해야 하는 부분은 모노 톤의 템플릿을 채용하는 경우가 많으며
    이미지의 경우, 다크모드와 일반 모드가 호환되도록 디자인 하기도 합니다.<br><br>


> ### Reference
  [HTML Email Template 만들기 - heropy](https://heropy.blog/2018/12/30/html-email-template/)