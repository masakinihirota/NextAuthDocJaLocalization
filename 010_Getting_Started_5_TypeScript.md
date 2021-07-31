TypeScript | NextAuth.js
https://next-auth.js.org/getting-started/typescript




# TypeScript



NextAuth.js comes with its own type definitions, so you can safely use it in your TypeScript projects. Even if you don't use TypeScript, IDEs like VSCode will pick this up, to provide you with a better developer experience. While you are typing, you will get suggestions about what certain objects/functions look like, and sometimes also links to documentation, examples and other useful resources.



NextAuth.jsには独自の型定義が用意されているので、TypeScriptプロジェクトで安全に使用することができます。TypeScriptを使用していなくても、VSCodeのようなIDEがこれを拾ってくれるので、より良い開発環境を提供することができます。タイピング中に、特定のオブジェクトや関数がどのように見えるかの提案があり、ドキュメントやサンプル、その他の有用なリソースへのリンクが表示されることもあります。



Check out the example repository showcasing how to use `next-auth` on a Next.js application with TypeScript:  
[https://github.com/nextauthjs/next-auth-typescript-example](https://github.com/nextauthjs/next-auth-typescript-example)


TypeScriptを使ったNext.jsアプリケーションで`next-auth`を使用する方法を紹介したサンプルリポジトリをご覧ください。 
[https://github.com/nextauthjs/next-auth-typescript-example](https://github.com/nextauthjs/next-auth-typescript-example)



##### warning



The types at [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) under the name of `@types/next-auth` are now deprecated, and not maintained anymore.


[DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)にある `@types/next-auth` という名前の型は、現在は非推奨であり、もうメンテナンスされていません。



___



## Adapters[#](#adapters "Direct link to heading")



If you're writing your own custom Adapter, you can take advantage of the types to make sure your implementation conforms to what's expected:


独自のアダプタを書く場合は、型を利用して期待通りの実装になるようにすることができます。


```
import type { Adapter } from "next-auth/adapters"

const MyAdapter: Adapter = () => {
  return {
    async getAdapter() {
      return {
        // your adapter methods here
      }
    },
  }
}
```



When writing your own custom Adapter in plain JavaScript, note that you can use **JSDoc** to get helpful editor hints and auto-completion like so:


独自のカスタムアダプタをプレーンな JavaScript で記述する場合は、 **JSDoc** を使用すると、エディタのヒントや自動補完機能が得られますのでご注意ください。


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


これは、VSCodeやWebStormのような強力なTypeScript統合機能を持つコードエディタで動作します。VIMやAtomのような軽量なエディタを使っている場合は動作しないかもしれません。



## Module Augmentation[#](#module-augmentation "Direct link to heading")


## モジュール拡張機能[#](#module-augmentation "Direct link to heading")



`next-auth` comes with certain types/interfaces, that are shared across submodules. Good examples are `Session` and `JWT`. Ideally, you should only need to create these types at a single place, and TS should pick them up in every location where they are referenced. Luckily, this is exactly what Module Augmentation can do for us. Define your shared interfaces in a single location, and get type-safety across your application, when you use `next-auth` (or one of its submodules).


`next-auth` には、サブモジュール間で共有される特定のタイプ/インターフェイスがあります。例えば、`Session` や `JWT` などがその例です。理想的には、これらの型を一か所で作成するだけでよく、参照されるすべての場所でTSがそれを拾うべきです。幸いなことに、これはまさにモジュール・オーグメンテーションが可能にしてくれるものです。next-auth` (またはそのサブモジュールの1つ) を使用すると、共有インターフェースを1箇所で定義し、アプリケーション全体で型安全性を確保できます。



### Main module[#](#main-module "Direct link to heading")



Let's look at `Session`:


それでは、`Session`を見てみましょう。



```pages/api/\[...nextauth\].ts
import NextAuth from "next-auth"

export default NextAuth({
  callbacks: {
    session(session, token) {
      return session // The type here should match the one returned in `useSession()`
    },
  },
})
```



```pages/index.ts
import { useSession } from "next-auth/client"

export default function IndexPage() {
  // `session` should match `callbacks.session()` in `NextAuth()`
  const [session] = useSession()

  return (
    // Your component
  )
}
```


To extend/augment this type, create a `types/next-auth.d.ts` file in your project:


このタイプを拡張するには、プロジェクト内に `types/next-auth.d.ts` ファイルを作成します。




```types/next-auth.d.ts
import NextAuth from "next-auth"

declare module "next-auth" {
  /**
   * Returned by `useSession`, `getSession` and received as a prop on the `Provider` React Context
   */
  interface Session {
    user: {
      /** The user's postal address. */
      address: string
    }
  }
}

```


#### Popular interfaces to augment[#](#popular-interfaces-to-augment "Direct link to heading")



Although you can augment almost anything, here are some of the more common interfaces that you might want to override in the `next-auth` module:


ほとんどのものをオーグメンテーションすることができますが、`next-auth`モジュールでオーバーライドしたい一般的なインターフェイスをいくつか紹介します。

/**
 * The shape of the user object returned in the OAuth providers' `profile` callback,
 * or the second parameter of the `session` callback, when using a database.
 */
interface User {}
/**
 * Usually contains information about the provider being used
 * and also extends `TokenSet`, which is different tokens returned by OAuth Providers.
 */
interface Account {}
/** The OAuth profile returned from your provider */
interface Profile {}

```

Make sure that the `types` folder is added to [`typeRoots`](https://www.typescriptlang.org/tsconfig/#typeRoots) in your project's `tsconfig.json` file.


プロジェクトの `tsconfig.json` ファイルの [typeRoots`](https://www.typescriptlang.org/tsconfig/#typeRoots) に `types` フォルダが追加されていることを確認してください。



### Submodules[#](#submodules "Direct link to heading")



The `JWT` interface can be found in the `next-auth/jwt` submodule:


JWT` インターフェースは、`next-auth/jwt` サブモジュールに含まれています。



```types/next-auth.d.ts
declare module "next-auth/jwt" {
  /** Returned by the `jwt` callback and `getToken`, when using JWT sessions */
  interface JWT {
    /** OpenID ID Token */
    idToken?: string
  }
}
```





### Useful links[#](#useful-links "Direct link to heading")



1.  [TypeScript documentation: Module Augmentation](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#module-augmentation)
2.  [Digital Ocean: Module Augmentation in TypeScript](https://www.digitalocean.com/community/tutorials/typescript-module-augmentation)



## Contributing[#](#contributing "Direct link to heading")



Contributions of any kind are always welcome, especially for TypeScript. Please keep in mind that we are a small team working on this project in our free time. We will try our best to give support, but if you think you have a solution for a problem, please open a PR!




どのような種類のコントリビューションでも、特に TypeScript についてはいつでも歓迎します。私たちは小さなチームで、自由な時間にこのプロジェクトに取り組んでいることを覚えておいてください。サポートには最善を尽くしますが、問題の解決策があると思われる場合は、ぜひPRを開いてください。

##### note

When contributing to TypeScript, if the actual JavaScript user API does not change in a breaking manner, we reserve the right to push any TypeScript change in a minor release. This is to ensure that we can keep us on a faster release cycle.



TypeScriptに貢献する際、実際のJavaScriptユーザーAPIが壊れるような形で変更されない場合、私たちはマイナーリリースでTypeScriptの変更をプッシュする権利を有します。これは、私たちがより速いリリースサイクルを維持できるようにするためです。



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/getting-started/typescript.md)