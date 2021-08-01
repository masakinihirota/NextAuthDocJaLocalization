DynamoDB Adapter | NextAuth.js
https://next-auth.js.org/adapters/dynamodb





# DynamoDB



This is the AWS DynamoDB Adapter for next-auth. This package can only be used in conjunction with the primary next-auth package. It is not a standalone package.


これは next-auth 用の AWS DynamoDB Adapter です。このパッケージは、プライマリのnext-authパッケージと組み合わせてのみ使用できます。単体のパッケージではありません。



You need a table with a partition key `pk` and a sort key `sk`. Your table also needs a global secondary index named `GSI1` with `GSI1PK` as partition key and `GSI1SK` as sorting key. You can set whatever you want as the table name and the billing method.

パーティションキー `pk` とソートキー `sk` を持つテーブルが必要です。このテーブルには、`GSI1`という名前のグローバルセカンダリインデックスが必要で、`GSI1PK`がパーティションキー、`GSI1SK`がソートキーとなります。テーブル名や課金方法には、好きなものを設定することができます。



You can find the full schema in the table structure section below.


完全なスキーマは以下のテーブル構造のセクションで見ることができます。



## Getting Started[#](#getting-started "Direct link to heading")



1.  Install `next-auth` and `@next-auth/dynamodb-adapter`


1.  next-auth`と`@next-auth/dynamodb-adapter`をインストールします。

```
npm install next-auth @next-auth/dynamodb-adapter

```


2.  Add this adapter to your `pages/api/auth/[...nextauth].js` next-auth configuration object.


2.  このアダプターを `pages/api/auth/[..nextauth].js` の next-auth 設定オブジェクトに追加します。




You need to pass `DocumentClient` instance from `aws-sdk` to the adapter. The default table name is `next-auth`, but you can customise that by passing `{ tableName: 'your-table-name' }` as the second parameter in the adapter.

aws-sdk "の "DocumentClient "インスタンスをアダプタに渡す必要があります。デフォルトのテーブル名は `next-auth` ですが、これをカスタマイズするには、 `{ tableName: 'your-table-name' }` をアダプタの2番目のパラメータとして渡すことでカスタマイズできます。

```pages/api/auth/[...nextauth].js
import AWS from "aws-sdk";
import NextAuth from "next-auth";
import Providers from "next-auth/providers";
import { DynamoDBAdapter } from "@next-auth/dynamodb-adapter"

AWS.config.update({
  accessKeyId: process.env.NEXT_AUTH_AWS_ACCESS_KEY,
  secretAccessKey: process.env.NEXT_AUTH_AWS_SECRET_KEY,
  region: process.env.NEXT_AUTH_AWS_REGION,
});

export default NextAuth({
  // Configure one or more authentication providers
  providers: [
    Providers.GitHub({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
    Providers.Email({
      server: process.env.EMAIL_SERVER,
      from: process.env.EMAIL_FROM,
    }),
    // ...add more providers here
  ],
  adapter: DynamoDBAdapter(
    new AWS.DynamoDB.DocumentClient()
  ),
  ...
});
```



(AWS secrets start with `NEXT_AUTH_` in order to not conflict with [Vercel's reserved environment variables](https://vercel.com/docs/environment-variables#reserved-environment-variables).)


(AWSのシークレットは、[Vercelの予約済み環境変数](https://vercel.com/docs/environment-variables#reserved-environment-variables)と衝突しないように、`NEXT_AUTH_`で始まります。)




## Schema[#](#schema "Direct link to heading")



The table respects the single table design pattern. This has many advantages:


テーブルは、シングルテーブルのデザインパターンを採用しています。これには多くの利点があります。



-   Only one table to manage, monitor and provision.
-   Querying relations is faster than with multi-table schemas (for eg. retrieving all sessions for a user).
-   Only one table needs to be replicated, if you want to go multi-region.


- 管理、監視、プロビジョニングが1つのテーブルで済む。
- 複数のテーブルを持つスキーマに比べて、リレーションのクエリが高速になります（例：ユーザーのすべてのセッションを取得する場合）。
- 複数の地域に展開する場合、1つのテーブルだけを複製する必要があります。



Here is a schema of the table :


以下は、テーブルのスキーマです。



![DynamoDB Table](https://i.imgur.com/hGZtWDq.png)



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/adapters/dynamodb.md)







