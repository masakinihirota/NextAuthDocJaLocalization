Client API | NextAuth.js
https://next-auth.js.org/getting-started/client



# Client API

# クライアントAPI



The NextAuth.js client library makes it easy to interact with sessions from React applications.

NextAuth.jsのクライアントライブラリを使うと、Reactアプリケーションからセッションを簡単に操作することができます。



#### Example Session Object[#](#example-session-object "Direct link to heading")

#### セッションオブジェクトの例[#](#example-session-object "Direct link to heading")

```
{
  user: {
    name: string,
    email: string,
    image: uri
  },
  accessToken: string,
  expires: "YYYY-MM-DDTHH:mm:ss.SSSZ"
}
```

##### tip



The session data returned to the client does not contain sensitive information such as the Session Token or OAuth tokens. It contains a minimal payload that includes enough data needed to display information on a page about the user who is signed in for presentation purposes (e.g name, email, image).



クライアントに返されるセッションデータには、セッショントークンやOAuthトークンなどの機密情報は含まれていません。プレゼンテーションの目的で、サインインしているユーザーの情報をページに表示するのに必要なデータ（名前、メール、画像など）を含む、最小限のペイロードを含んでいます。



You can use the [session callback](https://next-auth.js.org/configuration/callbacks#session-callback) to customize the session object returned to the client if you need to return additional data in the session object.



セッションオブジェクトの中に追加のデータを返す必要がある場合は、[セッションコールバック](https://next-auth.js.org/configuration/callbacks#session-callback)を使って、クライアントに返すセッションオブジェクトをカスタマイズすることができます。



___



## useSession()[#](#usesession "Direct link to heading")


## useSession()[#](#usesession "Direct link to heading")



-   Client Side: **Yes**
-   Server Side: No


- クライアント側で **はい**。
- サーバーサイド いいえ



The `useSession()` React Hook in the NextAuth.js client is the easiest way to check if someone is signed in.


NextAuth.jsクライアントの`useSession()` React Hookは、誰かがサインインしているかどうかを確認する最も簡単な方法です。


It works best when the [`<Provider>`](#provider) is added to `pages/_app.js`.


これは、[`<Provider>`](#provider)が `pages/_app.js` に追加されている場合に最適です。



#### Example[#](#example "Direct link to heading")

```
import { useSession } from "next-auth/client"

export default function Component() {
  const [session, loading] = useSession()

  if (session) {
    return <p>Signed in as {session.user.email}</p>
  }

  return <a href="/api/auth/signin">Sign in</a>
}
```



___



## getSession()[#](#getsession "Direct link to heading")



-   Client Side: **Yes**
-   Server Side: **Yes**

- クライアント側 **はい**。
- サーバーサイドの場合 **はい**



NextAuth.js provides a `getSession()` method which can be called client or server side to return a session.


NextAuth.jsでは、クライアントサイドまたはサーバーサイドで呼び出すことができる、セッションを返すための`getSession()`メソッドを提供しています。



It calls `/api/auth/session` and returns a promise with a session object, or null if no session exists.



このメソッドは `/api/auth/session` を呼び出し、セッションオブジェクトを含むプロミスを返し、セッションが存在しない場合は null を返します。



#### Client Side Example[#](#client-side-example "Direct link to heading")

```
async function myFunction() {
  const session = await getSession()
  /* ... */
}
```



#### Server Side Example[#](#server-side-example "Direct link to heading")

```
import { getSession } from "next-auth/client"

export default async (req, res) => {
  const session = await getSession({ req })
  /* ... */
  res.end()
}
```



##### note



When calling `getSession()` server side, you need to pass `{req}` or `context` object.



サーバーサイドで `getSession()` を呼び出す際には、`{req}` または `context` オブジェクトを渡す必要があります。


The tutorial [securing pages and API routes](https://next-auth.js.org/tutorials/securing-pages-and-api-routes) shows how to use `getSession()` in server side calls.


チュートリアル[ securing pages and API routes](https://next-auth.js.org/tutorials/securing-pages-and-api-routes)では、サーバーサイドの呼び出しで `getSession()` を使用する方法を紹介しています。



___



## getCsrfToken()[#](#getcsrftoken "Direct link to heading")



-   Client Side: **Yes**
-   Server Side: **Yes**



- クライアントサイドで **はい**
- サーバーサイド **はい**




The `getCsrfToken()` method returns the current Cross Site Request Forgery Token (CSRF Token) required to make POST requests (e.g. for signing in and signing out).


getCsrfToken()`メソッドは、サインインやサインアウトなどのPOSTリクエストに必要な、現在のCross Site Request Forgery Token (CSRF Token)を返します。



You likely only need to use this if you are not using the built-in `signIn()` and `signOut()` methods.




ビルトインの `signIn()` や `signOut()` メソッドを使用しない場合にのみ、このメソッドを使用する必要があるでしょう。


#### Client Side Example[#](#client-side-example-1 "Direct link to heading")

```
async function myFunction() {
  const csrfToken = await getCsrfToken()
  /* ... */
}
```


#### Server Side Example[#](#server-side-example-1 "Direct link to heading")

```
import { getCsrfToken } from "next-auth/client"

export default async (req, res) => {
  const csrfToken = await getCsrfToken({ req })
  /* ... */
  res.end()
}
```

___



## getProviders()[#](#getproviders "Direct link to heading")



-   Client Side: **Yes**
-   Server Side: **Yes**



- クライアント側 **はい**
- サーバーサイド **はい**



The `getProviders()` method returns the list of providers currently configured for sign in.



getProviders()`メソッドは、サインインのために現在設定されているプロバイダのリストを返します。



It calls `/api/auth/providers` and returns a list of the currently configured authentication providers.



このメソッドは `/api/auth/providers` を呼び出して、現在設定されている認証プロバイダのリストを返します。



It can be useful if you are creating a dynamic custom sign in page.


動的なカスタムサインインページを作成している場合に便利です。



___



#### API Route[#](#api-route "Direct link to heading")

```pages/api/example.js
import { getProviders } from "next-auth/client"

export default async (req, res) => {
  const providers = await getProviders()
  console.log("Providers", providers)
  res.end()
}
```


##### note



Unlike `getSession()` and `getCsrfToken()`, when calling `getProviders()` server side, you don't need to pass anything, just as calling it client side.


getSession()やgetCsrfToken()とは異なり、サーバーサイドで`getProviders()`を呼び出す際には、クライアントサイドで呼び出すのと同様に、何も渡す必要はありません。




___



## signIn()[#](#signin "Direct link to heading")



-   Client Side: **Yes**
-   Server Side: No



- クライアントサイドで **はい**。
- サーバーサイド いいえ



Using the `signIn()` method ensures the user ends back on the page they started on after completing a sign in flow. It will also handle CSRF Tokens for you automatically when signing in with email.


signIn()`メソッドを使用すると、ユーザーがサインインフローを完了した後、最初に見たページに戻ることができます。また、メールでサインインする際にはCSRFトークンを自動的に処理します。




The `signIn()` method can be called from the client in different ways, as shown below.


signIn()`メソッドは、以下に示すように、クライアントからさまざまな方法で呼び出すことができます。



#### Redirects to sign in page when clicked[#](#redirects-to-sign-in-page-when-clicked "Direct link to heading")


```
import { signIn } from "next-auth/client"

export default () => <button onClick={() => signIn()}>Sign in</button>

```



#### Starts Google OAuth sign-in flow when clicked[#](#starts-google-oauth-sign-in-flow-when-clicked "Direct link to heading")

```
import { signIn } from "next-auth/client"

export default () => (
  <button onClick={() => signIn("google")}>Sign in with Google</button>
)
```


#### Starts Email sign-in flow when clicked[#](#starts-email-sign-in-flow-when-clicked "Direct link to heading")



When using it with the email flow, pass the target `email` as an option.



emailフローで使用する場合は、オプションとしてターゲットの`email`を渡します。

```
import { signIn } from "next-auth/client"

export default ({ email }) => (
  <button onClick={() => signIn("email", { email })}>Sign in with Email</button>
)
```

#### Specifying a callbackUrl[#](#specifying-a-callbackurl "Direct link to heading")



The `callbackUrl` specifies to which URL the user will be redirected after signing in. It defaults to the current URL of a user.


callbackUrl`は、サインインした後にどのURLにリダイレクトするかを指定します。デフォルトでは、ユーザの現在のURLが指定されます。


You can specify a different `callbackUrl` by specifying it as the second argument of `signIn()`. This works for all providers.



signIn()`の第2引数に別の`callbackUrl`を指定することで、別の`callbackUrl`を指定することができます。これはすべてのプロバイダで動作します。



e.g.


例えば、以下のようになります。




-   `signIn(null, { callbackUrl: 'http://localhost:3000/foo' })`
-   `signIn('google', { callbackUrl: 'http://localhost:3000/foo' })`
-   `signIn('email', { email, callbackUrl: 'http://localhost:3000/foo' })`



The URL must be considered valid by the [redirect callback handler](https://next-auth.js.org/configuration/callbacks#redirect-callback). 

URLは、[redirect callback handler](https://next-auth.js.org/configuration/callbacks#redirect-callback)によって有効とみなされる必要があります。


By default it requires the URL to be an absolute URL at the same hostname, or else it will redirect to the homepage. 

デフォルトでは、URLが同じホスト名の絶対URLであることが要求され、そうでない場合はホームページにリダイレクトされます。


You can define your own [redirect callback](https://next-auth.js.org/configuration/callbacks#redirect-callback) to allow other URLs, including supporting relative URLs.



独自の[redirect callback](https://next-auth.js.org/configuration/callbacks#redirect-callback)を定義して、相対URLのサポートなど、他のURLを許可することができます。



#### Using the redirect: false option[#](#using-the-redirect-false-option "Direct link to heading")



##### note



The redirect option is only available for `credentials` and `email` providers.


redirectオプションは、`credentials`と`email`のプロバイダでのみ利用できます。


In some cases, you might want to deal with the sign in response on the same page and disable the default redirection. For example, if an error occurs (like wrong credentials given by the user), you might want to handle the error on the same page. For that, you can pass `redirect: false` in the second parameter object.



場合によっては、サインイン時のレスポンスを同じページで処理して、デフォルトのリダイレクトを無効にしたいこともあるでしょう。例えば、エラーが発生した場合（ユーザが与えた認証情報が間違っていた場合など）、同じページでエラーを処理したい場合があります。そのためには、2番目のパラメータオブジェクトに `redirect: false` を渡します。



e.g.


例えば、以下のようになります。




-   `signIn('credentials', { redirect: false, password: 'password' })`
-   `signIn('email', { redirect: false, email: 'bill@fillmurray.com' })`



`signIn` will then return a Promise, that resolves to the following:



そして、`signIn` は、以下のように解決する Promise を返します。

```
{
  /**
   * Will be different error codes,
   * depending on the type of error.
   */
  error: string | undefined
  /**
   * HTTP status code,
   * hints the kind of error that happened.
   */
  status: number
  /**
   * `true` if the signin was successful
   */
  ok: boolean
  /**
   * `null` if there was an error,
   * otherwise the url the user
   * should have been redirected to.
   */
  url: string | null
}
```


#### Additional params[#](#additional-params "Direct link to heading")



It is also possible to pass additional parameters to the `/authorize` endpoint through the third argument of `signIn()`.



また、`signIn()`の第3引数で`/authorize`エンドポイントに追加のパラメータを渡すことも可能です。



See the [Authorization Request OIDC spec](https://openid.net/specs/openid-connect-core-1_0.html#AuthRequest) for some ideas. (These are not the only possible ones, all parameters will be forwarded)



いくつかのアイデアについては、[Authorization Request OIDC spec](https://openid.net/specs/openid-connect-core-1_0.html#AuthRequest)を参照してください。(これらは唯一の可能性ではなく、すべてのパラメータが転送されます)



e.g.



例として



-   `signIn("identity-server4", null, { prompt: "login" })` _always ask the user to reauthenticate_
-   `signIn("auth0", null, { login_hint: "info@example.com" })` _hints the e-mail address to the provider_


- `signIn("identity-server4", null, { prompt: "login" })` _常にユーザに再認証を求めます_。
- `signIn("auth0", null, { login_hint: "info@example.com" })` _プロバイダへの電子メールアドレスをヒントにする。




##### note



You can also set these parameters through [`provider.authorizationParams`](https://next-auth.js.org/configuration/providers#oauth-provider-options).



これらのパラメータは、[`provider.authorizationParams`](https://next-auth.js.org/configuration/providers#oauth-provider-options)で設定することもできます。




##### note



The following parameters are always overridden server-side: `redirect_uri`, `state`


以下のパラメータは常にサーバーサイドでオーバーライドされます: `redirect_uri`, `state`.



___



## signOut()[#](#signout "Direct link to heading")



-   Client Side: **Yes**
-   Server Side: No



- クライアントサイドでは **Yes**（はい)
- サーバーサイド いいえ


In order to logout, use the `signOut()` method to ensure the user ends back on the page they started on after completing the sign out flow. It also handles CSRF tokens for you automatically.



ログアウトするには、`signOut()`メソッドを使用して、サインアウトのフローを完了した後、ユーザーが最初に見たページに戻るようにします。また、CSRFトークンも自動的に処理されます。




It reloads the page in the browser when complete.


完了するとブラウザでページを再読み込みします。


```
import { signOut } from "next-auth/client"

export default () => <button onClick={() => signOut()}>Sign out</button>

```

#### Specifying a callbackUrl[#](#specifying-a-callbackurl-1 "Direct link to heading")



As with the `signIn()` function, you can specify a `callbackUrl` parameter by passing it as an option.



`signIn()`関数と同様に、`callbackUrl`パラメータをオプションで指定することができます。



e.g. `signOut({ callbackUrl: 'http://localhost:3000/foo' })`



The URL must be considered valid by the [redirect callback handler](https://next-auth.js.org/configuration/callbacks#redirect-callback). By default this means it must be an absolute URL at the same hostname (or else it will default to the homepage); 

URLは、[リダイレクトコールバックハンドラ](https://next-auth.js.org/configuration/callbacks#redirect-callback)が有効とみなすものでなければなりません。デフォルトでは、同じホスト名の絶対URLでなければなりません（さもなければ、デフォルトでホームページになります）。

you can define your own custom [redirect callback](https://next-auth.js.org/configuration/callbacks#redirect-callback) to allow other URLs, including supporting relative URLs.




独自のカスタム[redirect callback](https://next-auth.js.org/configuration/callbacks#redirect-callback)を定義して、相対URLのサポートなど、他のURLを許可することができます。



#### Using the redirect: false option[#](#using-the-redirect-false-option-1 "Direct link to heading")



If you pass `redirect: false` to `signOut`, the page will not reload. The session will be deleted, and the `useSession` hook is notified, so any indication about the user will be shown as logged out automatically. It can give a very nice experience for the user.


signOut`に`redirect: false`を渡した場合、ページはリロードされません。セッションは削除され、`useSession` フックが通知されるので、ユーザーに関するあらゆる表示は自動的にログアウトしたものとして表示されます。これはユーザーにとって非常に良い経験となります。



##### tip



If you need to redirect to another page but you want to avoid a page reload, you can try: `const data = await signOut({redirect: false, callbackUrl: "/foo"})` where `data.url` is the validated url you can redirect the user to without any flicker by using Next.js's `useRouter().push(data.url)`



別のページにリダイレクトする必要があるが、ページのリロードは避けたいという場合には、次のようにします。`const data = await signOut({redirect: false, callbackUrl: "/foo"})` ここで、`data.url` は検証されたURLで、Next.jsの`useRouter().push(data.url)`を使うことで、フリッカーなしでユーザーをリダイレクトすることができます。




___



## Provider[#](#provider "Direct link to heading")



Using the supplied React `<Provider>` allows instances of `useSession()` to share the session object across components, by using [React Context](https://reactjs.org/docs/context.html) under the hood.


付属のReact `<Provider>`を使用すると、ボンネット内で[React Context](https://reactjs.org/docs/context.html)を使用して、`useSession()`のインスタンスがコンポーネント間でセッションオブジェクトを共有できるようになります。



This improves performance, reduces network calls and avoids page flicker when rendering. It is highly recommended and can be easily added to all pages in Next.js apps by using `pages/_app.js`.



これにより、パフォーマンスが向上し、ネットワークコールが減少し、レンダリング時のページのちらつきが回避されます。Next.jsアプリのすべてのページに、`pages/_app.js`を使って簡単に追加することができるので、強くお勧めします。



```pages/_app.js
import { Provider } from "next-auth/client"

export default function App({ Component, pageProps }) {
  return (
    <Provider session={pageProps.session}>
      <Component {...pageProps} />
    </Provider>
  )
}
```

If you pass the `session` page prop to the `<Provider>` – as in the example above – you can avoid checking the session twice on pages that support both server and client side rendering.


上の例のように、`<Provider>` に `session` ページのプロップを渡すと、サーバーサイドとクライアントサイドの両方のレンダリングをサポートしているページで、セッションを2回チェックする必要がなくなります。




This only works on pages where you provide the correct `pageProps`, however. This is normally done in `getInitialProps` or `getServerSideProps` like so:


ただし、これは正しい `pageProps` を提供しているページでのみ機能します。これは通常、`getInitialProps`や`getServerSideProps`で次のように行います。



```pages/index.js
import { getSession } from "next-auth/client"

...

export async function getServerSideProps(ctx) {
  return {
    props: {
      session: await getSession(ctx)
    }
  }
}

```

If every one of your pages needs to be protected, you can do this in `_app`, otherwise you can do it on a page-by-page basis. Alternatively, you can do per page authentication checks client side, instead of having each auth check be blocking (SSR) by using the method described below in [alternative client session handling](#custom-client-session-handling).


すべてのページを保護する必要がある場合には、`_app`で行うことができますが、そうでなければページごとに行うことができます。また、以下の[alternative client session handling](#custom-client-session-handling)で説明する方法を使えば、認証チェックのたびにブロッキング(SSR)を行うのではなく、クライアントサイドでページごとの認証チェックを行うこともできます。



### Options[#](#options "Direct link to heading")



The session state is automatically synchronized across all open tabs/windows and they are all updated whenever they gain or lose focus or the state changes in any of them (e.g. a user signs in or out).



セッションの状態は、開いているすべてのタブ/ウィンドウ間で自動的に同期され、フォーカスを得たり失ったり、いずれかのタブ/ウィンドウの状態が変更されたりするたびに、すべてのタブ/ウィンドウが更新されます (例: ユーザーがサインインまたはログアウトした場合)。



If you have session expiry times of 30 days (the default) or more then you probably don't need to change any of the default options in the Provider. If you need to, you can trigger an update of the session object across all tabs/windows by calling `getSession()` from a client side function.


セッションの有効期限が30日(デフォルト)以上ある場合は、プロバイダのデフォルトのオプションを変更する必要はないでしょう。必要であれば、クライアント側の関数から `getSession()` を呼び出すことで、すべてのタブ/ウィンドウのセッションオブジェクトの更新を引き起こすことができます。



However, if you need to customise the session behaviour and/or are using short session expiry times, you can pass options to the provider to customise the behaviour of the `useSession()` hook.



しかし、セッションの動作をカスタマイズする必要がある場合や、短いセッションの有効期限を使用している場合は、プロバイダにオプションを渡して、`useSession()`フックの動作をカスタマイズすることができます。



```pages/_app.js
import { Provider } from "next-auth/client"

export default function App({ Component, pageProps }) {
  return (
    <Provider
      session={pageProps.session}
      options={{
        clientMaxAge: 60, // Re-fetch session if cache is older than 60 seconds
        keepAlive: 5 * 60, // Send keepAlive message every 5 minutes
      }}
    >
      <Component {...pageProps} />
    </Provider>
  )
}
```


##### note



**These options have no effect on clients that are not signed in.**



**これらのオプションは、サインインしていないクライアントには効果がありません**。



Every tab/window maintains its own copy of the local session state; the session is not stored in shared storage like localStorage or sessionStorage. Any update in one tab/window triggers a message to other tabs/windows to update their own session state.


すべてのタブ/ウィンドウは、ローカルのセッション状態のコピーを維持します。セッションは、localStorage や sessionStorage のような共有ストレージには保存されません。セッションは localStorage や sessionStorage のような共有ストレージには保存されません。あるタブ/ウィンドウが更新されると、他のタブ/ウィンドウにメッセージが送られ、それぞれのセッション状態が更新されます。


Using low values for `clientMaxAge` or `keepAlive` will increase network traffic and load on authenticated clients and may impact hosting costs and performance.



clientMaxAge`や`keepAlive`に低い値を使用すると、ネットワークトラフィックや認証済みクライアントの負荷が増大し、ホスティングのコストやパフォーマンスに影響を与える可能性があります。



#### Client Max Age[#](#client-max-age "Direct link to heading")



The `clientMaxAge` option is the maximum age a session data can be on the client before it is considered stale.


clientMaxAge`オプションは、セッションデータがクライアント上で古くなったと判断されるまでの最大年齢を指定します。



When `clientMaxAge` is set to `0` (the default) the cache will always be used when useSession is called and only explicit calls made to get the session status (i.e. `getSession()`) or event triggers, such as signing in or out in another tab/window, or a tab/window gaining or losing focus, will trigger an update of the session state.


`clientMaxAge` が `0` に設定されている場合 (デフォルト)、 useSession が呼び出されたときには常にキャッシュが使用され、セッションの状態を取得するための明示的な呼び出し (例: `getSession()`) や、別のタブやウィンドウにサインインしたりログアウトしたり、タブやウィンドウにフォーカスが当たったり外れたりといったイベントトリガーのみが、セッションの状態を更新するきっかけとなります。



If set to any value other than zero, it specifies in seconds the maximum age of session data on the client before the `useSession()` hook will call the server again to sync the session state.


ゼロ以外の値を設定すると、`useSession()`フックがセッション状態を同期するためにサーバーを再度呼び出すまでの、クライアント上のセッションデータの最大経過時間を秒単位で指定します。



Unless you have a short session expiry time (e.g. < 24 hours) you probably don't need to change this option. Setting this option to too short a value will increase load (and potentially hosting costs).


セッションの有効期限が短い場合 (例: < 24時間) を除いて、このオプションを変更する必要はないでしょう。このオプションをあまり短い値に設定すると、負荷が高くなり(ホスティングコストが高くなる可能性があります)ます。



The value for `clientMaxAge` should always be lower than the value of the session `maxAge` option.


`clientMaxAge` の値は、常にセッションの `maxAge` オプションの値よりも小さくしてください。



#### Keep Alive[#](#keep-alive "Direct link to heading")



The `keepAlive` option is how often the client should contact the server to avoid a session expiring.


keepAlive`オプションは、セッションが終了しないように、クライアントがサーバーに問い合わせる頻度を指定します。




When `keepAlive` is set to `0` (the default) it will not send a keep alive message.



`keepAlive` を `0` に設定すると (デフォルト)、キープアライブメッセージを送信しません。



If set to any value other than zero, it specifies in seconds how often the client should contact the server to update the session state. If the session state has expired when it is triggered, all open tabs/windows will be updated to reflect this.


ゼロ以外の値を設定した場合、クライアントがサーバーに連絡してセッション状態を更新する頻度を秒単位で指定します。keepAlive`が起動されたときにセッションの状態が期限切れになっていた場合は、開いているすべてのタブやウィンドウが更新され、それが反映されます。



The value for `keepAlive` should always be lower than the value of the session `maxAge` option.




`keepAlive` の値は、常にセッションの `maxAge` オプションの値よりも小さくしてください。



##### note



See [**the Next.js documentation**](https://nextjs.org/docs/advanced-features/custom-app) for more information on **\_app.js** in Next.js applications.


Next.jsアプリケーションにおける**\.js**の詳細については、[**the Next.js documentation**](https://nextjs.org/docs/advanced-features/custom-app)を参照してください。



## Alternatives[#](#alternatives "Direct link to heading")



### Custom Client Session Handling[#](#custom-client-session-handling "Direct link to heading")



Due to the way Next.js handles `getServerSideProps` / `getInitialProps`, every protected page load has to make a server-side query to check if the session is valid and then generate the requested page. This alternative solution allows for showing a loading state on the initial check and every page transition afterward will be client-side, without having to check with the server and regenerate pages.


Next.jsの `getServerSideProps` / `getInitialProps` の処理方法により、保護されたページをロードするたびに、セッションが有効かどうかを確認するためのサーバーサイドのクエリを実行し、リクエストされたページを生成する必要があります。この代替案では、最初のチェック時にローディング状態を表示し、その後のすべてのページ遷移はクライアントサイドで行うことができ、サーバーに確認してページを再生成する必要がありません。



```pages/admin.jsx
export default function AdminDashboard() {
  const [session] = useSession()
  // session is always non-null inside this page, all the way down the React tree.
  return "Some super secret dashboard"
}

AdminDashboard.auth = true

```


```pages/_app.jsx

export default function App({ Component, pageProps }) {
  return (
    <Provider session={pageProps.session}>
      {Component.auth ? (
        <Auth>
          <Component {...pageProps} />
        </Auth>
      ) : (
        <Component {...pageProps} />
      )}
    </Provider>
  )
}

function Auth({ children }) {
  const [session, loading] = useSession()
  const isUser = !!session?.user
  React.useEffect(() => {
    if (loading) return // Do nothing while loading
    if (!isUser) signIn() // If not authenticated, force log in
  }, [isUser, loading])

  if (isUser) {
    return children
  }

  // Session is being fetched, or no user.
  // If no user, useEffect() will redirect.
  return <div>Loading...</div>
}

```


It can be easily be extended/modified to support something like an options object for role based authentication on pages. An example:



これは、ページでのロールベースの認証のためのオプションオブジェクトのようなものをサポートするために、簡単に拡張/修正することができます。例を挙げます。



```pages/admin.jsx
AdminDashboard.auth = {
  role: "admin",
  loading: <AdminLoadingSkeleton />,
  unauthorized: "/login-with-different-user", // redirect to this url
}
```

Because of how \_app is done, it won't unnecessarily contact the /api/auth/session endpoint for pages that do not require auth.



この方法では、認証を必要としないページでは、不必要に/api/auth/sessionエンドポイントにアクセスすることはありません。



More information can be found in the following [Github Issue](https://github.com/nextauthjs/next-auth/issues/1210).


詳細は以下の[Github Issue](https://github.com/nextauthjs/next-auth/issues/1210)に記載されています。



### NextAuth.js + React-Query[#](#nextauthjs--react-query "Direct link to heading")



There is also an alternative client-side API library based upon [`react-query`](https://www.npmjs.com/package/react-query) available under [`nextauthjs/react-query`](https://github.com/nextauthjs/react-query).


また、[`react-query`](https://www.npmjs.com/package/react-query)をベースにした別のクライアントサイドAPIライブラリが[`nextauthjs/react-query`](https://github.com/nextauthjs/react-query)で提供されています。


If you use `react-query` in your project already, you can leverage it with NextAuth.js to handle the client-side session management for you as well. This replaces NextAuth.js's native `useSession` and `Provider` from `next-auth/client`.


もしあなたのプロジェクトで `react-query` を使用しているのであれば、NextAuth.js と一緒に活用することで、クライアントサイドのセッション管理を行うことができます。これは、NextAuth.js のネイティブな `useSession` と `Provider` を `next-auth/client` から置き換えるものです。




See repository [`README`](https://github.com/nextauthjs/react-query) for more details.



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/getting-started/client.md)