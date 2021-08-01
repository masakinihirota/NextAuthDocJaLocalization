# Overview



## TypeORM Adapter[#](#typeorm-adapter "Direct link to heading")



NextAuth.js comes with a default Adapter that uses [TypeORM](https://typeorm.io/) so that it can be used with many different databases without any further configuration, you simply add the node module for the database driver you want to use in your project and pass a database connection string to NextAuth.js.



NextAuth.js にはデフォルトで [TypeORM](https://typeorm.io/) を用いたアダプタが用意されており、 さまざまなデータベースに対応できるようになっています。使用したいデータベースドライバの node モジュールをプロジェクトに追加し、データベースの接続文字列を NextAuth.js に渡すだけです。



### Database Schemas[#](#database-schemas "Direct link to heading")



Configure your database by creating the tables and columns to match the schema expected by NextAuth.js.

NextAuth.js が期待するスキーマに合わせてテーブルやカラムを作成し、データベースを設定します。


-   [MySQL Schema](https://next-auth.js.org/adapters/typeorm/mysql)
-   [Postgres Schema](https://next-auth.js.org/adapters/typeorm/postgres)
-   [Microsoft SQL Server Schema](https://next-auth.js.org/adapters/typeorm/mssql)
-   [MongoDB](https://next-auth.js.org/adapters/typeorm/mongodb)



The default Adapter is the TypeORM Adapter and the default database type for TypeORM is SQLite, the following configuration options are exactly equivalent.


デフォルトのアダプタはTypeORMアダプタで、TypeORMのデフォルトのデータベースタイプはSQLiteです。以下の設定オプションは全く同じです。

```
database: {
  type: 'sqlite',
  database: ':memory:',
  synchronize: true
}
```

```
adapter: Adapters.Default({
  type: "sqlite",
  database: ":memory:",
  synchronize: true,
})
```

```
adapter: Adapters.TypeORM.Adapter({
  type: "sqlite",
  database: ":memory:",
  synchronize: true,
})
```




The tutorial [Custom models with TypeORM](https://next-auth.js.org/tutorials/typeorm-custom-models) explains how to extend the built in models and schemas used by the TypeORM Adapter. You can use these models in your own code.



チュートリアル[Custom models with TypeORM](https://next-auth.js.org/tutorials/typeorm-custom-models)では、TypeORMアダプタで使用されている組み込みモデルやスキーマを拡張する方法を説明しています。これらのモデルを自分のコードで使用することができます。



##### tip



The `synchronize` option in TypeORM will generate SQL that exactly matches the documented schemas for MySQL and Postgres. This will automatically apply any changes it finds in the entity model, therefore it **should not be enabled against production databases** as it may cause data loss if the configured schema does not match the expected schema!


TypeORMの`synchronize`オプションは、MySQLやPostgresのドキュメントされたスキーマに正確にマッチするSQLを生成します。エンティティモデルに変更があった場合、自動的に適用されます。したがって、設定されたスキーマが期待されるスキーマと一致しない場合、データ損失を引き起こす可能性があるため、**実稼働中のデータベース**に対して有効にすべきではありません。


[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/adapters/typeorm/overview.md)