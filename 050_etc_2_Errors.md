Errors | NextAuth.js
https://next-auth.js.org/errors




# Errors



This is a list of errors output from NextAuth.js.



All errors indicate an unexpected problem, you should not expect to see errors.



If you are seeing any of these errors in the console, something is wrong.



___



## Client[#](#client "Direct link to heading")



These errors are returned from the client. As the client is [Universal JavaScript (or "Isomorphic JavaScript")](https://en.wikipedia.org/wiki/Isomorphic_JavaScript) it can be run on the client or server, so these errors can occur in both in the terminal and in the browser console.



#### CLIENT\_USE\_SESSION\_ERROR[#](#client_use_session_error "Direct link to heading")



This error occurs when the `useSession()` React Hook has a problem fetching session data.



#### CLIENT\_FETCH\_ERROR[#](#client_fetch_error "Direct link to heading")



If you see `CLIENT_FETCH_ERROR` make sure you have configured the `NEXTAUTH_URL` environment variable.



___



## Server[#](#server "Direct link to heading")



These errors are displayed on the terminal.



### OAuth[#](#oauth "Direct link to heading")



#### OAUTH\_GET\_ACCESS\_TOKEN\_ERROR[#](#oauth_get_access_token_error "Direct link to heading")



#### OAUTH\_V1\_GET\_ACCESS\_TOKEN\_ERROR[#](#oauth_v1_get_access_token_error "Direct link to heading")



#### OAUTH\_GET\_PROFILE\_ERROR[#](#oauth_get_profile_error "Direct link to heading")



#### OAUTH\_PARSE\_PROFILE\_ERROR[#](#oauth_parse_profile_error "Direct link to heading")



#### OAUTH\_CALLBACK\_HANDLER\_ERROR[#](#oauth_callback_handler_error "Direct link to heading")



___



### Signin / Callback[#](#signin--callback "Direct link to heading")



#### GET\_AUTHORIZATION\_URL\_ERROR[#](#get_authorization_url_error "Direct link to heading")



#### SIGNIN\_OAUTH\_ERROR[#](#signin_oauth_error "Direct link to heading")



#### CALLBACK\_OAUTH\_ERROR[#](#callback_oauth_error "Direct link to heading")



#### SIGNIN\_EMAIL\_ERROR[#](#signin_email_error "Direct link to heading")



#### CALLBACK\_EMAIL\_ERROR[#](#callback_email_error "Direct link to heading")



#### EMAIL\_REQUIRES\_ADAPTER\_ERROR[#](#email_requires_adapter_error "Direct link to heading")



The Email authentication provider can only be used if a database is configured.



#### CALLBACK\_CREDENTIALS\_JWT\_ERROR[#](#callback_credentials_jwt_error "Direct link to heading")



The Credentials Provider can only be used if JSON Web Tokens are used for sessions.



JSON Web Tokens are used for Sessions by default if you have not specified a database. However if you are using a database, then Database Sessions are enabled by default and you need to [explicitly enable JWT Sessions](https://next-auth.js.org/configuration/options#session) to use the Credentials Provider.



If you are using a Credentials Provider, NextAuth.js will not persist users or sessions in a database - user accounts used with the Credentials Provider must be created and managed outside of NextAuth.js.



In _most cases_ it does not make sense to specify a database in NextAuth.js options and support a Credentials Provider.



#### CALLBACK\_CREDENTIALS\_HANDLER\_ERROR[#](#callback_credentials_handler_error "Direct link to heading")



#### PKCE\_ERROR[#](#pkce_error "Direct link to heading")



The provider you tried to use failed when setting [PKCE or Proof Key for Code Exchange](https://tools.ietf.org/html/rfc7636#section-4.2). The `code_verifier` is saved in a cookie called (by default) `__Secure-next-auth.pkce.code_verifier` which expires after 15 minutes. Check if `cookies.pkceCodeVerifier` is configured correctly. The default `code_challenge_method` is `"S256"`. This is currently not configurable to `"plain"`, as it is not recommended, and in most cases it is only supported for backward compatibility.



___



### Session Handling[#](#session-handling "Direct link to heading")



#### JWT\_SESSION\_ERROR[#](#jwt_session_error "Direct link to heading")



[https://next-auth.js.org/errors#jwt\_session\_error](https://next-auth.js.org/errors#jwt_session_error) JWKKeySupport: the key does not support HS512 verify algorithm



The algorithm used for generating your key isn't listed as supported. You can generate a HS512 key using



jose newkey -s 512 -t oct -a HS512



Copy



If you are unable to use an HS512 key (for example to interoperate with other services) you can define what is supported using



jwt: {



signingKey: {"kty":"oct","kid":"--","alg":"HS256","k":"--"},



verificationOptions: {



algorithms: \["HS256"\]



}



}



Copy



#### SESSION\_ERROR[#](#session_error "Direct link to heading")



___



### Signout[#](#signout "Direct link to heading")



#### SIGNOUT\_ERROR[#](#signout_error "Direct link to heading")



___



### Database[#](#database "Direct link to heading")



These errors are logged by the TypeORM Adapter, which is the default database adapter.



They all indicate a problem interacting with the database.



#### ADAPTER\_CONNECTION\_ERROR[#](#adapter_connection_error "Direct link to heading")



#### CREATE\_USER\_ERROR[#](#create_user_error "Direct link to heading")



#### GET\_USER\_BY\_ID\_ERROR[#](#get_user_by_id_error "Direct link to heading")



#### GET\_USER\_BY\_EMAIL\_ERROR[#](#get_user_by_email_error "Direct link to heading")



#### GET\_USER\_BY\_PROVIDER\_ACCOUNT\_ID\_ERROR[#](#get_user_by_provider_account_id_error "Direct link to heading")



#### LINK\_ACCOUNT\_ERROR[#](#link_account_error "Direct link to heading")



#### CREATE\_SESSION\_ERROR[#](#create_session_error "Direct link to heading")



#### GET\_SESSION\_ERROR[#](#get_session_error "Direct link to heading")



#### UPDATE\_SESSION\_ERROR[#](#update_session_error "Direct link to heading")



#### DELETE\_SESSION\_ERROR[#](#delete_session_error "Direct link to heading")



#### CREATE\_VERIFICATION\_REQUEST\_ERROR[#](#create_verification_request_error "Direct link to heading")



#### GET\_VERIFICATION\_REQUEST\_ERROR[#](#get_verification_request_error "Direct link to heading")



#### DELETE\_VERIFICATION\_REQUEST\_ERROR[#](#delete_verification_request_error "Direct link to heading")



___



### Other[#](#other "Direct link to heading")



#### SEND\_VERIFICATION\_EMAIL\_ERROR[#](#send_verification_email_error "Direct link to heading")



This error occurs when the Email Authentication Provider is unable to send an email.



Check your mail server configuration.



#### MISSING\_NEXTAUTH\_API\_ROUTE\_ERROR[#](#missing_nextauth_api_route_error "Direct link to heading")



This error happens when `[...nextauth].js` file is not found inside `pages/api/auth`.



Make sure the file is there and the filename is written correctly.



[Edit this page](https://github.com/nextauthjs/next-auth/edit/main/www/docs/errors.md)







