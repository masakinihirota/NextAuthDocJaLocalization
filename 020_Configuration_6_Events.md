Events | NextAuth.js
https://next-auth.js.org/configuration/events




# Events



Events are asynchronous functions that do not return a response, they are useful for audit logs / reporting.


イベントはレスポンスを返さない非同期の関数で、監査ログやレポート作成に役立ちます。



You can specify a handler for any of these events below, for debugging or for an audit log.


デバッグや監査ログのために、以下のイベントのハンドラを指定することができます。



##### note



Execution of your auth API will be blocked by an `await` on your event handler. If your event handler starts any burdensome work it should not block its own promise on that work.


auth APIの実行は、イベントハンドラの `await` によってブロックされます。イベントハンドラーが負荷のかかる作業を開始する場合、その作業に関する自分の約束をブロックしてはいけません。



## Events[#](#events "Direct link to heading")



### signIn[#](#signin "Direct link to heading")



Sent on successful sign in.


サインインに成功したときに送信されます。



The message will be an object and contain:


メッセージはオブジェクトで、以下の内容を含みます。



-   `user` (from your adapter or from the provider if a `credentials` type provider)
-   `account` (from your adapter or the provider)
-   `isNewUser` (whether your adapter had a user for this account already)


- user` (お使いのアダプタから、または `credentials` タイプのプロバイダの場合はプロバイダから)
- account` (お客様のアダプタまたはプロバイダから)
- isNewUser` (アダプタが既にこのアカウントのユーザーを持っているかどうか)



### signOut[#](#signout "Direct link to heading")



Sent when the user signs out.


ユーザーがサインアウトしたときに送信されます。



The message object is the JWT, if using them, or the adapter session object for the session that is being ended.


メッセージオブジェクトは、JWT を使用している場合は JWT、終了するセッションのアダプタセッションオブジェクトです。



### createUser[#](#createuser "Direct link to heading")



Sent when the adapter is told to create a new user.



アダプタが新しいユーザを作成するように指示されたときに送信されます。



The message object will be the user.


メッセージオブジェクトはユーザーになります。



### updateUser[#](#updateuser "Direct link to heading")



Sent when the adapter is told to update an existing user. Currently this is only sent when the user verifies their email address.



既存のユーザーを更新するようアダプタに指示したときに送信されます。現在は、ユーザーがメールアドレスを確認した場合にのみ送信されます。




The message object will be the user.


メッセージオブジェクトはユーザーになります。




### linkAccount[#](#linkaccount "Direct link to heading")



Sent when an account in a given provider is linked to a user in our userbase. For example, when a user signs up with Twitter or when an existing user links their Google account.


特定のプロバイダーのアカウントが、ユーザーベースのユーザーにリンクされたときに送信されます。例えば、ユーザーがTwitterに登録したときや、既存のユーザーがGoogleアカウントをリンクしたときなどです。




The message will be an object and contain:


メッセージはオブジェクトで、次の内容を含みます。


-   `user`: The user object from your adapter
-   `providerAccount`: The object returned from the provider.


- `user`: アダプタから取得したユーザオブジェクト
- `providerAccount`: プロバイダから返されるオブジェクトです。


### session[#](#session "Direct link to heading")



Sent at the end of a request for the current session.



現在のセッションに対するリクエストの最後に送信されます。


The message will be an object and contain:



メッセージはオブジェクトで、以下の内容を含みます。




-   `session`: The session object from your adapter
-   `jwt`: If using JWT, the token for this session.



- `session`: アダプタからのセッションオブジェクト
- `jwt`: JWTを使用している場合は、このセッションのトークンです。




### error[#](#error "Direct link to heading")



Sent when an error occurs


エラーが発生したときに送信されます。




The message could be any object relevant to describing the error.


メッセージには、エラーの説明に関連する任意のオブジェクトを指定できます。


[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/configuration/events.md)