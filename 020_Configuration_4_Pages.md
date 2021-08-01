Pages | NextAuth.js
https://next-auth.js.org/configuration/pages




# Pages



NextAuth.js automatically creates simple, unbranded authentication pages for handling Sign in, Sign out, Email Verification and displaying error messages.


NextAuth.jsは、サインイン、サインアウト、メール認証、エラーメッセージの表示などを行う、シンプルでブランド力のない認証ページを自動的に作成します。


The options displayed on the sign up page are automatically generated based on the providers specified in the options passed to NextAuth.js.


サインアップページに表示されるオプションは、NextAuth.jsに渡されるオプションで指定されたプロバイダーに基づいて自動的に生成されます。




To add a custom login page, you can use the `pages` option:

カスタムのログインページを追加するには、`pages`オプションを使用します。



```pages/api/auth/[...nextauth].js
...
  pages: {
    signIn: '/auth/signin',
    signOut: '/auth/signout',
    error: '/auth/error', // Error code passed in query string as ?error=
    verifyRequest: '/auth/verify-request', // (used for check email message)
    newUser: '/auth/new-user' // New users will be directed here on first sign in (leave the property out if not of interest)
  }
...



```






## Error codes[#](#error-codes "Direct link to heading")



We purposefully restrict the returned error codes for increased security.


セキュリティ強化のため、返されるエラーコードを意図的に制限しています。



### Error page[#](#error-page "Direct link to heading")



The following errors are passed as error query parameters to the default or overridden error page:


以下のエラーは、デフォルトまたはオーバーライドされたエラーページにエラークエリパラメータとして渡されます。


-   **Configuration**: There is a problem with the server configuration. Check if your [options](https://next-auth.js.org/configuration/options#options) is correct.
-   **AccessDenied**: Usually occurs, when you restricted access through the [`signIn` callback](https://next-auth.js.org/configuration/callbacks#sign-in-callback), or [`redirect` callback](https://next-auth.js.org/configuration/callbacks#redirect-callback)
-   **Verification**: Related to the Email provider. The token has expired or has already been used
-   **Default**: Catch all, will apply, if none of the above matched


- **設定**: サーバーの設定に問題があります。options](https://next-auth.js.org/configuration/options#options)が正しいかどうか確認してください。
- **AccessDenied**: 通常、[signIn`コールバック](https://next-auth.js.org/configuration/callbacks#sign-in-callback)または[`redirect`コールバック](https://next-auth.js.org/configuration/callbacks#redirect-callback)でアクセスを制限した場合に発生します。
- **Verification**。メールプロバイダーに関連しています。トークンの有効期限が切れているか、すでに使用されています。
- **デフォルト**: 上記のどれにも当てはまらない場合に適用されます。


Example: `/auth/error?error=Configuration`



### Sign-in page[#](#sign-in-page "Direct link to heading")



The following errors are passed as error query parameters to the default or overridden sign-in page:


以下のエラーは、デフォルトまたはオーバーライドされたサインインページにエラーのクエリパラメーターとして渡されます。



-   **OAuthSignin**: Error in constructing an authorization URL ([1](https://github.com/nextauthjs/next-auth/blob/457952bb5abf08b09861b0e5da403080cd5525be/src/server/lib/signin/oauth.js), [2](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/pkce-handler.js), [3](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/state-handler.js)),
-   **OAuthCallback**: Error in handling the response ([1](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/callback.js), [2](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/pkce-handler.js), [3](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/state-handler.js)) from an OAuth provider.
-   **OAuthCreateAccount**: Could not create OAuth provider user in the database.
-   **EmailCreateAccount**: Could not create email provider user in the database.
-   **Callback**: Error in the [OAuth callback handler route](https://github.com/nextauthjs/next-auth/blob/main/src/server/routes/callback.js)
-   **OAuthAccountNotLinked**: If the email on the account is already linked, but not with this OAuth account
-   **EmailSignin**: Sending the e-mail with the verification token failed
-   **CredentialsSignin**: The `authorize` callback returned `null` in the [Credentials provider](https://next-auth.js.org/providers/credentials). We don't recommend providing information about which part of the credentials were wrong, as it might be abused by malicious hackers.
-   **Default**: Catch all, will apply, if none of the above matched



- **OAuthSignin**: 認証URLの構築でエラーが発生しました([1](https://github.com/nextauthjs/next-auth/blob/457952bb5abf08b09861b0e5da403080cd5525be/src/server/lib/signin/oauth.js), [2](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/pkce-handler.js), [3](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/state-handler.js))。
- **OAuthCallback**: OAuthプロバイダからの応答([1](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/callback.js), [2](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/pkce-handler.js), [3](https://github.com/nextauthjs/next-auth/blob/main/src/server/lib/oauth/state-handler.js))の処理でエラーが発生しました。
- **OAuthCreateAccount**: データベースにOAuthプロバイダーのユーザーを作成できませんでした。
- **EmailCreateAccount**。データベース内に電子メール・プロバイダ・ユーザを作成できませんでした。
- **コールバック**。OAuthコールバックハンドラールート]でのエラー(https://github.com/nextauthjs/next-auth/blob/main/src/server/routes/callback.js)
- **OAuthAccountNotLinked**。アカウントの電子メールがすでにリンクされているが、このOAuthアカウントとはリンクされていない場合
- **EmailSignin**: 検証トークンを含むメールの送信に失敗した場合
- **CredentialsSignin**: 認証情報プロバイダ](https://next-auth.js.org/providers/credentials)の`authorize`コールバックが`null`を返しました。認証情報のどの部分が間違っていたかという情報を提供することは、悪意のあるハッカーに悪用される可能性があるため、お勧めしません。
- **デフォルト**: Catch all, 上記のどれにもマッチしない場合に適用されます。




Example: `/auth/error?error=Default`



## Theming[#](#theming "Direct link to heading")



By default, the built-in pages will follow the system theme, utilizing the [`prefer-color-scheme`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) Media Query. You can override this to always use a dark or light theme, through the [`theme` option](https://next-auth.js.org/configuration/options#theme).



デフォルトでは、組み込みページはシステムテーマに従い、[`prefer-color-scheme`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) メディアクエリを利用します。theme`オプション](https://next-auth.js.org/configuration/options#theme)を使って、常に暗いテーマや明るいテーマを使用するように上書きすることができます。



## Examples[#](#examples "Direct link to heading")



### OAuth Sign in[#](#oauth-sign-in "Direct link to heading")



In order to get the available authentication providers and the URLs to use for them, you can make a request to the API endpoint `/api/auth/providers`:



利用可能な認証プロバイダと、そのプロバイダに使用するURLを取得するには、APIエンドポイントの `/api/auth/providers` にリクエストを行います。



```pages/auth/signin.js
import { getProviders, signIn } from 'next-auth/client'

export default function SignIn({ providers }) {
  return (
    <>
      {Object.values(providers).map(provider => (
        <div key={provider.name}>
          <button onClick={() => signIn(provider.id)}>Sign in with {provider.name}</button>
        </div>
      ))}
    </>
  )
}

// This is the recommended way for Next.js 9.3 or newer
export async function getServerSideProps(context){
  const providers = await getProviders()
  return {
    props: { providers }
  }
}

/*
// If older than Next.js 9.3
SignIn.getInitialProps = async () => {
  return {
    providers: await getProviders()
  }
}
*/

```





### Email Sign in[#](#email-sign-in "Direct link to heading")



If you create a custom sign in form for email sign in, you will need to submit both fields for the **email** address and **csrfToken** from **/api/auth/csrf** in a POST request to **/api/auth/signin/email**.


メールサインイン用のカスタムサインインフォームを作成する場合は、**/api/auth/csrf**から**email**アドレスと**csrfToken**の両方のフィールドを**/api/auth/signin/email**へのPOSTリクエストで送信する必要があります。


```pages/auth/email-signin.js
import { getCsrfToken } from 'next-auth/client'

export default function SignIn({ csrfToken }) {
  return (
    <form method='post' action='/api/auth/signin/email'>
      <input name='csrfToken' type='hidden' defaultValue={csrfToken}/>
      <label>
        Email address
        <input type='email' id='email' name='email'/>
      </label>
      <button type='submit'>Sign in with Email</button>
    </form>
  )
}

// This is the recommended way for Next.js 9.3 or newer
export async function getServerSideProps(context){
  const csrfToken = await getCsrfToken(context)
  return {
    props: { csrfToken }
  }
}

/*
// If older than Next.js 9.3
SignIn.getInitialProps = async (context) => {
  return {
    csrfToken: await getCsrfToken(context)
  }
}
*/

```



You can also use the `signIn()` function which will handle obtaining the CSRF token for you:



CSRFトークンの取得を代行してくれる`signIn()`関数を使うこともできます。


```
signIn('email', { email: 'jsmith@example.com' })
```




### Credentials Sign in[#](#credentials-sign-in "Direct link to heading")



If you create a sign in form for credentials based authentication, you will need to pass a **csrfToken** from **/api/auth/csrf** in a POST request to **/api/auth/callback/credentials**.


クレデンシャルベースの認証用にサインインフォームを作成する場合は、 **/api/auth/csrf** から **/api/auth/callback/credentials** へのPOSTリクエストで **csrfToken** を渡す必要があります。



```pages/auth/credentials-signin.js
import { getCsrfToken } from 'next-auth/client'

export default function SignIn({ csrfToken }) {
  return (
    <form method='post' action='/api/auth/callback/credentials'>
      <input name='csrfToken' type='hidden' defaultValue={csrfToken}/>
      <label>
        Username
        <input name='username' type='text'/>
      </label>
      <label>
        Password
        <input name='password' type='password'/>
      </label>
      <button type='submit'>Sign in</button>
    </form>
  )
}

// This is the recommended way for Next.js 9.3 or newer
export async function getServerSideProps(context) {
  return {
    props: {
      csrfToken: await getCsrfToken(context)
    }
  }
}

/*
// If older than Next.js 9.3
SignIn.getInitialProps = async (context) => {
  return {
    csrfToken: await getCsrfToken(context)
  }
}
*/
```



You can also use the `signIn()` function which will handle obtaining the CSRF token for you:


CSRFトークンの取得を代行してくれる`signIn()`関数を使うこともできます。


```
signIn('credentials', { username: 'jsmith', password: '1234' })

```



##### tip



Remember to put any custom pages in a folder outside **/pages/api** which is reserved for API code. As per the examples above, a location convention suggestion is `pages/auth/...`.



カスタムページは、APIコード用に予約されている **/pages/api** の外のフォルダに置くことを忘れないでください。上記の例では、「pages/auth/...`」という場所を提案しています。



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/configuration/pages.md)