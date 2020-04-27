# Introduction

Authentication is tedious. Many projects need some sort of authentication system. And in many of these projects you will basically start from scratch. Thats why `cbauth` was created.

cbauth is a library that handles creating user sessions for your app, while giving enough customisation to user different authentication methods and session storages.

These are some of the methods you can use in your project:

```javascript
auth.authenticate( username, password );
auth.isLoggedIn();
auth.getUser();
auth.logout();
```

`cbauth` manages user sessions, it doesn't protect handlers or actions from being accessed by logged out our unauthorised users. This part of the job is left to libraries such as cbsecurity or cbguard.

`cbauth` delivers a standard API for managing user session, but leaves plenty of customisation options to use different authentication methods and session storages.

