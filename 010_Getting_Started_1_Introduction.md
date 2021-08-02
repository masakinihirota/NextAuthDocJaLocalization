Introduction | NextAuth.js
https://next-auth.js.org/getting-started/introduction

# Introduction

# はじめに

## About NextAuth.js[#](#about-nextauthjs "Direct link to heading")

## NextAuth.js について[#](#about-nextauthjs "Direct link to heading")

NextAuth.js is a complete open source authentication solution for [Next.js](http://nextjs.org/) applications.

NextAuth.js は、[Next.js](http://nextjs.org/)アプリケーションのための完全なオープンソースの認証ソリューションです。

It is designed from the ground up to support Next.js and Serverless.

Next.js と Serverless をサポートするために、ゼロから設計されています。

[Check out the example code](https://next-auth.js.org/getting-started/example) to see how easy it is to use NextAuth.js for authentication.

[Check out the example code](https://next-auth.js.org/getting-started/example)で、NextAuth.js を使った認証がどれほど簡単かを確認できます。

### Flexible and easy to use[#](#flexible-and-easy-to-use "Direct link to heading")

### 柔軟で簡単に使える[#](#柔軟で簡単に使える「Direct link to heading」)

- Designed to work with any OAuth service, it supports OAuth 1.0, 1.0A and 2.0
- Built-in support for [many popular sign-in services](https://next-auth.js.org/configuration/providers)
- Supports email / passwordless authentication
- Supports stateless authentication with any backend (Active Directory, LDAP, etc)
- Supports both JSON Web Tokens and database sessions
- Designed for Serverless but runs anywhere (AWS Lambda, Docker, Heroku, etc…)

- どのような OAuth サービスでも動作するように設計されており、OAuth 1.0、1.0A、2.0 をサポートしている
- [多くの一般的なサインインサービス](https://next-auth.js.org/configuration/providers)をサポートしています。
- 電子メール／パスワードレス認証をサポート
- あらゆるバックエンド（Active Directory、LDAP など）とのステートレス認証に対応
- JSON Web トークンとデータベースセッションの両方をサポート
- サーバーレスのために設計されていますが、どこでも動作します (AWS Lambda, Docker, Heroku, etc..)

### Own your own data[#](#own-your-own-data "Direct link to heading")

NextAuth.js can be used with or without a database.

NextAuth.js は、データベースがあってもなくても使用できます。

- An open source solution that allows you to keep control of your data
- Supports Bring Your Own Database (BYOD) and can be used with any database
- Built-in support for [MySQL, MariaDB, Postgres, SQL Server, MongoDB and SQLite](https://next-auth.js.org/configuration/databases)
- Works great with databases from popular hosting providers
- Can also be used _without a database_ (e.g. OAuth + JWT)

- 自分のデータを自分で管理できるオープンソースソリューション
- Bring Your Own Database (BYOD)をサポートし、あらゆるデータベースと併用可能
- MySQL、MariaDB、Postgres、SQL Server、MongoDB、SQLite](https://next-auth.js.org/configuration/databases)をサポートしています。
- 一般的なホスティングプロバイダーのデータベースにも対応
- データベースなしでの使用も可能（例：OAuth + JWT)

_Note: Email sign in requires a database to be configured to store single-use verification tokens._

注：メールサインインには、シングルユースの認証トークンを保存するためのデータベースの設定が必要です。

### Secure by default[#](#secure-by-default "Direct link to heading")

### セキュアバイデフォルト[#](#secure-by-default "Direct link to heading")

- Promotes the use of passwordless sign in mechanisms
- Designed to be secure by default and encourage best practice for safeguarding user data
- Uses Cross Site Request Forgery Tokens on POST routes (sign in, sign out)
- Default cookie policy aims for the most restrictive policy appropriate for each cookie
- When JSON Web Tokens are enabled, they are signed by default (JWS) with HS512
- Use JWT encryption (JWE) by setting the option `encryption: true` (defaults to A256GCM)
- Auto-generates symmetric signing and encryption keys for developer convenience
- Features tab/window syncing and keepalive messages to support short lived sessions
- Attempts to implement the latest guidance published by [Open Web Application Security Project](https://owasp.org/)

- パスワードレスのサインインメカニズムの使用を促進する
- デフォルトで安全であるように設計されており、ユーザーデータを保護するためのベスト・プラクティスを推奨しています。
- POST ルート(sign in, sign out)に Cross Site Request Forgery Tokens を採用
- デフォルトのクッキーポリシーは、各クッキーに適した最も制限的なポリシーを目指す
- JSON Web Tokens を有効にすると、デフォルトで HS512 で署名される (JWS)
- オプション `encryption: true` (デフォルトは A256GCM) を設定することで、JWT の暗号化 (JWE) を使用します。
- 開発者の利便性を考慮し、対称性のある署名鍵と暗号鍵を自動生成
- 短時間のセッションをサポートするために、タブ/ウィンドウの同期とキープアライブメッセージを搭載
- [Open Web Application Security Project](https://owasp.org/)が公開している最新のガイダンスの実装を試みます。

Advanced options allow you to define your own routines to handle controlling what accounts are allowed to sign in, for encoding and decoding JSON Web Tokens and to set custom cookie security policies and session properties, so you can control who is able to sign in and how often sessions have to be re-validated.

詳細オプションでは、サインインを許可するアカウントの制御、JSON Web トークンのエンコードとデコード、カスタムクッキーのセキュリティポリシーとセッションプロパティの設定など、独自のルーチンを定義することができ、サインインできる人やセッションの再検証の頻度を制御することができます。

## Credits[#](#credits "Direct link to heading")

## クレジット[#](#credits "Direct link to heading")

NextAuth.js is an open source project that is only possible [thanks to contributors](https://next-auth.js.org/contributors).

NextAuth.js はオープンソースプロジェクトであり、貢献者のおかげで成り立っています(https://next-auth.js.org/contributors)。

## Getting Started[#](#getting-started "Direct link to heading")

[Check out the example code](https://next-auth.js.org/getting-started/example) to see how easy it is to use NextAuth.js for authentication.

[Check out the example code](https://next-auth.js.org/getting-started/example)で、NextAuth.js を使った認証がいかに簡単にできるかを確認してください。

[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/getting-started/introduction.md)
