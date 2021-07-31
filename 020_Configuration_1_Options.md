Options | NextAuth.js
https://next-auth.js.org/configuration/options




# Options



## Environment Variables[#](#environment-variables "Direct link to heading")



### NEXTAUTH_URL[#](#nextauth_url "Direct link to heading")



When deploying to production, set the `NEXTAUTH_URL` environment variable to the canonical URL of your site.


本番環境にデプロイする場合は、環境変数`NEXTAUTH_URL`にサイトの正規のURLを設定してください。



NEXTAUTH_URL=https://example.com



Copy



If your Next.js application uses a custom base path, specify the route to the API endpoint in full.


Next.jsアプリケーションがカスタムベースパスを使用している場合は、APIエンドポイントへのルートを完全に指定します。



_e.g. `NEXTAUTH_URL=https://example.com/custom-route/api/auth`_



##### tip



To set environment variables on Vercel, you can use the [dashboard](https://vercel.com/dashboard) or the `vercel env` command.

Vercelで環境変数を設定するには、[dashboard](https://vercel.com/dashboard)または`vercel env`コマンドを使用します。


### NEXTAUTH\_URL\_INTERNAL[#](#nextauth_url_internal "Direct link to heading")



If provided, server-side calls will use this instead of `NEXTAUTH_URL`. Useful in environments when the server doesn't have access to the canonical URL of your site. Defaults to `NEXTAUTH_URL`.


提供された場合、サーバーサイドの呼び出しは `NEXTAUTH_URL` の代わりにこれを使用します。サーバーがサイトの正規のURLにアクセスできない環境で便利です。デフォルトでは `NEXTAUTH_URL` が使用されます。

```
NEXTAUTH\_URL\_INTERNAL=http://10.240.8.16
```

___



## Options[#](#options "Direct link to heading")



Options are passed to NextAuth.js when initializing it in an API route.



NextAuth.js を API ルートで初期化する際にオプションが渡されます。



### providers[#](#providers "Direct link to heading")



-   **Default value**: `[]`
-   **Required**: _Yes_


- **デフォルト値**です。`[]`
- **必須**です。_Yes_



#### Description[#](#description "Direct link to heading")



An array of authentication providers for signing in (e.g. Google, Facebook, Twitter, GitHub, Email, etc) in any order. This can be one of the built-in providers or an object with a custom provider.



サインインするための認証プロバイダー（Google、Facebook、Twitter、GitHub、Emailなど）を任意の順番で配列したものです。これは、ビルトインのプロバイダの一つでも、カスタムプロバイダを持つオブジェクトでも構いません。



See the [providers documentation](https://next-auth.js.org/configuration/providers) for a list of supported providers and how to use them.



サポートされているプロバイダの一覧とその使い方については、[providers documentation](https://next-auth.js.org/configuration/providers)を参照してください。


___



### database[#](#database "Direct link to heading")



-   **Default value**: `null`
-   **Required**: _No (unless using email provider)_



- **デフォルト値**: null`
- **必須**: _No (メールプロバイダを使用していない場合)_


#### Description[#](#description-1 "Direct link to heading")



[A database connection string or configuration object.](https://next-auth.js.org/configuration/databases)


[データベースの接続文字列または構成オブジェクトです](https://next-auth.js.org/configuration/databases)



___



### secret[#](#secret "Direct link to heading")



-   **Default value**: `string` (_SHA hash of the "options" object_)
-   **Required**: _No - but strongly recommended!_


- **デフォルト値**です。文字列` (「options」オブジェクトの_SHAハッシュ_)
- **必須**: _いいえ - しかし、強くお勧めします！ _



#### Description[#](#description-2 "Direct link to heading")



A random string used to hash tokens, sign cookies and generate cryptographic keys.


トークンのハッシュ化、クッキーの署名、暗号鍵の生成に使用されるランダムな文字列です。




If not specified, it uses a hash for all configuration options, including Client ID / Secrets for entropy.



指定されていない場合は、エントロピーのために Client ID / Secrets を含むすべての設定オプションにハッシュを使用します。


The default behaviour is volatile, and it is strongly recommended you explicitly specify a value to avoid invalidating end user sessions when configuration changes are deployed.

volatile
《形-1》移り気な,気紛れな,興奮しやすい,激しやすい,軽薄な,不安定な,変わりやすい,急変する,予測が非常に難しい,《形-2》一触即発の,蒸発しやすい,爆発しやすい,《形-3》《電》揮発性の,《名》《電》揮発性

explicitly
《副》はっきりと,明白に,明示的に

specify
《他動》～を指定する,～に記入する,明白に記す,明記する,指示する,特定する,＾明確［明細］に述べる,～の仕様を定める

デフォルトの動作は揮発性です。設定変更を展開したときにエンドユーザーのセッションが無効にならないように、明示的に値を指定することを強くお勧めします。



___



### session[#](#session "Direct link to heading")



-   **Default value**: `object`
-   **Required**: _No_



#### Description[#](#description-3 "Direct link to heading")



The `session` object and all properties on it are optional.

`session`オブジェクトとそれに付随するすべてのプロパティはオプションです。



Default values for this option are shown below:

このオプションのデフォルト値は以下のとおりです。

```

session: {
  // Use JSON Web Tokens for session instead of database sessions.
  // This option can be used with or without a database for users/accounts.
  // Note: `jwt` is automatically set to `true` if no database is specified.
  jwt: false,

  // Seconds - How long until an idle session expires and is no longer valid.
  maxAge: 30 * 24 * 60 * 60, // 30 days

  // Seconds - Throttle how frequently to write to database to extend a session.
  // Use it to limit write operations. Set to 0 to always update the database.
  // Note: This option is ignored if using JSON Web Tokens
  updateAge: 24 * 60 * 60, // 24 hours
}

```


// Use JSON Web Tokens for session instead of database sessions.


// データベースセッションではなく、JSON Web Tokens をセッションに使用します。



// This option can be used with or without a database for users/accounts.


// このオプションは、ユーザー/アカウント用のデータベースがあってもなくても使用できます。



// Note: \`jwt\` is automatically set to \`true\` if no database is specified.


// 注意：データベースが指定されていない場合は、自動的に「jwt」が「true」になります。




// Seconds - How long until an idle session expires and is no longer valid.


// Seconds - アイドルセッションが期限切れで無効になるまでの時間です。


// Seconds - Throttle how frequently to write to database to extend a session.


// Seconds - セッションを延長するために、データベースへの書き込みの頻度を調整します。





// Use it to limit write operations. Set to 0 to always update the database.


// 書き込み操作を制限するために使用します。0 に設定すると常にデータベースを更新します。



// Note: This option is ignored if using JSON Web Tokens


// 注意：このオプションは、JSON Web Tokens を使用している場合は無視されます。





___



### jwt[#](#jwt "Direct link to heading")



-   **Default value**: `object`
-   **Required**: _No_



#### Description[#](#description-4 "Direct link to heading")



JSON Web Tokens can be used for session tokens if enabled with `session: { jwt: true }` option. JSON Web Tokens are enabled by default if you have not specified a database.


JSON Web Tokensは、`session.{ jwt: true }`オプションで有効にすると、セッショントークンとして使用できます。`{jwt: true }` オプションで有効にすると、セッショントークンに JSON Web Tokens を使うことができます。データベースを指定していない場合は、デフォルトでJSON Web Tokensが有効になります。



By default JSON Web Tokens are signed (JWS) but not encrypted (JWE), as JWT encryption adds additional overhead and comes with some caveats. You can enable encryption by setting `encryption: true`.


デフォルトでは、JSON Web Tokensは署名されていますが(JWS)、暗号化されていません(JWE)。JWTの暗号化はオーバーヘッドを増やし、いくつかの注意点があるからです。`encryption: true`を設定することで、暗号化を有効にできます。



#### JSON Web Token Options[#](#json-web-token-options "Direct link to heading")

```
jwt: {
  // A secret to use for key generation - you should set this explicitly
  // Defaults to NextAuth.js secret if not explicitly specified.
  // This is used to generate the actual signingKey and produces a warning
  // message if not defined explicitly.
  secret: 'INp8IvdIyeMcoGAgFGoA61DdBglwwSqnXJZkgz8PSnw',
  // You can generate a signing key using `jose newkey -s 512 -t oct -a HS512`
  // This gives you direct knowledge of the key used to sign the token so you can use it
  // to authenticate indirectly (eg. to a database driver)
  signingKey: {
     kty: "oct",
     kid: "Dl893BEV-iVE-x9EC52TDmlJUgGm9oZ99_ZL025Hc5Q",
     alg: "HS512",
     k: "K7QqRmJOKRK2qcCKV_pi9PSBv3XP0fpTu30TP8xn4w01xR3ZMZM38yL2DnTVPVw6e4yhdh0jtoah-i4c_pZagA"
  },
  // If you chose something other than the default algorithm for the signingKey (HS512)
  // you also need to configure the algorithm
  verificationOptions: {
     algorithms: ['HS256']
  },
  // Set to true to use encryption. Defaults to false (signing only).
  encryption: true,
  encryptionKey: "",
  // decryptionKey: encryptionKey,
  decryptionOptions: {
     algorithms: ['A256GCM']
  },
  // You can define your own encode/decode functions for signing and encryption
  // if you want to override the default behaviour.
  async encode({ secret, token, maxAge }) {},
  async decode({ secret, token, maxAge }) {},
}
```



An example JSON Web Token contains a payload like this:

JSON Web Tokenの例では、以下のようなペイロードが含まれています。

```
{
  name: 'Iain Collins',
  email: 'me@iaincollins.com',
  picture: 'https://example.com/image.jpg',
  iat: 1594601838,
  exp: 1597193838
}
```


#### JWT Helper[#](#jwt-helper "Direct link to heading")



You can use the built-in `getToken()` helper method to verify and decrypt the token, like this:

以下のように、組み込みの`getToken()`ヘルパーメソッドを使って、トークンの検証と復号化を行うことができます。


```
import jwt from "next-auth/jwt"

const secret = process.env.JWT_SECRET

export default async (req, res) => {
  const token = await jwt.getToken({ req, secret })
  console.log("JSON Web Token", token)
  res.end()
}
```




_For convenience, this helper function is also able to read and decode tokens passed in an HTTP Bearer header._


_便宜上、このヘルパー関数は、HTTP Bearerヘッダーで渡されたトークンを読み込んでデコードすることもできます。



**Required**



The getToken() helper requires the following options:



getToken()ヘルパーには、以下のオプションが必要です。



-   `req` - (object) Request object
-   `secret` - (string) JWT Secret


- `req` - (object) リクエストオブジェクト
- secret` - (string) JWTシークレット



You must also pass _any options configured on the `jwt` option_ to the helper.



また、`jwt` オプションで設定されたすべてのオプション_をヘルパーに渡す必要があります。



e.g. Including custom session `maxAge` and custom signing and/or encryption keys or options


例：カスタムセッション `maxAge` やカスタム署名・暗号化キー、オプションを含む。



**Optional**



It also supports the following options:


また、以下のオプションもサポートしています。




-   `secureCookie` - (boolean) Use secure prefixed cookie name

- secureCookie` - (boolean) 安全なプレフィックスのクッキー名を使用します。



    By default, the helper function will attempt to determine if it should use the secure prefixed cookie (e.g. `true` in production and `false` in development, unless NEXTAUTH\_URL contains an HTTPS URL).


    デフォルトでは、ヘルパー関数は、セキュアな接頭辞付きクッキーを使用すべきかどうかを判断しようとします (例: NEXTAUTH\_URL に HTTPS URL が含まれていない限り、運用環境では `true` 、開発環境では `false` となります)。



-   `cookieName` - (string) Session token cookie name

- cookieName` - (string) セッショントークンのクッキー名


    The `secureCookie` option is ignored if `cookieName` is explicitly specified.


    cookieName` が明示的に指定されている場合、`secureCookie` オプションは無視されます。




-   `raw` - (boolean) Get raw token (not decoded)


- `raw` - (boolean) 生のトークンを取得します（デコードされていません）。




    If set to `true` returns the raw token without decrypting or verifying it.


    true` に設定すると、復号化や検証を行わずに、生のトークンを返します。




##### note



The JWT is stored in the Session Token cookie, the same cookie used for tokens with database sessions.


JWTはSession Tokenクッキーに保存されます。これは、データベースセッションを持つトークンに使用されるクッキーと同じです。




___



### pages[#](#pages "Direct link to heading")



-   **Default value**: `{}`
-   **Required**: _No_



#### Description[#](#description-5 "Direct link to heading")



Specify URLs to be used if you want to create custom sign in, sign out and error pages.


カスタムのサインイン、サインアウト、エラーページを作成する場合に使用するURLを指定します。



Pages specified will override the corresponding built-in page.

指定したページは、対応する内蔵ページを上書きします。




_For example:_

_例えば以下のようになります。

```
pages: {
  signIn: '/auth/signin',
  signOut: '/auth/signout',
  error: '/auth/error', // Error code passed in query string as ?error=
  verifyRequest: '/auth/verify-request', // (used for check email message)
  newUser: '/auth/new-user' // New users will be directed here on first sign in (leave the property out if not of interest)
}
```

See the documentation for the [pages option](https://next-auth.js.org/configuration/pages) for more information.



___



### callbacks[#](#callbacks "Direct link to heading")



-   **Default value**: `object`
-   **Required**: _No_



#### Description[#](#description-6 "Direct link to heading")



Callbacks are asynchronous functions you can use to control what happens when an action is performed.


コールバックは、あるアクションが実行されたときに起こることを制御するために使用できる非同期関数です。


Callbacks are extremely powerful, especially in scenarios involving JSON Web Tokens as they allow you to implement access controls without a database and to integrate with external databases or APIs.


コールバックは非常に強力で、特にJSON Web Tokensを使用するシナリオでは、データベースなしでアクセスコントロールを実装したり、外部のデータベースやAPIと統合したりすることができます。



You can specify a handler for any of the callbacks below.



以下のいずれかのコールバックにハンドラを指定できます。


```
callbacks: {
  async signIn(user, account, profile) {
    return true
  },
  async redirect(url, baseUrl) {
    return baseUrl
  },
  async session(session, user) {
    return session
  },
  async jwt(token, user, account, profile, isNewUser) {
    return token
  }
}

```


See the [callbacks documentation](https://next-auth.js.org/configuration/callbacks) for more information on how to use the callback functions.



___



### events[#](#events "Direct link to heading")



-   **Default value**: `object`
-   **Required**: _No_



#### Description[#](#description-7 "Direct link to heading")



Events are asynchronous functions that do not return a response, they are useful for audit logging.


イベントは、応答を返さない非同期の関数で、監査ログを取るのに便利です。



You can specify a handler for any of these events below - e.g. for debugging or to create an audit log.


これらのイベントには、以下のようにハンドラーを指定することができます - 例えば、デバッグや監査ログの作成のために。



The content of the message object varies depending on the flow (e.g. OAuth or Email authentication flow, JWT or database sessions, etc). See the [events documentation](https://next-auth.js.org/configuration/events) for more information on the form of each message object and how to use the events functions.




メッセージオブジェクトの内容は、フローによって異なります（例：OAuthやEmail認証のフロー、JWTやデータベースセッションなど）。各メッセージオブジェクトの形式や、events関数の使い方については、[events documentation](https://next-auth.js.org/configuration/events)を参照してください。


```
events: {
  async signIn(message) { /* on successful sign in */ },
  async signOut(message) { /* on signout */ },
  async createUser(message) { /* user created */ },
  async updateUser(message) { /* user updated - e.g. their email was verified */ },
  async linkAccount(message) { /* account (e.g. Twitter) linked to a user */ },
  async session(message) { /* session is active */ },
  async error(message) { /* error in authentication flow */ }
}
```



___



### adapter[#](#adapter "Direct link to heading")



-   **Default value**: _Adapter.Default()_
-   **Required**: _No_



#### Description[#](#description-8 "Direct link to heading")



By default NextAuth.js uses a database adapter that uses TypeORM and supports MySQL, MariaDB, Postgres and MongoDB and SQLite databases. An alternative adapter that uses Prisma, which currently supports MySQL, MariaDB and Postgres, is also included.

NextAuth.jsのデフォルトでは、TypeORMを使用し、MySQL、MariaDB、Postgres、MongoDBとSQLiteのデータベースをサポートするデータベースアダプタを使用します。Prisma を使った代替アダプタも含まれており、現在は MySQL、MariaDB、Postgres をサポートしています。





You can use the `adapter` option to use the Prisma adapter - or pass in your own adapter if you want to use a database that is not supported by one of the built-in adapters.


また、内蔵のアダプタでサポートされていないデータベースを使用したい場合は、独自のアダプタを渡すこともできます。




See the [adapter documentation](https://next-auth.js.org/adapters/overview) for more information.



##### note



If the `adapter` option is specified it overrides the `database` option, only specify one or the other.



ただし、`adapter`オプションが指定されている場合は、`database`オプションよりも優先されるので、どちらか一方のみを指定してください。



___



### debug[#](#debug "Direct link to heading")



-   **Default value**: `false`
-   **Required**: _No_



#### Description[#](#description-9 "Direct link to heading")



Set debug to `true` to enable debug messages for authentication and database operations.



debugを`true`に設定すると、認証やデータベース操作時のデバッグメッセージが有効になります。



___



### logger[#](#logger "Direct link to heading")



-   **Default value**: `console`
-   **Required**: _No_



#### Description[#](#description-10 "Direct link to heading")



Override any of the logger levels (`undefined` levels will use the built-in logger), and intercept logs in NextAuth. You can use this to send NextAuth logs to a third-party logging service.


任意のロガーレベルをオーバーライドし（`undefined`レベルはビルトインロガーを使用します）、NextAuthのログをインターセプトします。NextAuth のログをサードパーティのロギングサービスに送信する際に使用できます。




Example:



```/pages/api/auth/\[...nextauth\].js
import log from "logging-service"

export default NextAuth({
  ...
  logger: {
    error(code, ...message) {
      log.error(code, message)
    },
    warn(code, ...message) {
      log.warn(code, message)
    },
    debug(code, ...message) {
      log.debug(code, message)
    }
  }
  ...
})

```

##### note



If the `debug` level is defined by the user, it will be called regardless of the `debug: false` [option](#debug).



ユーザーが `debug` レベルを定義している場合は、`debug: false` [オプション](#debug) に関係なく呼び出されます。



___



### theme[#](#theme "Direct link to heading")



-   **Default value**: `"auto"`
-   **Required**: _No_



#### Description[#](#description-11 "Direct link to heading")



Changes the theme of [pages](https://next-auth.js.org/configuration/pages). Set to `"light"`, if you want to force pages to always be light. Set to `"dark"`, if you want to force pages to always be dark. Set to `"auto"`, (or leave this option out) if you want the pages to follow the preferred system theme. (Uses the [prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) media query.)


[ページ](https://next-auth.js.org/configuration/pages)のテーマを変更します。light"`に設定すると、ページを常に明るい色で表示します。dark"`に設定すると、ページを常に暗い色で表示します。ページを好みのシステムテーマに従わせたい場合は、`"auto"`に設定してください（このオプションを外しても構いません）。([prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)メディアクエリを使用しています)




___



## Advanced Options[#](#advanced-options "Direct link to heading")



Advanced options are passed the same way as basic options, but may have complex implications or side effects. You should try to avoid using advanced options unless you are very comfortable using them.


高度なオプションは基本的なオプションと同じように渡されますが、複雑な意味合いや副作用を持つ場合があります。高度なオプションは、よほど使い慣れていない限り、なるべく使わないようにしましょう。



___



### useSecureCookies[#](#usesecurecookies "Direct link to heading")



-   **Default value**: `true` for HTTPS sites / `false` for HTTP sites
-   **Required**: _No_


- **デフォルト値**: HTTPSサイトでは「true」、HTTPサイトでは「false」となります。
- **必須**: _No_



#### Description[#](#description-12 "Direct link to heading")



When set to `true` (the default for all site URLs that start with `https://`) then all cookies set by NextAuth.js will only be accessible from HTTPS URLs.


`true`（`https://`で始まるすべてのサイトのURLのデフォルト）に設定すると、NextAuth.jsが設定するすべてのCookieは、HTTPSのURLからのみアクセスできるようになります。



This option defaults to `false` on URLs that start with `http://` (e.g. `http://localhost:3000`) for developer convenience.




このオプションは、開発者の利便性を考慮して、`http://`で始まるURL（例：`http://localhost:3000`）では、デフォルトで`false`となります。



You can manually set this option to `false` to disable this security feature and allow cookies to be accessible from non-secured URLs (this is not recommended).


このオプションを手動で`false`に設定することで、このセキュリティ機能を無効にして、安全でないURLからのクッキーのアクセスを可能にすることができます（これは推奨されません）。



##### note



Properties on any custom `cookies` that are specified override this option.



指定された任意のカスタム `Cookie` のプロパティは、このオプションを上書きします。



##### warning



Setting this option to _false_ in production is a security risk and may allow sessions to be hijacked if used in production. It is intended to support development and testing. 

Using this option is not recommended.


本番環境でこのオプションを_false_に設定することは、セキュリティ上のリスクがあり、本番環境で使用するとセッションが乗っ取られてしまう可能性があります。開発やテストをサポートすることを目的としています。

このオプションの使用は推奨されません。



___



### cookies[#](#cookies "Direct link to heading")



-   **Default value**: `{}`
-   **Required**: _No_



#### Description[#](#description-13 "Direct link to heading")



You can override the default cookie names and options for any of the cookies used by NextAuth.js.


NextAuth.jsが使用するすべてのCookieについて、デフォルトのCookie名とオプションを上書きすることができます。



This is an advanced option and using it is not recommended as you may break authentication or introduce security flaws into your application.

これは高度なオプションで、認証ができなくなったり、アプリケーションにセキュリティ上の欠陥が生じたりする可能性があるため、使用はお勧めできません。



You can specify one or more cookies with custom properties, but if you specify custom options for a cookie you must provide all the options for that cookie.


カスタムプロパティで1つまたは複数のクッキーを指定することができますが、あるクッキーにカスタムオプションを指定する場合は、そのクッキーのすべてのオプションを提供する必要があります。



If you use this feature, you will likely want to create conditional behaviour to support setting different cookies policies in development and production builds, as you will be opting out of the built-in dynamic policy.


この機能を使用する場合、組み込みの動的なポリシーから外れることになるので、開発ビルドと本番ビルドで異なるクッキーポリシーを設定するための条件付き動作を作成するとよいでしょう。



##### tip



An example of a use case for this option is to support sharing session tokens across subdomains.


このオプションの使用例としては、サブドメイン間でのセッショントークンの共有をサポートすることが挙げられます。



#### Example[#](#example "Direct link to heading")

```
cookies: {
  sessionToken: {
    name: `__Secure-next-auth.session-token`,
    options: {
      httpOnly: true,
      sameSite: 'lax',
      path: '/',
      secure: true
    }
  },
  callbackUrl: {
    name: `__Secure-next-auth.callback-url`,
    options: {
      sameSite: 'lax',
      path: '/',
      secure: true
    }
  },
  csrfToken: {
    name: `__Host-next-auth.csrf-token`,
    options: {
      httpOnly: true,
      sameSite: 'lax',
      path: '/',
      secure: true
    }
  },
  pkceCodeVerifier: {
    name: `${cookiePrefix}next-auth.pkce.code_verifier`,
    options: {
      httpOnly: true,
      sameSite: 'lax',
      path: '/',
      secure: useSecureCookies
    }
  }
}

```


##### warning



Using a custom cookie policy may introduce security flaws into your application and is intended as an option for advanced users who understand the implications. Using this option is not recommended.


カスタムCookieポリシーを使用すると、アプリケーションにセキュリティ上の欠陥が生じる可能性があるため、その影響を理解している上級ユーザー向けのオプションとして用意されています。このオプションの使用は推奨されません。



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/configuration/options.md)