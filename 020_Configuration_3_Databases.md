Databases | NextAuth.js
https://next-auth.js.org/configuration/databases




# Databases



NextAuth.js comes with multiple ways of connecting to a database:



NextAuth.js には、データベースに接続するための複数の方法が用意されています。



-   **TypeORM** (default)  
    _The TypeORM adapter supports MySQL, PostgreSQL, MSSQL, SQLite and MongoDB databases._
-   **Prisma**  
    _The Prisma 2 adapter supports MySQL, PostgreSQL and SQLite databases._
-   **Fauna**  
    _The FaunaDB adapter only supports FaunaDB._
-   **Custom Adapter**  
    _A custom Adapter can be used to connect to any database._


- **TypeORM** (デフォルト)  
    TypeORM** (デフォルト) TypeORMアダプタは、MySQL、PostgreSQL、MSSQL、SQLite、MongoDBのデータベースをサポートしています。
- **Prisma**（デフォルト  
    _Prisma 2アダプタは、MySQL、PostgreSQL、SQLiteデータベースをサポートしています。
- **Fauna** （ファウナ  
    _FaunaDB アダプタは FaunaDB のみをサポートしています。
- カスタムアダプタ  
    _カスタムアダプタは、任意のデータベースに接続するために使用することができます。



> There are currently efforts in the [`nextauthjs/adapters`](https://github.com/nextauthjs/adapters) repository to get community-based DynamoDB, Sanity, PouchDB and Sequelize Adapters merged. If you are interested in any of the above, feel free to check out the PRs in the `nextauthjs/adapters` repository!


> 現在、[`nextauthjs/adapters`](https://github.com/nextauthjs/adapters) リポジトリでは、コミュニティベースの DynamoDB、Sanity、PouchDB、Sequelize アダプタをマージする作業が行われています。上記のいずれかに興味がある方は、`nextauthjs/adapters`リポジトリのPRを気軽にチェックしてみてください!



**This document covers the default adapter (TypeORM).**



**このドキュメントは、デフォルトのアダプタ(TypeORM)を対象としています**。




See the [documentation for adapters](https://next-auth.js.org/adapters/overview) to learn more about using Prisma adapter or using a custom adapter.


Prismaアダプタの使用やカスタムアダプタの使用については、[document for adapters](https://next-auth.js.org/adapters/overview)を参照してください。



To learn more about databases in NextAuth.js and how they are used, check out [databases in the FAQ](https://next-auth.js.org/faq#databases).


NextAuth.jsのデータベースについて、またその使い方については、[FAQのデータベース](https://next-auth.js.org/faq#databases)をご覧ください。




___



## How to use a database[#](#how-to-use-a-database "Direct link to heading")




You can specify database credentials as as a connection string or a [TypeORM configuration](https://github.com/typeorm/typeorm/blob/master/docs/using-ormconfig.md) object.



データベースの認証情報は、接続文字列または[TypeORM configuration](https://github.com/typeorm/typeorm/blob/master/docs/using-ormconfig.md)オブジェクトとして指定することができます。



The following approaches are exactly equivalent:



以下の方法は全く同じです。


```
database: "mysql://nextauth:password@127.0.0.1:3306/database_name"
```

```
database: {
  type: 'mysql',
  host: '127.0.0.1',
  port: 3306,
  username: 'nextauth',
  password: 'password',
  database: 'database_name'
}
```



##### tip



You can pass in any valid [TypeORM configuration option](https://github.com/typeorm/typeorm/blob/master/docs/using-ormconfig.md).



有効な[TypeORM設定オプション](https://github.com/typeorm/typeorm/blob/master/docs/using-ormconfig.md)を渡すことができます。



_e.g. To set a prefix for all table names you can use the **entityPrefix** option as connection string parameter:_


例えば、全てのテーブル名にプレフィックスを設定するには、接続文字列パラメータとして **entityPrefix** オプションを使用することができます:

```
"mysql://nextauth:password@127.0.0.1:3306/database_name?entityPrefix=nextauth_"

```




_…or as a database configuration object:_


_...または、データベース構成オブジェクトとして使用します。

```
database: {
  type: 'mysql',
  host: '127.0.0.1',
  port: 3306,
  username: 'nextauth',
  password: 'password',
  database: 'database_name',
  entityPrefix: 'nextauth_'
}
```



___



## Setting up a database[#](#setting-up-a-database "Direct link to heading")



Using SQL to create tables and columns is the recommended way to set up an SQL database for NextAuth.js.


SQLを使ってテーブルやカラムを作成することは、NextAuth.jsのSQLデータベースをセットアップするための推奨される方法です。



Check out the links below for SQL you can run to set up a database for NextAuth.js.


NextAuth.js 用のデータベースをセットアップするために実行できる SQL については、以下のリンクを参照してください。




-   [MySQL Schema](https://next-auth.js.org/adapters/typeorm/mysql)
-   [Postgres Schema](https://next-auth.js.org/adapters/typeorm/postgres)



_If you are running SQLite, MongoDB or a Document database you can skip this step._


_SQLite、MongoDB、Documentデータベースを使用している場合は、このステップをスキップできます。



Alternatively, you can also have your database configured automatically using the `synchronize: true` option:



また、`synchronize: true`オプションを使って、データベースを自動的に設定することもできます。


```
database: "mysql://nextauth:password@127.0.0.1:3306/database_name?synchronize=true"
```

```
database: {
  type: 'mysql',
  host: '127.0.0.1',
  port: 3306,
  username: 'nextauth',
  password: 'password',
  database: 'database_name',
  synchronize: true
}
```



##### warning



**The `synchronize` option should not be used against production databases.**



**「synchronize」オプションは、運用中のデータベースに対して使用すべきではありません。'**


It is useful to create the tables you need when setting up a database for the first time, but it should not be enabled against production databases as it may result in data loss if there is a difference between the schema that found in the database and the schema that the version of NextAuth.js being used is expecting.



初めてデータベースをセットアップする際に必要なテーブルを作成するのに便利ですが、データベースにあるスキーマと、使用しているNextAuth.jsのバージョンが期待するスキーマに違いがあると、データが失われる可能性があるため、本番のデータベースに対しては有効にすべきではありません。



___



## Supported databases[#](#supported-databases "Direct link to heading")



The default database adapter is TypeORM, but only some databases supported by TypeORM are supported by NextAuth.js as custom logic needs to be handled by NextAuth.js.


デフォルトのデータベースアダプターはTypeORMですが、カスタムロジックはNextAuth.jsで処理する必要があるため、TypeORMでサポートされている一部のデータベースのみがNextAuth.jsでサポートされています。



Databases compatible with MySQL, Postgres and MongoDB should work out of the box with NextAuth.js. When used with any other database, NextAuth.js will assume an ANSI SQL compatible database.


MySQL、Postgres、MongoDBと互換性のあるデータベースは、NextAuth.jsですぐに動作するはずです。それ以外のデータベースを使用する場合、NextAuth.jsはANSI SQL互換のデータベースを想定しています。


##### tip



When configuring your database you also need to install an appropriate **node module** for your database.


データベースを設定する際には、そのデータベースに適した **node モジュール** をインストールする必要があります。



### MySQL[#](#mysql "Direct link to heading")



Install module: `npm i mysql`



#### Example[#](#example "Direct link to heading")

```
database: "mysql://username:password@127.0.0.1:3306/database_name"
```




### MariaDB[#](#mariadb "Direct link to heading")



Install module: `npm i mariadb`



#### Example[#](#example-1 "Direct link to heading")


```
database: "mariadb://username:password@127.0.0.1:3306/database_name"
```

### Postgres / CockroachDB[#](#postgres--cockroachdb "Direct link to heading")


```
Install module: `npm i pg`
```

```
database: "postgres://username:password@127.0.0.1:5432/database_name"
```


#### Example[#](#example-2 "Direct link to heading")



PostgresDB

```
database: "postgres://username:password@127.0.0.1:5432/database_name"
```

CockroachDB

```
database: "postgres://username:password@127.0.0.1:26257/database_name"
```

If the node is using Self-signed cert


ノードが自己署名証明書を使用している場合

```
database: {
    type: "cockroachdb",
    host: process.env.DATABASE_HOST,
    port: 26257,
    username: process.env.DATABASE_USER,
    password: process.env.DATABASE_PASSWORD,
    database: process.env.DATABASE_NAME,
    ssl: {
      rejectUnauthorized: false,
      ca: fs.readFileSync('/path/to/server-certificates/root.crt').toString()
    },
  },
```



Read more: [https://node-postgres.com/features/ssl](https://node-postgres.com/features/ssl)



___



### Microsoft SQL Server[#](#microsoft-sql-server "Direct link to heading")



Install module: `npm i mssql`



#### Example[#](#example-3 "Direct link to heading")


```
database: "mssql://sa:password@localhost:1433/database_name"
```



### MongoDB[#](#mongodb "Direct link to heading")



Install module: `npm i mongodb`



#### Example[#](#example-4 "Direct link to heading")

```
database: "mongodb://username:password@127.0.0.1:3306/database_name"
```


### SQLite[#](#sqlite "Direct link to heading")



_SQLite is intended only for development / testing and not for production use._


_SQLiteは開発/テストのみを目的としており、本番での使用はできません。


Install module: `npm i sqlite3`



#### Example[#](#example-5 "Direct link to heading")

```
database: "sqlite://localhost/:memory:"
```




## Other databases[#](#other-databases "Direct link to heading")



See the [documentation for adapters](https://next-auth.js.org/adapters/overview) for more information on advanced configuration, including how to use NextAuth.js with other databases using a [custom adapter](https://next-auth.js.org/tutorials/creating-a-database-adapter).


[カスタムアダプター](https://next-auth.js.org/tutorials/creating-a-database-adapter)を使ってNextAuth.jsを他のデータベースで使用する方法など、高度な設定については[アダプターのためのドキュメント](https://next-auth.js.org/adapters/overview)を参照してください。


[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/configuration/databases.md)