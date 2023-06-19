<div align="right">Created : 2023.06.19</div>

## **Next Auth.js**
<br>

`Search Engine Optimization` 을 위해 <br>
우리 팀에서는 필요한 경우, `Next.js`를 사용한다. <br>

이번에 내가 맡은 공식 홈페이지의 Account 관련 기능 중에<br>
로그인, 회원가입을 구현하기 위해 기술 검토를 하게 되었다.<br>

특히 `OAuth 2.0 기반의 소셜 로그인`을 <br> 
프론트 엔드에서 어떻게 구현할 것 인가 에 대해 고민 하면서 <br>
API 테스트가 끝나갈 무렵에 `NextAuth.js` 를 접하게 되었다. <br>

이에 대해 가볍게 정리하고자 한다. <br><br>

### **NextAuth.js?**
<br>

`NextAuth` 는 여러가지의 소셜 로그인을 React 기반의 `Next.js` 에서 <br>
간편하게 사용할 수 있게, `JSX 형태의 컴포넌트`로 제공하는 라이브러리 이다. <br>

Google 이나 Apple 에서 OAuth 2.0 를 변경하거나 버전이 바뀌지 않는 이상 <br>
굳이 구성 되어 있는 걸 건드릴 필요도 없다.<br>

대부분의 메이저 서비스는 큰 변경 사항이 있을때, <br>
구버전과 병렬로 제공하거나 마이그레이션을 진행할 유예기간을 주기 때문에 <br>
유지 보수에 대해 큰 이슈는 아직까지는 없는 것으로 보인다.<br>

추후, `Auth.js` 로 여러 라이브러리에서 사용할 수 있게 통합 된다고 하니, <br>
지금 기록해두면 나중에 또 새로 구성할 날이 오지 않을까 하는 생각이 있다. <br><br>

### **Getting Started**
<br>

아래 문서는 4.22.1 버전 기준으로 작성 되었습니다. <br><br>

**1. 먼저 npm 에서 next-auth 를 설치한다.**
<br>

```javascript
npm install next-auth
```
<br>

**2. 프로젝트에 NextAuth 를 추가해준다.**
<br>

NextAuth.js 구성 요소를 포함하는 `[...nextauth].js` 파일을 추가한다. <br>
스프레드 연산자를 보면 알수 있듯이, 동적 경로 처리를 포함하게 된다. <br>

pages/api/auth 에 아래의 내용을 가진 파일을 작성한다.<br><br>

```javascript 
pages/api/auth/[...nextauth].js
--------------------------------
import NextAuth from "next-auth";
import GithubProvider from "next-auth/providers/github";

export const authOptions = {
  // 소셜 인증 Provider 를 정의
  providers: [
    GithubProvider({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
  ],
};

export default NextAuth(authOptions);
```

소셜에 대한 정보를 Provider 에 작성하는데, <br>
기본적으로 clientId, clientSecret 을 기재하고, <br>
추가로 필요한 옵션은 별도로 작성한다. <br>

`clientId`, `clientSecret` 은 민감 정보이므로 <br>
환경 변수 파일이나 서버 사이드에서 관리하는 것을 권장한다.<br><br>

**3. Next.js App 에 적용 시킨다.**
<br>

소셜 정보를 전역에서 사용하기 위해, <br>
앱의 최상단에 Session Context 를 제공해야 한다.<br><br>

```javascript
import { SessionProvider } from "next-auth/react"

export default function App({
  Component,
  pageProps: { session, ...pageProps },
}) {
  return (
    <SessionProvider session={session}>
      <Component {...pageProps} />
    </SessionProvider>
  )
}
```
<br>

**4. React Hook 을 이용한 확인**
<br>

위의 인스턴스에 클라이언트 사이드에서 `useSession` Hook 으로 접근 가능하다. <br>
서버 사이드에서도 접근이 가능하나, 이 문서에는 별도로 서술하지 않는다.<br><br>

```javascript
import { useSession, signIn, signOut } from "next-auth/react"

export default function Component() {
  const { data: session } = useSession()
  if (session) {
    return (
      <>
        Signed in as {session.user.email} <br />
        <button onClick={() => signOut()}>Sign out</button>
      </>
    )
  }
  return (
    <>
      Not signed in <br />
      <button onClick={() => signIn()}>Sign in</button>
    </>
  )
}
```
<br>

**5. 확장성**
<br>

단순히 소셜 계정을 로그인시키는 것으로 끝나면 좋겠지만 그렇지 않다. <br><br>

원하는 기능을 위해서는 별도의 프로세스가 필요한데, <br>
여기서는 클라이언트 사이드에서 세션과 jwt 의 정보를 받아오는 예시를 든다. <br>

```javascript
pages/api/auth/[...nextauth].js
-----------------------------------
...
callbacks: {
  async jwt({ token, account }) {
    // 로그인 이후 토큰에 Access Token 을 유지 시킨다.
    if (account) {
      token.accessToken = account.access_token
    }
    return token
  },
  async session({ session, token, user }) {
    // Access Token 을 클라이언트 사이드에서 사용할 수 있게 전달한다.
    session.accessToken = token.accessToken
    return session
  }
}
...
```
<br>

**6. Callback URL**
<br>

OAuth 2.0 을 제공하는 서비스에서 인증 이후 Callback URL 을 넣어줘야한다.<br>


<br>

### **끝으로**
<br>

NextAuth 를 접했을 때는 이미 각 소셜 (Google, Apple) 에서 <br>
공식 도큐먼트를 참고하여 이미 테스트가 끝난 후 였다.<br>

그래서 그런지, NextAuth 의 작동 방식이나 사용법에 대해 큰 어려움이 없었고,<br>
다시 한번 클라이언트 사이드에서 로그인 프로세스 구현에 대해 생각하게 된 계기가 되었다.
<br><br>