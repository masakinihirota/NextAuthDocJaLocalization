Firebase Adapter | NextAuth.js
https://next-auth.js.org/adapters/firebase







# Firebase



This is the Firebase Adapter for [`next-auth`](https://next-auth.js.org). This package can only be used in conjunction with the primary `next-auth` package. It is not a standalone package.


これは [`next-auth`](https://next-auth.js.org) の Firebase アダプタです。このパッケージは、主要な `next-auth` パッケージと組み合わせてのみ使用できます。単体のパッケージではありません。



## Getting Started[#](#getting-started "Direct link to heading")



1.  Install `next-auth` and `@next-auth/firebase-adapter`


1.  next-auth "と"@next-auth/firebase-adapter "をインストールします。


```
npm install next-auth @next-auth/firebase-adapter
```


2.  Add this adapter to your `pages/api/auth/[...nextauth].js` next-auth configuration object.


2.  このアダプターを `pages/api/auth/[...nextauth].js` のnext-auth設定オブジェクトに追加します。


```pages/api/auth/[...nextauth].js
import NextAuth from "next-auth"
import Providers from "next-auth/providers"
import { FirebaseAdapter } from "@next-auth/firebase-adapter"

import firebase from "firebase/app"
import "firebase/firestore"

const firestore = (
  firebase.apps[0] ?? firebase.initializeApp(/* your config */)
).firestore()

// For more information on each option (and a full list of options) go to
// https://next-auth.js.org/configuration/options
export default NextAuth({
  // https://next-auth.js.org/configuration/providers
  providers: [
    Providers.Google({
      clientId: process.env.GOOGLE_ID,
      clientSecret: process.env.GOOGLE_SECRET,
    }),
  ],
  adapter: FirebaseAdapter(firestore),
  ...
})

```






## Options[#](#options "Direct link to heading")



When initializing the firestore adapter, you must pass in the firebase config object with the details from your project. More details on how to obtain that config object can be found [here](https://support.google.com/firebase/answer/7015592).



firestoreアダプターを初期化する際には、プロジェクトの詳細を記載したfirebase configオブジェクトを渡す必要があります。コンフィグオブジェクトの取得方法の詳細は[こちら](https://support.google.com/firebase/answer/7015592)を参照してください。



An example firebase config looks like this:


firebaseコンフィグの例は以下のようになります。

```

const firebaseConfig = {
  apiKey: "AIzaSyDOCAbC123dEf456GhI789jKl01-MnO",
  authDomain: "myapp-project-123.firebaseapp.com",
  databaseURL: "https://myapp-project-123.firebaseio.com",
  projectId: "myapp-project-123",
  storageBucket: "myapp-project-123.appspot.com",
  messagingSenderId: "65211879809",
  appId: "1:65211879909:web:3ae38ef1cdcb2e01fe5f0c",
  measurementId: "G-8GSGZQ44ST",
}

```





See [firebase.google.com/docs/web/setup](https://firebase.google.com/docs/web/setup) for more details.



##### **From Firebase**



**Caution**: We do not recommend manually modifying an app's Firebase config file or object. If you initialize an app with invalid or missing values for any of these required "Firebase options", then your end users may experience serious issues.


**注意**してください。アプリのFirebase設定ファイルやオブジェクトを手動で変更することはお勧めできません。これらのFirebaseオプションが無効または欠損している状態でアプリを初期化した場合、エンドユーザーに深刻な問題が発生する可能性があります。




For open source projects, we generally do not recommend including the app's Firebase config file or object in source control because, in most cases, your users should create their own Firebase projects and point their apps to their own Firebase resources (via their own Firebase config file or object).



オープンソースプロジェクトの場合、アプリのFirebase設定ファイルやオブジェクトをソースコントロールに含めることは一般的にお勧めしません。ほとんどの場合、ユーザーは独自のFirebaseプロジェクトを作成し、アプリを独自のFirebaseリソース（独自のFirebase設定ファイルやオブジェクトを介して）に向けるべきだからです。



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/adapters/firebase.md)






