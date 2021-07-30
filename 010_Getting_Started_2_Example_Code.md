Example Code | NextAuth.js
https://next-auth.js.org/getting-started/example



# Example Code

# コード例



## Get started with NextAuth.js[#](#get-started-with-nextauthjs "Direct link to heading")



The example code below describes how to add authentication to a Next.js app.


以下のサンプルコードでは、Next.jsのアプリに認証機能を追加する方法を説明しています。



##### tip



The easiest way to get started is to clone the [example app](https://github.com/nextauthjs/next-auth-example) and follow the instructions in README.md. You can try out a live demo at [next-auth-example.vercel.app](https://next-auth-example.vercel.app)



一番簡単な始め方は、[example app](https://github.com/nextauthjs/next-auth-example)をクローンして、README.mdの指示に従うことです。ライブデモは[next-auth-example.vercel.app](https://next-auth-example.vercel.app)で試すことができます。


### Add API route[#](#add-api-route "Direct link to heading")

### APIルートの追加[#](#add-api-route "Direct link to heading")



To add NextAuth.js to a project create a file called `[...nextauth].js` in `pages/api/auth`.


NextAuth.jsをプロジェクトに追加するには、`pages/api/auth`に`[...nextauth].js`というファイルを作成します。



[Read more about how to add authentication providers.](https://next-auth.js.org/configuration/providers)


[認証プロバイダの追加方法についてはこちらをご覧ください。](https://next-auth.js.org/configuration/providers)



```pages/api/auth/\[...nextauth\].js
import NextAuth from 'next-auth'
import Providers from 'next-auth/providers'

export default NextAuth({
  // Configure one or more authentication providers
  // 1つまたは複数の認証プロバイダーを設定します
  providers: [
    Providers.GitHub({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET
    }),
    // ...add more providers here
    // 1つまたは複数の認証プロバイダーを設定します
  ],

  // A database is optional, but required to persist accounts in a database
  // データベースはオプションですが、アカウントをデータベースに保存するために必要です
  database: process.env.DATABASE_URL,
})
```

persist
【＠】パーシスト,パスィスト,【変化】《動》persists | persisting | persisted,【大学入試】,《自動-1》しつこく主張する,主張し続ける,言い張る,固執する,やり通す,あくまで通す,《自動-2》存続する,持続する,続く,生き残る


All requests to `/api/auth/*` (signin, callback, signout, etc) will automatically be handed by NextAuth.js.

`/api/auth/*` へのすべてのリクエスト（サインイン、コールバック、サインアウトなど）は、NextAuth.js によって自動的に処理されます。

##### tip



See the [options documentation](https://next-auth.js.org/configuration/options) for how to configure providers, databases and other options.

プロバイダやデータベースなどのオプションの設定方法は、[options documentation](https://next-auth.js.org/configuration/options)を参照してください。



### Add React Hook[#](#add-react-hook "Direct link to heading")

### Reactフックの追加[#](#add-react-hook "Direct link to heading")


The `useSession()` React Hook in the NextAuth.js client is the easiest way to check if someone is signed in.

NextAuth.jsクライアントの`useSession()` React Hookは、誰かがサインインしているかどうかを確認する最も簡単な方法です。


```pages/index.js
import { signIn, signOut, useSession } from 'next-auth/client'

export default function Page() {
  const [ session, loading ] = useSession()

  return <>
    {!session && <>
      Not signed in <br/>
      <button onClick={() => signIn()}>Sign in</button>
    </>}
    {session && <>
      Signed in as {session.user.email} <br/>
      <button onClick={() => signOut()}>Sign out</button>
    </>}
  </>
}
```

##### tip



You can use the `useSession` hook from anywhere in your application (e.g. in a header component).


`useSession`フックは、アプリケーションのどこからでも（例えばヘッダーコンポーネントの中で）使うことができます。


### Add session state[#](#add-session-state "Direct link to heading")



### セッション状態の追加[#](#add-session-state "Direct link to heading")

To allow session state to be shared between pages - which improves performance, reduces network traffic and avoids component state changes while rendering - you can use the NextAuth.js Provider in `pages/_app.js`.

ページ間でセッション状態を共有できるようにすると、パフォーマンスが向上し、ネットワークトラフィックが減少し、レンダリング中にコンポーネントの状態が変化するのを避けることができます。NextAuth.jsプロバイダを`pages/_app.js`で使用できます。



```pages/_app.js
import { Provider } from 'next-auth/client'

export default function App ({ Component, pageProps }) {
  return (
    <Provider session={pageProps.session}>
      <Component {...pageProps} />
    </Provider>
  )
}
```




##### tip



Check out the [client documentation](https://next-auth.js.org/getting-started/client) to see how you can improve the user experience and page performance by using the NextAuth.js client.

NextAuth.jsクライアントを使うことで、どのようにユーザーエクスペリエンスやページパフォーマンスを向上させることができるのか、[client documentation](https://next-auth.js.org/getting-started/client)をチェックしてみましょう。



### Deploying to production[#](#deploying-to-production "Direct link to heading")

### 本番環境へのデプロイ[#](#deploying-to-production "Direct link to heading")



When deploying your site set the `NEXTAUTH_URL` environment variable to the canonical URL of the website.

canonical
《形-1》教会法上に従った,聖書正典の,正統な,権威のある,《形-2》規範的な,標準的な,基準の

サイトをデプロイする際には、環境変数 `NEXTAUTH_URL` にウェブサイトの正規の URL を設定します。


```
NEXTAUTH_URL=https://example.com
```




##### tip



In production, this needs to be set as an environment variable on the service you use to deploy your app.


本番環境では、アプリのデプロイに使用するサービス上で、これを環境変数として設定する必要があります。



To set environment variables on Vercel, you can use the [dashboard](https://vercel.com/dashboard) or the `vercel env pull` [command](https://vercel.com/docs/build-step#development-environment-variables).



Vercelで環境変数を設定するには、[dashboard](https://vercel.com/dashboard)または`vercel env pull` [command](https://vercel.com/docs/build-step#development-environment-variables)を使用します。


[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/getting-started/example.md)