Errors | NextAuth.js
https://next-auth.js.org/errors




# Errors



This is a list of errors output from NextAuth.js.


これはNextAuth.jsから出力されるエラーのリストです。




All errors indicate an unexpected problem, you should not expect to see errors.


すべてのエラーは予期せぬ問題を示しており、エラーが表示されることを期待してはいけません。




If you are seeing any of these errors in the console, something is wrong.



コンソールにこれらのエラーのいずれかが表示されている場合、何かが間違っています。




___



## Client[#](#client "Direct link to heading")



These errors are returned from the client. As the client is [Universal JavaScript (or "Isomorphic JavaScript")](https://en.wikipedia.org/wiki/Isomorphic_JavaScript) it can be run on the client or server, so these errors can occur in both in the terminal and in the browser console.


これらのエラーは、クライアントから返されます。クライアントは[Universal JavaScript (またはIsomorphic JavaScript)](https://en.wikipedia.org/wiki/Isomorphic_JavaScript)であるため、クライアントでもサーバーでも実行することができ、これらのエラーはターミナルでもブラウザのコンソールでも発生します。

### CLIENT_USE_SESSION_ERROR

This error occurs when the `useSession()` React Hook has a problem fetching session data.



このエラーは、`useSession()` React Hookがセッションデータの取得に問題がある場合に発生します。

### CLIENT_FETCH_ERROR



If you see `CLIENT_FETCH_ERROR` make sure you have configured the `NEXTAUTH_URL` environment variable.


CLIENT_FETCH_ERROR`が表示された場合は、環境変数`NEXTAUTH_URL`が設定されていることを確認してください。




___



## Server[#](#server "Direct link to heading")



These errors are displayed on the terminal.


これらのエラーはターミナルに表示されます。

### OAuth

### OAUTH_GET_ACCESS_TOKEN_ERROR#
### OAUTH_V1_GET_ACCESS_TOKEN_ERROR#
### OAUTH_GET_PROFILE_ERROR#
### OAUTH_PARSE_PROFILE_ERROR#
### OAUTH_CALLBACK_HANDLER_ERROR#



___

### Signin / Callback#

### GET_AUTHORIZATION_URL_ERROR#
### SIGNIN_OAUTH_ERROR#
### CALLBACK_OAUTH_ERROR#
### SIGNIN_EMAIL_ERROR#
### CALLBACK_EMAIL_ERROR#
### EMAIL_REQUIRES_ADAPTER_ERROR#

The Email authentication provider can only be used if a database is configured.

Email認証プロバイダは、データベースが構成されている場合にのみ使用できます。

### CALLBACK_CREDENTIALS_JWT_ERROR#

The Credentials Provider can only be used if JSON Web Tokens are used for sessions.

資格情報プロバイダーは、セッションにJSON Web Tokensを使用する場合にのみ使用できます。


JSON Web Tokens are used for Sessions by default if you have not specified a database. However if you are using a database, then Database Sessions are enabled by default and you need to [explicitly enable JWT Sessions](https://next-auth.js.org/configuration/options#session) to use the Credentials Provider.


データベースを指定していない場合は、デフォルトでJSON Web Tokensがセッションに使用されます。ただし、データベースを使用している場合は、デフォルトでDatabase Sessionsが有効になっており、クレデンシャル・プロバイダを使用するには[JWT Sessionsを明示的に有効にする](https://next-auth.js.org/configuration/options#session)必要があります。



If you are using a Credentials Provider, NextAuth.js will not persist users or sessions in a database - user accounts used with the Credentials Provider must be created and managed outside of NextAuth.js.



資格情報プロバイダーを使用する場合、NextAuth.jsはユーザーやセッションをデータベースに保存しません。資格情報プロバイダーで使用するユーザーアカウントは、NextAuth.jsの外部で作成・管理する必要があります。



In _most cases_ it does not make sense to specify a database in NextAuth.js options and support a Credentials Provider.


ほとんどの場合、NextAuth.js のオプションでデータベースを指定し、クレデンシャル プロバイダをサポートすることは意味がありません。


### CALLBACK_CREDENTIALS_HANDLER_ERROR

### PKCE_ERROR

The provider you tried to use failed when setting [PKCE or Proof Key for Code Exchange](https://tools.ietf.org/html/rfc7636#section-4.2). The `code_verifier` is saved in a cookie called (by default) `__Secure-next-auth.pkce.code_verifier` which expires after 15 minutes. Check if `cookies.pkceCodeVerifier` is configured correctly. The default `code_challenge_method` is `"S256"`. This is currently not configurable to `"plain"`, as it is not recommended, and in most cases it is only supported for backward compatibility.


PKCE または Proof Key for Code Exchange](https://tools.ietf.org/html/rfc7636#section-4.2)の設定で、使おうとしたプロバイダーが失敗しました。`code_verifier`は（デフォルトでは）`__Secure-next-auth.pkce.code_verifier`というクッキーに保存され、15分後に失効します。`cookies.pkceCodeVerifier` が正しく設定されているかどうかを確認してください。デフォルトの `code_challenge_method` は `"S256"` です。これは推奨されておらず、ほとんどの場合、後方互換性のためにのみサポートされているため、現在のところ `"plain"` に設定することはできません。


___



### Session Handling[#](#session-handling "Direct link to heading")


### JWT_SESSION_ERROR


[https://next-auth.js.org/errors#jwt\_session\_error](https://next-auth.js.org/errors#jwt_session_error) JWKKeySupport: the key does not support HS512 verify algorithm



The algorithm used for generating your key isn't listed as supported. You can generate a HS512 key using



鍵の生成に使用されたアルゴリズムがサポートされていないと表示されています。HS512 の鍵は以下の方法で生成できます。

```
jose newkey -s 512 -t oct -a HS512

```



If you are unable to use an HS512 key (for example to interoperate with other services) you can define what is supported using


HS512 キーを使用できない場合（他のサービスとの相互運用など）、以下の方法でサポート対象を定義できます。


```
  jwt: {
    signingKey: {"kty":"oct","kid":"--","alg":"HS256","k":"--"},
    verificationOptions: {
      algorithms: ["HS256"]
    }
  }

```



#### SESSION_ERROR[#](#session_error "Direct link to heading")



___



### Signout[#](#signout "Direct link to heading")

### SIGNOUT_ERROR


___



### Database[#](#database "Direct link to heading")



These errors are logged by the TypeORM Adapter, which is the default database adapter.


これらのエラーは、デフォルトのデータベースアダプタであるTypeORMアダプタによって記録されます。



They all indicate a problem interacting with the database.


これらはすべて、データベースとのやりとりに問題があることを示しています。

### ADAPTER_CONNECTION_ERROR#
### CREATE_USER_ERROR#
### GET_USER_BY_ID_ERROR#
### GET_USER_BY_EMAIL_ERROR#
### GET_USER_BY_PROVIDER_ACCOUNT_ID_ERROR#
### LINK_ACCOUNT_ERROR#
### CREATE_SESSION_ERROR#
### GET_SESSION_ERROR#
### UPDATE_SESSION_ERROR#
### DELETE_SESSION_ERROR#
### CREATE_VERIFICATION_REQUEST_ERROR#
### GET_VERIFICATION_REQUEST_ERROR#
### DELETE_VERIFICATION_REQUEST_ERROR#

___



### Other[#](#other "Direct link to heading")


### SEND_VERIFICATION_EMAIL_ERROR#



This error occurs when the Email Authentication Provider is unable to send an email.



このエラーは、メール認証プロバイダがメールを送信できない場合に発生します。



Check your mail server configuration.


メールサーバーの設定を確認してください。



### MISSING_NEXTAUTH_API_ROUTE_ERROR

This error happens when `[...nextauth].js` file is not found inside `pages/api/auth`.



このエラーは、`[...nextauth].js`ファイルが`pages/api/auth`内で見つからない場合に発生します。



Make sure the file is there and the filename is written correctly.



ファイルが存在し、ファイル名が正しく書かれていることを確認してください。




[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/errors.md)







