Overview | NextAuth.js
https://next-auth.js.org/adapters/overview




# Overview



An **Adapter** in NextAuth.js connects your application to whatever database or backend system you want to use to store data for user accounts, sessions, etc.



NextAuth.js の **Adapter** は、ユーザーアカウントやセッションなどのデータを保存するために使いたいデータベースやバックエンドシステムにアプリケーションを接続します。



The adapters can be found in their own repository under [`nextauthjs/adapters`](https://github.com/nextauthjs/adapters).


アダプタは、[`nextauthjs/adapters`](https://github.com/nextauthjs/adapters) にある独自のリポジトリに格納されています。




There you can find the following adapters:


そこには次のようなアダプタがあります。



-   [`typeorm-legacy`](https://next-auth.js.org/adapters/typeorm/typeorm-overview)
-   [`prisma`](https://next-auth.js.org/adapters/prisma)
-   [`prisma-legacy`](https://next-auth.js.org/adapters/prisma-legacy)
-   [`fauna`](https://next-auth.js.org/adapters/fauna)
-   [`dynamodb`](https://next-auth.js.org/adapters/dynamodb)
-   [`firebase`](https://next-auth.js.org/adapters/firebase)



## Custom Adapter[#](#custom-adapter "Direct link to heading")



See the tutorial for [creating a database Adapter](https://next-auth.js.org/tutorials/creating-a-database-adapter) for more information on how to create a custom Adapter. Have a look at the [Adapter repository](https://github.com/nextauthjs/adapters) to see community maintained custom Adapter or add your own.


カスタムアダプタを作成する方法については、 [create a database Adapter](https://next-auth.js.org/tutorials/creating-a-database-adapter) のチュートリアルを参照ください。[Adapter repository](https://github.com/nextauthjs/adapters) を見ると、 コミュニティで管理されているカスタムアダプタを見ることができますし、 自分のアダプタを追加することもできます。



### Editor integration[#](#editor-integration "Direct link to heading")


### エディタとの連携[#](#editor-integration "Direct link to heading")



When writing your own custom Adapter in plain JavaScript, note that you can use **JSDoc** to get helpful editor hints and auto-completion like so:


自作のアダプタをプレーンな JavaScript で書く場合は、 **JSDoc** を使うと、次のようにエディタのヒントや自動補完が得られることに注意してください。

```
/** @type { import("next-auth/adapters").Adapter } */
const MyAdapter = () => {
  return {
    async getAdapter() {
      return {
        // your adapter methods here
      }
    },
  }
}

```


##### note



This will work in code editors with a strong TypeScript integration like VSCode or WebStorm. It might not work if you're using more lightweight editors like VIM or Atom.


これは、VSCodeやWebStormのような強力なTypeScript統合機能を持つコードエディタで動作します。VIMやAtomのような軽量なエディタを使用している場合は動作しないかもしれません。




[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/adapters/overview.md)