Email | NextAuth.js
https://next-auth.js.org/providers/email




# Email



## Overview[#](#overview "Direct link to heading")



The Email provider uses email to send "magic links" that can be used to sign in, you will likely have seen these if you have used services like Slack before.

メールプロバイダは、サインインに使用できる「マジックリンク」をメールで送信します。



Adding support for signing in via email in addition to one or more OAuth services provides a way for users to sign in if they lose access to their OAuth account (e.g. if it is locked or deleted).



1つまたは複数のOAuthサービスに加えて電子メールによるサインインのサポートを追加することで、ユーザーがOAuthアカウントへのアクセスを失った場合（ロックや削除など）にもサインインできるようになります。



The Email provider can be used in conjunction with (or instead of) one or more OAuth providers.


メールプロバイダは、1つまたは複数のOAuthプロバイダと組み合わせて (または代わりに) 使用することができます。




### How it works[#](#how-it-works "Direct link to heading")



On initial sign in, a **Verification Token** is sent to the email address provided. By default this token is valid for 24 hours. If the Verification Token is used within that time (i.e. by clicking on the link in the email) an account is created for the user and they are signed in.


初回のサインイン時に、入力されたメールアドレスに **Verification Token** が送信されます。デフォルトでは、このトークンの有効期限は24時間です。24時間以内にVerification Tokenが使用されると（例：メール内のリンクをクリックする）、そのユーザーのアカウントが作成され、サインインしたことになります。



If someone provides the email address of an _existing account_ when signing in, an email is sent and they are signed into the account associated with that email address when they follow the link in the email.


また、サインイン時に既存のアカウントのEメールアドレスを入力した場合は、Eメールが送信され、Eメール内のリンクをクリックすると、そのEメールアドレスに関連付けられているアカウントにサインインしたことになります。




##### tip



The Email Provider can be used with both JSON Web Tokens and database sessions, but you **must** configure a database to use it. It is not possible to enable email sign in without using a database.


Email Providerは、JSON Web Tokensとデータベースセッションの両方で使用できますが、使用するためにはデータベースを**設定する必要があります。データベースを使用せずにEメールサインインを有効にすることはできません。



## Options[#](#options "Direct link to heading")



The **Email Provider** comes with a set of default options:


**Eメールプロバイダ**には、デフォルトのオプションが用意されています。



-   [Email Provider options](https://github.com/nextauthjs/next-auth/blob/main/src/providers/email.js)



You can override any of the options to suit your own use case.


これらのオプションは、ユーザーの使用目的に合わせて上書きすることができます。




## Configuration[#](#configuration "Direct link to heading")



1.  You will need an SMTP account; ideally for one of the [services known to work with nodemailer](http://nodemailer.com/smtp/well-known/).
2.  There are two ways to configure the SMTP server connection.



1.  SMTPアカウントが必要です。理想的には[nodemailerで動作することが知られているサービス](http://nodemailer.com/smtp/well-known/)のいずれかです。
2. SMTPサーバーの接続を設定するには2つの方法があります。



You can either use a connection string or a nodemailer configuration object.


接続文字列を使用する方法と、nodemailerの設定オブジェクトを使用する方法です。


2.1 **Using a connection string**



Create an .env file to the root of your project and add the connection string and email address.

プロジェクトのルートに.envファイルを作成し、接続文字列と電子メールアドレスを追加します。




```.env
    EMAIL_SERVER=smtp://username:password@smtp.example.com:587
    EMAIL_FROM=noreply@example.com
```

Now you can add the email provider like this:


これで、以下のようにメール・プロバイダを追加することができます。

```pages/api/auth/[...nextauth].js
providers: [
  Providers.Email({
    server: process.env.EMAIL_SERVER,
    from: process.env.EMAIL_FROM
  }),
],

```



2.2 **Using a configuration object**



In your `.env` file in the root of your project simply add the configuration object options individually:



プロジェクトのルートにある `.env` ファイルに、コンフィギュレーション・オブジェクトのオプションを個別に追加します。




```.env
EMAIL_SERVER_USER=username
EMAIL_SERVER_PASSWORD=password
EMAIL_SERVER_HOST=smtp.example.com
    EMAIL_SERVER_PORT=587
    EMAIL_FROM=noreply@example.com

```



Now you can add the provider settings to the NextAuth options object in the Email Provider.


これで、プロバイダの設定をEmail ProviderのNextAuth optionsオブジェクトに追加することができます。


```pages/api/auth/[...nextauth].js
providers: [
  Providers.Email({
    server: {
      host: process.env.EMAIL_SERVER_HOST,
      port: process.env.EMAIL_SERVER_PORT,
      auth: {
        user: process.env.EMAIL_SERVER_USER,
        pass: process.env.EMAIL_SERVER_PASSWORD
      }
    },
    from: process.env.EMAIL_FROM
  }),
],
```




3.  You can now sign in with an email address at `/api/auth/signin`.



3.  これで、`/api/auth/signin`でメールアドレスを使ってサインインできるようになりました。




A user account (i.e. an entry in the Users table) will not be created for the user until the first time they verify their email address. If an email address is already associated with an account, the user will be signed in to that account when they use the link in the email.


ユーザーアカウント（Usersテーブルのエントリ）は、ユーザーが初めてメールアドレスを確認するまで作成されません。メールアドレスがすでにアカウントに関連付けられている場合は、ユーザーがメール内のリンクを使用すると、そのアカウントにサインインします。



## Customizing emails[#](#Customizing-emails "Direct link to heading")



You can fully customise the sign in email that is sent by passing a custom function as the `sendVerificationRequest` option to `Providers.Email()`.


カスタム関数を `Providers.Email()` の `sendVerificationRequest` オプションに渡すことで、送信されるサインインメールを完全にカスタマイズすることができます。



e.g.

```pages/api/auth/[...nextauth].js
providers: [
  Providers.Email({
    server: process.env.EMAIL_SERVER,
    from: process.env.EMAIL_FROM,
    sendVerificationRequest: ({
      identifier: email,
      url,
      token,
      baseUrl,
      provider,
    }) => {
      /* your function */
    },
  }),
]

```



The following code shows the complete source for the built-in `sendVerificationRequest()` method:


次のコードは、組み込みの`sendVerificationRequest()`メソッドの完全なソースです。

```
import nodemailer from "nodemailer"

const sendVerificationRequest = ({
  identifier: email,
  url,
  token,
  baseUrl,
  provider,
}) => {
  return new Promise((resolve, reject) => {
    const { server, from } = provider
    // Strip protocol from URL and use domain as site name
    const site = baseUrl.replace(/^https?:\/\//, "")

    nodemailer.createTransport(server).sendMail(
      {
        to: email,
        from,
        subject: `Sign in to ${site}`,
        text: text({ url, site, email }),
        html: html({ url, site, email }),
      },
      (error) => {
        if (error) {
          logger.error("SEND_VERIFICATION_EMAIL_ERROR", email, error)
          return reject(new Error("SEND_VERIFICATION_EMAIL_ERROR", error))
        }
        return resolve()
      }
    )
  })
}

// Email HTML body
const html = ({ url, site, email }) => {
  // Insert invisible space into domains and email address to prevent both the
  // email address and the domain from being turned into a hyperlink by email
  // clients like Outlook and Apple mail, as this is confusing because it seems
  // like they are supposed to click on their email address to sign in.
  const escapedEmail = `${email.replace(/\./g, "&#8203;.")}`
  const escapedSite = `${site.replace(/\./g, "&#8203;.")}`

  // Some simple styling options
  const backgroundColor = "#f9f9f9"
  const textColor = "#444444"
  const mainBackgroundColor = "#ffffff"
  const buttonBackgroundColor = "#346df1"
  const buttonBorderColor = "#346df1"
  const buttonTextColor = "#ffffff"

  // Uses tables for layout and inline CSS due to email client limitations
  return `
<body style="background: ${backgroundColor};">
  <table width="100%" border="0" cellspacing="0" cellpadding="0">
    <tr>
      <td align="center" style="padding: 10px 0px 20px 0px; font-size: 22px; font-family: Helvetica, Arial, sans-serif; color: ${textColor};">
        <strong>${escapedSite}</strong>
      </td>
    </tr>
  </table>
  <table width="100%" border="0" cellspacing="20" cellpadding="0" style="background: ${mainBackgroundColor}; max-width: 600px; margin: auto; border-radius: 10px;">
    <tr>
      <td align="center" style="padding: 10px 0px 0px 0px; font-size: 18px; font-family: Helvetica, Arial, sans-serif; color: ${textColor};">
        Sign in as <strong>${escapedEmail}</strong>
      </td>
    </tr>
    <tr>
      <td align="center" style="padding: 20px 0;">
        <table border="0" cellspacing="0" cellpadding="0">
          <tr>
            <td align="center" style="border-radius: 5px;" bgcolor="${buttonBackgroundColor}"><a href="${url}" target="_blank" style="font-size: 18px; font-family: Helvetica, Arial, sans-serif; color: ${buttonTextColor}; text-decoration: none; text-decoration: none;border-radius: 5px; padding: 10px 20px; border: 1px solid ${buttonBorderColor}; display: inline-block; font-weight: bold;">Sign in</a></td>
          </tr>
        </table>
      </td>
    </tr>
    <tr>
      <td align="center" style="padding: 0px 0px 10px 0px; font-size: 16px; line-height: 22px; font-family: Helvetica, Arial, sans-serif; color: ${textColor};">
        If you did not request this email you can safely ignore it.
      </td>
    </tr>
  </table>
</body>
`
}

// Email text body – fallback for email clients that don't render HTML
const text = ({ url, site }) => `Sign in to ${site}\n${url}\n\n`

```



##### tip



If you want to generate great looking email client compatible HTML with React, check out [https://mjml.io](https://mjml.io)


Reactで見栄えのするメールクライアント対応のHTMLを生成したい場合は、[https://mjml.io](英語)をご覧ください。




## Customizing the Verification Token[#](#Customizing-the-verification-token "Direct link to heading")


## Customizing the Verification Token[#](#Customizing-the-verification-token "Direct link to heading")




By default, we are generating a random verification token. You can define a `generateVerificationToken` method in your provider options if you want to override it:


デフォルトでは、ランダムな検証トークンを生成しています。これをオーバーライドしたい場合は、プロバイダのオプションで `generateVerificationToken` メソッドを定義します。

```pages/api/auth/[...nextauth].js
providers: [
  Providers.Email({
    async generateVerificationToken() {
      return "ABC123"
    }
  })
],

```

[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/providers/email.md)





