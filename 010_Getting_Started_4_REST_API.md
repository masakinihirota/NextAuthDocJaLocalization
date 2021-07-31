REST API | NextAuth.js
https://next-auth.js.org/getting-started/rest-api




# REST API



NextAuth.js exposes a REST API which is used by the NextAuth.js client.


NextAuth.js は、NextAuth.js クライアントが使用する REST API を公開しています。




#### `GET` /api/auth/signin[#](#get-apiauthsignin "Direct link to heading")



Displays the sign in page.

サインインページを表示します。



#### `POST` /api/auth/signin/:provider[#](#post-apiauthsigninprovider "Direct link to heading")



Starts an OAuth signin flow for the specified provider.


指定したプロバイダーのOAuthサインインフローを開始します。



The POST submission requires CSRF token from `/api/auth/csrf`.


POSTの送信には、`/api/auth/csrf`からのCSRFトークンが必要です。




#### `GET` /api/auth/callback/:provider[#](#get-apiauthcallbackprovider "Direct link to heading")



Handles returning requests from OAuth services during sign in.



サインイン時にOAuthサービスからのリクエストを返す処理を行います。


For OAuth 2.0 providers that support the `state` option, the value of the `state` parameter is checked against the one that was generated when the sign in flow was started - this uses a hash of the CSRF token which MUST match for both the POST and `GET` calls during sign in.


`state` オプションをサポートしている OAuth 2.0 プロバイダーの場合、`state` パラメータの値は、サインインフローが開始されたときに生成されたものと照合されます。これには CSRF トークンのハッシュが使われ、サインイン中の POST と `GET` の両方のコールで一致しなければなりません。



#### `GET` /api/auth/signout[#](#get-apiauthsignout "Direct link to heading")



Displays the sign out page.


サインアウトのページを表示します。




#### `POST` /api/auth/signout[#](#post-apiauthsignout "Direct link to heading")



Handles signing out - this is a `POST` submission to prevent malicious links from triggering signing a user out without their consent.


サインアウトを処理します。これは、悪意のあるリンクがユーザーの同意なしにサインアウトを誘発するのを防ぐための `POST` 送信です。



The `POST` submission requires CSRF token from `/api/auth/csrf`.


`POST`の送信には、`/api/auth/csrf`のCSRFトークンが必要です。



#### `GET` /api/auth/session[#](#get-apiauthsession "Direct link to heading")



Returns client-safe session object - or an empty object if there is no session.



クライアントが安全なセッションオブジェクトを返します - セッションがない場合は空のオブジェクトを返します。




The contents of the session object that is returned are configurable with the session callback.



返されたセッションオブジェクトの内容は、セッションコールバックで設定できます。



#### `GET` /api/auth/csrf[#](#get-apiauthcsrf "Direct link to heading")



Returns object containing CSRF token. In NextAuth.js, CSRF protection is present on all authentication routes. It uses the "double submit cookie method", which uses a signed HttpOnly, host-only cookie.



CSRFトークンを含むオブジェクトを返します。NextAuth.jsでは、すべての認証ルートにCSRF対策が施されています。これは「ダブルサブミットクッキー方式」を採用しており、署名入りのHttpOnly、ホストオンリーのクッキーを使用しています。


The CSRF token returned by this endpoint must be passed as form variable named `csrfToken` in all `POST` submissions to any API endpoint.

このエンドポイントが返すCSRFトークンは、任意のAPIエンドポイントへのすべての`POST`送信において、`csrfToken`という名前のフォーム変数として渡す必要があります。





#### `GET` /api/auth/providers[#](#get-apiauthproviders "Direct link to heading")



Returns a list of configured OAuth services and details (e.g. sign in and callback URLs) for each service.



設定されたOAuthサービスのリストと、各サービスの詳細（サインインやコールバックURLなど）を返します。



It can be used to dynamically generate custom sign up pages and to check what callback URLs are configured for each OAuth provider that is configured.


カスタムサインアップページを動的に生成したり、設定されている各OAuthプロバイダにどのようなコールバックURLが設定されているかを確認したりするのに使用できます。



___



##### note



The default base path is `/api/auth` but it is configurable by specifying a custom path in `NEXTAUTH_URL`


デフォルトのベースパスは `/api/auth` ですが、`NEXTAUTH_URL` にカスタムパスを指定することで設定可能です。



e.g.



`NEXTAUTH_URL=https://example.com/myapp/api/authentication`



`/api/auth/signin` -> `/myapp/api/authentication/signin`



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/getting-started/rest-api.md)