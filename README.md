# Introduction

Authentication is tedious. Many projects need some sort of authentication system. And in many of these projects you will basically start from scratch. That's why `cbauth` was created.

cbauth is a library that handles creating user sessions for your app including authenticating users, logging users in and out, and retrieving the currently authenticated user. It is customizable to plug in to yout existing authentication method and session storage.

{% hint style="info" %}
cbauth is designed to be customized for existing applications.  As such, it requires some work to configure correctly.  If you are starting a new project and would like this configuration done for you check out the pre-configured application templates on ForgeBox like [`quick-with-auth`](https://forgebox.io/view/cbtemplate-quick-with-auth) and [`quick-tailwind-inertia`](https://forgebox.io/view/cbtemplate-quick-tailwind-inertia).
{% endhint %}

These are some of the methods you can use in your project:

```javascript
auth.authenticate( username, password );
auth.isLoggedIn();
auth.getUser();
auth.logout();
```

{% hint style="warning" %}
While `cbauth` manages user sessions, it doesn't protect handlers or actions from being accessed by logged out our unauthorized users. This part of the job is left to libraries such as [cbsecurity](https://coldbox-security.ortusbooks.com/) or [cbguard](https://www.forgebox.io/view/cbguard).
{% endhint %}

