Callbacks | NextAuth.js
https://next-auth.js.org/configuration/callbacks

# Callbacks

Callbacks are **asynchronous** functions you can use to control what happens when an action is performed.

コールバックとは、あるアクションが実行されたときに起こることを制御するために使用できる**非同期**関数です。

Callbacks are extremely powerful, especially in scenarios involving JSON Web Tokens as they allow you to implement access controls without a database and to integrate with external databases or APIs.

コールバックは非常に強力で、特に JSON Web Tokens を使ったシナリオでは、データベースを使わずにアクセスコントロールを実装したり、外部のデータベースや API と統合したりすることができます。

##### tip

If you want to pass data such as an Access Token or User ID to the browser when using JSON Web Tokens, you can persist the data in the token when the `jwt` callback is called, then pass the data through to the browser in the `session` callback.

JSON Web トークンを使用しているときに、アクセストークンやユーザー ID などのデータをブラウザに渡したい場合は、`jwt` コールバックが呼び出されたときにトークン内のデータを永続化し、`session` コールバックでデータをブラウザに渡します。

You can specify a handler for any of the callbacks below.

以下のどのコールバックに対しても、ハンドラを指定することができます。

```pages/api/auth/[...nextauth].js

...
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
...

}

```

The documentation below shows how to implement each callback, their default behaviour and an example of what the response for each callback should be. Note that configuration options and authentication providers you are using can impact the values passed to the callbacks.

以下のドキュメントでは、各コールバックの実装方法、デフォルトの動作、各コールバックのレスポンスの例を示しています。なお、設定オプションや使用している認証プロバイダによっては、コールバックに渡される値に影響が出る場合があります。

## Sign in callback[#](#sign-in-callback "Direct link to heading")

Use the `signIn()` callback to control if a user is allowed to sign in.

`signIn()`コールバックを使用して、ユーザーのサインインを許可するかどうかを制御します。

```pages/api/auth/[...nextauth].js

...
callbacks: {
  /**
   * @param  {object} user     User object
   * @param  {object} account  Provider account
   * @param  {object} profile  Provider profile
   * @return {boolean|string}  Return `true` to allow sign in
   *                           Return `false` to deny access
   *                           Return `string` to redirect to (eg.: "/unauthorized")
   */
  async signIn(user, account, profile) {
    const isAllowedToSignIn = true
    if (isAllowedToSignIn) {
      return true
    } else {
      // Return false to display a default error message
      return false
      // Or you can return a URL to redirect to:
      // return '/unauthorized'
    }
  }
}
...

```

- When using the **Email Provider** the `signIn()` callback is triggered both when the user makes a **Verification Request** (before they are sent email with a link that will allow them to sign in) and again _after_ they activate the link in the sign in email.

- **Email Provider**を使用する場合、`signIn()`コールバックは、ユーザーが**Verification Request**を行った時（サインインを可能にするリンクを含むメールが送られる前）と、サインインメールのリンクを有効にした後の両方でトリガされます。

  Email accounts do not have profiles in the same way OAuth accounts do. On the first call during email sign in the `profile` object will include a property `verificationRequest: true` to indicate it is being triggered in the verification request flow. When the callback is invoked _after_ a user has clicked on a sign in link, this property will not be present.

  メールアカウントは、OAuth アカウントのようなプロファイルを持ちません。E メールでのサインイン時の最初の呼び出しで、`profile`オブジェクトは、検証リクエストフローの中でトリガーされていることを示すために、`verificationRequest: true`というプロパティを含みます。ユーザーがサインインリンクをクリックした後にコールバックが呼び出された場合、このプロパティは存在しません。

  You can check for the `verificationRequest` property to avoid sending emails to addresses or domains on a blocklist (or to only explicitly generate them for email address in an allow list).

  ブロックリストに登録されているアドレスやドメインにメールを送信しないようにするために（あるいは、許可リストに登録されているメールアドレスに対してのみメールを明示的に生成するために）、`verificationRequest` プロパティをチェックすることができます。

- When using the **Credentials Provider** the `user` object is the response returned from the `authorize` callback and the `profile` object is the raw body of the `HTTP POST` submission.

- **Credentials Provider** を使用する場合、`user` オブジェクトは `authorize` コールバックから返されたレスポンスで、`profile` オブジェクトは `HTTP POST` 送信の生のボディです。

##### note

When using NextAuth.js with a database, the User object will be either a user object from the database (including the User ID) if the user has signed in before or a simpler prototype user object (i.e. name, email, image) for users who have not signed in before.

NextAuth.js をデータベースと一緒に使う場合、User オブジェクトは、ユーザーが以前にサインインしたことがある場合にはデータベースからのユーザーオブジェクト (ユーザー ID を含む) になり、以前にサインインしたことがないユーザーの場合には、よりシンプルなプロトタイプのユーザーオブジェクト (名前、メール、画像など) になります。

When using NextAuth.js without a database, the user object it will always be a prototype user object, with information extracted from the profile.

NextAuth.js をデータベースなしで使用する場合、ユーザーオブジェクトは常にプロファイルから抽出された情報を持つプロトタイプユーザーオブジェクトとなります。

##### note

Redirects returned by this callback cancel the authentication flow. Only redirect to error pages that, for example, tell the user why they're not allowed to sign in.

このコールバックが返すリダイレクトは、認証フローをキャンセルします。サインインできない理由をユーザーに伝えるなどのエラーページにのみリダイレクトします。

To redirect to a page after a successful sign in, please use [the `callbackUrl` option](https://next-auth.js.org/getting-started/client#specifying-a-callbackurl) or [the redirect callback](https://next-auth.js.org/configuration/callbacks#redirect-callback).

サインインに成功した後のページにリダイレクトするには、[the `callbackUrl` option](https://next-auth.js.org/getting-started/client#specifying-a-callbackurl)または[the redirect callback](https://next-auth.js.org/configuration/callbacks#redirect-callback)をご利用ください。

## Redirect callback[#](#redirect-callback "Direct link to heading")

The redirect callback is called anytime the user is redirected to a callback URL (e.g. on signin or signout).

リダイレクトコールバックは、ユーザーがコールバック URL にリダイレクトされるたびに呼び出されます(例：サインイン時やサインアウト時)。

By default only URLs on the same URL as the site are allowed, you can use the redirect callback to customise that behaviour.

デフォルトでは、サイトと同じ URL のみが許可されますが、リダイレクトコールバックを使用してその動作をカスタマイズすることができます。

```pages/api/auth/[...nextauth].js

...
callbacks: {
  /**
   * @param  {string} url      URL provided as callback URL by the client
   * @param  {string} baseUrl  Default base URL of site (can be used as fallback)
   * @return {string}          URL the client will be redirect to
   */
  async redirect(url, baseUrl) {
    return url.startsWith(baseUrl)
      ? url
      : baseUrl
  }
}
...

```

##### note

The redirect callback may be invoked more than once in the same flow.

リダイレクトコールバックは、同一フロー内で複数回起動することができます。

## JWT callback[#](#jwt-callback "Direct link to heading")

This JSON Web Token callback is called whenever a JSON Web Token is created (i.e. at sign in) or updated (i.e whenever a session is accessed in the client).

この JSON Web Token コールバックは、JSON Web Token が作成されたとき（すなわちサインイン時）や更新されたとき（すなわちクライアントでセッションにアクセスされたとき）に呼び出されます。

e.g. `/api/auth/signin`, `getSession()`, `useSession()`, `/api/auth/session`

- As with database session expiry times, token expiry time is extended whenever a session is active.
- The arguments _user_, _account_, _profile_ and _isNewUser_ are only passed the first time this callback is called on a new session, after the user signs in.

- データベースのセッションの有効期限と同様に、トークンの有効期限は、セッションがアクティブなときは常に延長されます。
- 引数*user*, _account_, _profile_, *isNewUser*は、ユーザーがサインインした後、新しいセッションで初めてこのコールバックが呼ばれたときにのみ渡されます。

The contents _user_, _account_, _profile_ and _isNewUser_ will vary depending on the provider and on if you are using a database or not. If you want to pass data such as User ID, OAuth Access Token, etc. to the browser, you can persist it in the token and use the `session()` callback to return it.

_user_, _account_, _profile_, *isNewUser*の内容は、プロバイダや、データベースを使用しているかどうかによって異なります。ユーザー ID や OAuth アクセストークンなどのデータをブラウザに渡したい場合は、トークンに永続化させ、`session()`コールバックを使って返します。

```pages/api/auth/[...nextauth].js

...
callbacks: {
  /**
   * @param  {object}  token     Decrypted JSON Web Token
   * @param  {object}  user      User object      (only available on sign in)
   * @param  {object}  account   Provider account (only available on sign in)
   * @param  {object}  profile   Provider profile (only available on sign in)
   * @param  {boolean} isNewUser True if new user (only available on sign in)
   * @return {object}            JSON Web Token that will be saved
   */
  async jwt(token, user, account, profile, isNewUser) {
    // Add access_token to the token right after signin
    if (account?.accessToken) {
      token.accessToken = account.accessToken
    }
    return token
  }
}
...


```

##### tip

Use an if branch in jwt with checking for existence of any other params than token. If any of those exist, you call jwt for the first time. This is a good place to add for example an `access_token` to your jwt, if you want to.

jwt では、token 以外のパラメータの存在をチェックする if 分岐を使用します。これらのパラメータが存在する場合、初めて jwt を呼び出します。必要であれば、jwt に`access_token`などを追加するのに適した場所です。

##### tip

Check out the content of all the params in addition `token`, to see what info you have available on signin.

サインイン時に利用できる情報を確認するために、`token`に加えて、すべてのパラメータの内容をチェックしてください。

##### warning

NextAuth.js does not limit how much data you can store in a JSON Web Token, however a ~**4096 byte limit** per cookie is commonly imposed by browsers.

NextAuth.js は JSON Web Token に保存できるデータ量を制限していませんが、ブラウザでは一般的にクッキーあたり ~**4096 バイトの制限** が課せられています。

If you need to persist a large amount of data, you will need to persist it elsewhere (e.g. in a database). A common solution is to store a key in the cookie that can be used to look up the remaining data in the database, for example, in the `session()` callback.

大量のデータを永続化する必要がある場合は、別の場所（データベースなど）に永続化する必要があります。一般的な解決策は、データベース内の残りのデータを検索するのに使用できるキーをクッキーに保存することです。例えば、`session()`のコールバックで使用します。

## Session callback[#](#session-callback "Direct link to heading")

The session callback is called whenever a session is checked. By default, only a subset of the token is returned for increased security. If you want to make something available you added to the token through the `jwt()` callback, you have to explicitly forward it here to make it available to the client.

セッションコールバックは、セッションがチェックされるたびに呼び出されます。デフォルトでは、セキュリティ強化のため、トークンのサブセットのみが返されます。jwt()`コールバックでトークンに追加したものを利用可能にしたい場合は、クライアントがそれを利用できるようにするために、ここに明示的に転送する必要があります。

e.g. `getSession()`, `useSession()`, `/api/auth/session`

- When using database sessions, the User object is passed as an argument.
- When using JSON Web Tokens for sessions, the JWT payload is provided instead.

- データベースセッションを使用する場合は、User オブジェクトが引数として渡されます。
- セッションに JSON Web Tokens を使用する場合は、代わりに JWT ペイロードが提供されます。

```
...
callbacks: {
  /**
   * @param  {object} session      Session object
   * @param  {object} token        User object    (if using database sessions)
   *                               JSON Web Token (if not using database sessions)
   * @return {object}              Session that will be returned to the client
   */
  async session(session, token) {
    // Add property to session, like an access_token from a provider.
    session.accessToken = token.accessToken
    return session
  }
}
...

```

##### tip

When using JSON Web Tokens the `jwt()` callback is invoked before the `session()` callback, so anything you add to the JSON Web Token will be immediately available in the session callback, like for example an `access_token` from a provider.

JSON Web Token を使用する場合、`jwt()` コールバックは `session()` コールバックの前に呼び出されるので、JSON Web Token に追加したものは、例えばプロバイダからの `access_token` のように、すぐにセッションコールバックで利用できます。

##### tip

To better represent its value, when using a JWT session, the second parameter should be called `token` (This is the same thing you return from the `jwt()` callback). If you use a database, call it `user`.

JWT セッションを使用する場合、その値をよりよく表現するために、2 番目のパラメータは`token`と呼ぶべきです（これは、`jwt()`コールバックから返されるものと同じです）。データベースを使用している場合は、`user`と呼びます。

##### warning

The session object is not persisted server side, even when using database sessions - only data such as the session token, the user, and the expiry time is stored in the session table.

データベースセッションを使用している場合でも、セッションオブジェクトはサーバー側で永続化されません。セッショントークン、ユーザー、有効期限などのデータのみがセッションテーブルに保存されます。

If you need to persist session data server side, you can use the `accessToken` returned for the session as a key - and connect to the database in the `session()` callback to access it. Session `accessToken` values do not rotate and are valid as long as the session is valid.

セッションデータをサーバーサイドに保存する必要がある場合は、セッションに対して返される `accessToken` をキーにして、`session()` コールバックでデータベースに接続してアクセスすることができます。セッションの `accessToken` の値は回転せず、セッションが有効である限り、有効です。

If using JSON Web Tokens instead of database sessions, you should use the User ID or a unique key stored in the token (you will need to generate a key for this yourself on sign in, as access tokens for sessions are not generated when using JSON Web Tokens).

データベースセッションの代わりに JSON Web Tokens を使用する場合は、ユーザー ID またはトークンに格納されている一意のキーを使用する必要があります（JSON Web Tokens を使用する場合、セッション用のアクセストークンは生成されないため、サインイン時にこのためのキーを自分で生成する必要があります）。

[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/configuration/callbacks.md)
