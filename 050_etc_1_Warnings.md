Warnings | NextAuth.js
https://next-auth.js.org/warnings





# Warnings



This is a list of warning output from NextAuth.js.


NextAuth.js から出力される警告の一覧です。



All warnings indicate things which you should take a look at, but do not inhibit normal operation.


すべての警告は、注意すべき点を示していますが、正常な動作を妨げるものではありません。



___



## Client[#](#client "Direct link to heading")



#### NEXTAUTH\_URL[#](#nextauth_url "Direct link to heading")



Environment variable `NEXTAUTH_URL` missing. Please set it in your `.env` file.


環境変数 `NEXTAUTH_URL` がありません。.env "ファイルで設定してください。



___



## Server[#](#server "Direct link to heading")



These warnings are displayed on the terminal.


このような警告がターミナルに表示されます。


#### JWT_AUTO_GENERATED_SIGNING_KEY[#](#jwt_auto_generated_signing_key "Direct link to heading")



To remedy this warning, you can either:


この警告を改善するには、以下のいずれかの方法があります。



**Option 1**: Pass a pre-regenerated Private Key (and, optionally a Public Key) in the jwt options.


**オプション1**: オプション1**: 事前に生成された秘密鍵（および、任意で公開鍵）をjwtオプションで渡す。


```/pages/api/auth/[...nextauth].js
jwt: {
  signingKey: process.env.JWT_SIGNING_PRIVATE_KEY,

  // You can also specify a public key for verification if using public/private key (but private only is fine)
  // verificationKey: process.env.JWT_SIGNING_PUBLIC_KEY,

  // If you want to use some key format other than HS512 you can specify custom options to use
  // when verifying (note: verificationOptions should include a value for maxTokenAge as well).
  // verificationOptions = {
  //   maxTokenAge: `${maxAge}s`, // e.g. `${30 * 24 * 60 * 60}s` = 30 days
  //   algorithms: ['HS512']
  // },
}
```




You can use [node-jose-tools](https://www.npmjs.com/package/node-jose-tools) to generate keys on the command line and set them as environment variables, i.e. `jose newkey -s 256 -t oct -a HS512`.


jose newkey -s 256 -t oct -a HS512`のように、[node-jose-tools](https://www.npmjs.com/package/node-jose-tools)を使って、コマンドラインで鍵を生成し、環境変数として設定することができます。




**Option 2**: Specify custom encode/decode functions on the jwt object. This gives you complete control over signing / verification / etc.


**オプション2**: jwtオブジェクトにカスタムエンコード/デコード関数を指定します。これにより、署名/検証などを完全にコントロールすることができます。



#### JWT_AUTO_GENERATED_ENCRYPTION_KEY[#](#jwt_auto_generated_encryption_key "Direct link to heading")



#### SIGNIN\_CALLBACK\_REJECT\_REDIRECT[#](#signin_callback_reject_redirect "Direct link to heading")



You returned something in the `signIn` callback, that is being deprecated.



あなたは `signIn` コールバックの中で、廃止されようとしている何かを返しました。



You probably had something similar in the callback:


おそらくコールバックの中に似たようなものがあったのではないでしょうか。


```
return Promise.reject("/some/url")

```

or


```
throw "/some/url"

```

To remedy this, simply return the url instead:


これを解決するには、単純に代わりにURLを返します。



```
return "/some/url"
```




#### STATE\_OPTION\_DEPRECATION[#](#state_option_deprecation "Direct link to heading")



You provided `state: true` or `state: false` as a provider option. This is being deprecated in a later release in favour of `protection: "state"` and `protection: "none"` respectively. To remedy this warning:


プロバイダのオプションとして、`state: true`または`state: false`が指定されています。これは後のリリースで非推奨となり、`protection: 「state"`と`protection: 「none"`となります。この警告を修正します。



-   If you use `state: true`, just simply remove it. The default is `protection: "state"` already..
-   If you use `state: false`, set `protection: "none"`.


- state: true` を使用している場合は、単にそれを削除してください。デフォルトでは `protection: "state"`がすでに使用されています。
- state: false` を使用している場合は、`protection: "none"` を設定してください。"none"`を設定してください。




[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/warnings.md)

