Models | NextAuth.js
https://next-auth.js.org/adapters/models




# Models



Models in NextAuth.js are built for ANSI SQL but are polymorphic and are transformed to adapt to the database being used; there is some variance in specific data types (e.g. for datetime, text fields, etc) but they are functionally the same with as much parity in behaviour as possible.


NextAuth.js のモデルは ANSI SQL 用に作成されていますが、多義性があり、使用するデータベースに合わせて変換されます。特定のデータ型 (datetime やテキストフィールドなど) には多少の違いがありますが、機能的には同じで、できるだけ同じ動作をするようになっています。




All table/collection names in the built in models are plural, and all table names and column names use `snake_case` when used with an SQL database and `camelCase` when used with Document database.

組み込みモデルのテーブル/コレクション名はすべて複数形で、すべてのテーブル名とカラム名は、SQLデータベースで使用する場合は`snake_case`、Documentデータベースで使用する場合は`camelCase`を使用しています。



##### note



You can [extend the built in models](https://next-auth.js.org/tutorials/typeorm-custom-models) and even [create your own database adapter](https://next-auth.js.org/tutorials/creating-a-database-adapter) if you want to use NextAuth.js with a database that is not supported out of the box.



NextAuth.js をサポートされていないデータベースで使用したい場合は、[組み込みモデルの拡張](https://next-auth.js.org/tutorials/typeorm-custom-models)や [独自のデータベースアダプターの作成](https://next-auth.js.org/tutorials/creating-a-database-adapter)も可能です。




___



## User[#](#user "Direct link to heading")



Table: `users`



**Description:**



The User model is for information such as the users name and email address.

Userモデルには、ユーザーの名前やメールアドレスなどの情報が入ります。



Email address are optional, but if one is specified for a User then it must be unique.


メールアドレスは任意ですが、ユーザーに指定する場合は、一意でなければなりません。



##### note



If a user first signs in with OAuth then their email address is automatically populated using the one from their OAuth profile, if the OAuth provider returns one.



ユーザーが最初にOAuthでサインインしたとき、OAuthプロバイダがメールアドレスを返していれば、そのメールアドレスはOAuthプロファイルのものを使って自動的に入力されます。



This provides a way to contact users and for users to maintain access to their account and sign in using email in the event they are unable to sign in with the OAuth provider in future (if email sign in is configured).


これは、ユーザーに連絡を取るための方法であり、ユーザーが将来OAuthプロバイダでサインインできなくなった場合に、アカウントへのアクセスを維持し、電子メールを使ってサインインするためのものです（電子メールによるサインインが設定されている場合）。



## Account[#](#account "Direct link to heading")



Table: `accounts`



**Description:**



The Account model is for information about OAuth accounts associated with a User.


Account モデルは、User に関連付けられた OAuth アカウントに関する情報です。



A single User can have multiple Accounts, each Account can only have one User.

1人のユーザーは複数のAccountを持つことができますが、各Accountは1人のユーザーしか持つことができません。



## Session[#](#session "Direct link to heading")



Table: `sessions`



**Description:**



The Session model is used for database sessions. It is not used if JSON Web Tokens are enabled.


Sessionモデルはデータベースのセッションに使用されます。JSON Web Tokensが有効な場合は使用されません。



A single User can have multiple Sessions, each Session can only have one User.

1人のユーザーは複数のセッションを持つことができますが、各セッションは1人のユーザーしか持つことができません。



## Verification Request[#](#verification-request "Direct link to heading")



Table: `verification_requests`



**Description:**



The Verification Request model is used to store tokens for passwordless sign in emails.


検証リクエストモデルは、パスワードなしでサインインするメールのトークンを保存するために使用されます。



A single User can have multiple open Verification Requests (e.g. to sign in to different devices).


1人のユーザーが複数の検証リクエストを持つことができます（例：異なるデバイスにサインインするため）。



It has been designed to be extendable for other verification purposes in future (e.g. 2FA / short codes).



将来的には、他の認証目的（2FAやショートコードなど）にも拡張できるように設計されています。



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/adapters/models.md)
