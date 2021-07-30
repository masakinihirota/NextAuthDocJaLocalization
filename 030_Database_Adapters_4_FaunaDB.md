FaunaDB Adapter | NextAuth.js
https://next-auth.js.org/adapters/fauna




# FaunaDB



This is the Fauna Adapter for [`next-auth`](https://next-auth.js.org). This package can only be used in conjunction with the primary `next-auth` package. It is not a standalone package.



You can find the Fauna schema and seed information in the docs at [next-auth.js.org/adapters/fauna](https://next-auth.js.org/adapters/fauna).



## Getting Started[#](#getting-started "Direct link to heading")



1.  Install `next-auth` and `@next-auth/fauna-adapter`



npm install next\-auth @next\-auth/fauna\-adapter



Copy



2.  Add this adapter to your `pages/api/[...nextauth].js` next-auth configuration object.



pages/api/auth/\[...nextauth\].js



import NextAuth from "next-auth"



import Providers from "next-auth/providers"



import \* as Fauna from "faunadb"



import { FaunaAdapter } from "@next-auth/fauna-adapter"



const client \= new Fauna.Client({



secret: "secret",



scheme: "http",



domain: "localhost",



port: 8443,



})



// For more information on each option (and a full list of options) go to



// https://next-auth.js.org/configuration/options



export default NextAuth({



// https://next-auth.js.org/configuration/providers



providers: \[



Providers.Google({



clientId: process.env.GOOGLE\_ID,



clientSecret: process.env.GOOGLE\_SECRET,



}),



\],



adapter: FaunaAdapter({ faunaClient: client})



...



})



Copy



## Schema[#](#schema "Direct link to heading")



Run the following commands inside of the `Shell` tab in the Fauna dashboard to setup the appropriate collections and indexes.



CreateCollection({ name: "accounts" })



CreateCollection({ name: "sessions" })



CreateCollection({ name: "users" })



CreateCollection({ name: "verification\_requests" })



CreateIndex({



name: "account\_by\_provider\_account\_id",



source: Collection("accounts"),



unique: true,



terms: \[



{ field: \["data", "providerId"\] },



{ field: \["data", "providerAccountId"\] },



\],



})



CreateIndex({



name: "session\_by\_token",



source: Collection("sessions"),



unique: true,



terms: \[{ field: \["data", "sessionToken"\] }\],



})



CreateIndex({



name: "user\_by\_email",



source: Collection("users"),



unique: true,



terms: \[{ field: \["data", "email"\] }\],



})



CreateIndex({



name: "verification\_request\_by\_token\_and\_identifier",



source: Collection("verification\_requests"),



unique: true,



terms: \[{ field: \["data", "token"\] }, { field: \["data", "identifier"\] }\],



})



Copy



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/adapters/fauna.md)1