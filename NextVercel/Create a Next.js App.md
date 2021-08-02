Create a Next.js App | Learn Next.js
https://nextjs.org/learn/basics/create-nextjs-app








## Create a Next.js App



[1](https://nextjs.org/learn/basics/create-nextjs-app)



[2](https://nextjs.org/learn/basics/create-nextjs-app/setup)



[3](https://nextjs.org/learn/basics/create-nextjs-app/welcome-to-nextjs)



[4](https://nextjs.org/learn/basics/create-nextjs-app/editing-the-page)



To build a complete web application with React from scratch, there are many important details you need to consider:


Reactを使って完全なWebアプリケーションを一から構築するには、考慮しなければならない重要な内容がたくさんあります。




-   Code has to be bundled using a bundler like webpack and transformed using a compiler like Babel.
-   You need to do production optimizations such as code splitting.
-   You might want to statically pre-render some pages for performance and SEO. You might also want to use server-side rendering or client-side rendering.
-   You might have to write some server-side code to connect your React app to your data store.



- コードは、webpackのようなバンドルラーを使って束ね、Babelのようなコンパイラを使って変換しなければなりません。
- コードをwebpackのようなbundlerで束ね、Babelのようなコンパイラで変換する必要があります。
- パフォーマンスとSEOのために、一部のページを静的にプリレンダリングする必要があるかもしれません。また、サーバーサイドレンダリングやクライアントサイドレンダリングを使用したい場合もあるでしょう。
- Reactアプリをデータストアに接続するために、サーバーサイドのコードを書かなければならないかもしれません。



A _framework_ can solve these problems. But such a framework must have the right level of abstraction — otherwise it won’t be very useful. It also needs to have great "Developer Experience", ensuring you and your team have an amazing experience while writing code.


フレームワークはこれらの問題を解決することができます。しかし、そのようなフレームワークは適切な抽象度を持っていなければなりません - そうでなければあまり役に立ちません。また、コードを書いている間、あなたやあなたのチームが素晴らしい体験をできるように、優れた「デベロッパー・エクスペリエンス」を備えている必要があります。



### Next.js: The React Framework



Enter **Next.js**, the React Framework. Next.js provides a solution to all of the above problems. But more importantly, it puts you and your team in the [pit of success](https://blog.codinghorror.com/falling-into-the-pit-of-success/) when building React applications.


Reactフレームワークである**Next.js**を紹介します。Next.jsは、上記の問題をすべて解決してくれます。しかし、もっと重要なことは、Reactアプリケーションを構築する際に、あなたとあなたのチームを[成功の落とし穴](https://blog.codinghorror.com/falling-into-the-pit-of-success/)に入れることです。



Next.js aims to have best-in-class developer experience and many built-in features, such as:



Next.jsは、クラス最高の開発者体験と、以下のような多くの組み込み機能を持つことを目指しています。



-   An intuitive [page-based](https://nextjs.org/docs/basic-features/pages) routing system (with support for [dynamic routes](https://nextjs.org/docs/routing/dynamic-routes))
-   [Pre-rendering](https://nextjs.org/docs/basic-features/pages#pre-rendering), both [static generation](https://nextjs.org/docs/basic-features/pages#static-generation-recommended) (SSG) and [server-side rendering](https://nextjs.org/docs/basic-features/pages#server-side-rendering) (SSR) are supported on a per-page basis
-   Automatic code splitting for faster page loads
-   [Client-side routing](https://nextjs.org/docs/routing/introduction#linking-between-pages) with optimized prefetching
-   [Built-in CSS](https://nextjs.org/docs/basic-features/built-in-css-support) and [Sass support](https://nextjs.org/docs/basic-features/built-in-css-support#sass-support), and support for any [CSS-in-JS](https://nextjs.org/docs/basic-features/built-in-css-support#css-in-js) library
-   Development environment with [Fast Refresh](https://nextjs.org/docs/basic-features/fast-refresh) support
-   [API routes](https://nextjs.org/docs/api-routes/introduction) to build API endpoints with Serverless Functions
-   Fully extendable


- 直感的な[ページベース](https://nextjs.org/docs/basic-features/pages)のルーティングシステム（[ダイナミックルート](https://nextjs.org/docs/routing/dynamic-routes)をサポート）。
- [プリレンダリング](https://nextjs.org/docs/basic-features/pages#pre-rendering)、[静的生成](https://nextjs.org/docs/basic-features/pages#static-generation-recommended) (SSG)と[サーバーサイドレンダリング](https://nextjs.org/docs/basic-features/pages#server-side-rendering) (SSR)の両方をページ単位でサポート
- コードの自動分割によるページロードの高速化
- 最適化されたプリフェッチを備えた[クライアントサイドルーティング](https://nextjs.org/docs/routing/introduction#linking-between-pages)
- [内蔵CSS](https://nextjs.org/docs/basic-features/built-in-css-support)と[Sassサポート](https://nextjs.org/docs/basic-features/built-in-css-support#sass-support)、および任意の[CSS-in-JS](https://nextjs.org/docs/basic-features/built-in-css-support#css-in-js)ライブラリのサポート
- [Fast Refresh](https://nextjs.org/docs/basic-features/fast-refresh)に対応した開発環境
- Serverless FunctionsでAPIエンドポイントを構築するための[API routes](https://nextjs.org/docs/api-routes/introduction)
- 完全な拡張性



Next.js is used in tens of thousands of production-facing websites and web applications, including many of the world's largest brands.


Next.jsは、世界の大手ブランドをはじめとする何万もの本番用WebサイトやWebアプリケーションで使用されています。


### About This Tutorial



This free interactive course will guide you through how to get started with Next.js.


この無料のインタラクティブコースでは、Next.jsの始め方を説明します。



In this tutorial, you’ll learn Next.js basics by creating a very simple **blog app**. Here’s an example of the final result:


このチュートリアルでは、非常にシンプルな**ブログアプリ**を作成することで、Next.jsの基本を学びます。ここでは、最終的な結果の例を示します。



**[https://next-learn-starter.vercel.app](https://next-learn-starter.vercel.app/)** ([source](https://github.com/vercel/next-learn-starter/tree/master/demo))



Let’s get started!



> This tutorial assumes basic knowledge of JavaScript and React. If you’ve never written React code, you should go through [the official React tutorial](https://reactjs.org/tutorial/tutorial.html) first.
> 
> If you’re looking for documentation instead, [visit the Next.js documentation](https://nextjs.org/docs/getting-started).




> このチュートリアルは、JavaScriptとReactの基本的な知識を前提としています。もしReactのコードを書いたことがないのであれば、まず[公式Reactチュートリアル](https://reactjs.org/tutorial/tutorial.html)をご覧ください。
> 
> > 代わりにドキュメントを探しているのであれば、[Next.js documentation](https://nextjs.org/docs/getting-started)をご覧ください。
