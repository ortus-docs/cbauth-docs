# Interception points

## Interceptions

`cbauth` announces several custom interception points. You can use these interception points to change request data or add additional values to session or request scopes. The `preAuthentication` and `postAuthentication` events fire during the standard `authenticate()` method call with a username and password. The `preLogin` and `postLogin` events fire during the `login()` method call. The `preLogout` and `postLogout` events fire during the `logout()` method call.

{% hint style="info" %}
the `preLogin` and `postLogin` interception points will be called during the course of `authenticate()`. The order of the calls then are `preAuthentication` -&gt; `preLogin` -&gt; `postLogin` -&gt; `postAuthentication`.
{% endhint %}

### preAuthentication

**InterceptData**

| Name | Description |
| :--- | :--- |
| username | The username passed in to `cbauth` |
| password | The password passed in to `cbauth` |

Modifying the values in the `interceptData` will change what is passed to `isValidCredentials` and `retrieveUserByUsername`. This is the prime time to ignore certain requests or remove or pad usernames.

### postAuthentication

**InterceptData**

| **Name** | Description |
| :--- | :--- |
| user | The user component to be logged in |
| sessionStorage | The sessionStorage object to store additional values if needed |
| requestStorage | The requestStorage object to store additional values if needed |

This is the prime time to store additional values based on the user returned.

### preLogin

**InterceptData**

| **Name** | Description |
| :--- | :--- |
| user | The user component to be logged in |

### postLogin

**InterceptData**

| **Name** | Description |
| :--- | :--- |
| user | The user component to be logged in. |
| sessionStorage | The sessionStorage object to store additional values if needed |
| requestStorage | The requestStorage object to store additional values if needed |

This is a good opportunity to store additional data if your application logged the user in manually without authenticating via a username/password like a "remember me" system.

### preLogout

**InterceptData**

| **Name** | Description |
| :--- | :--- |
| user | The user component to be logged in. |

### postLogout

InterceptData

| Name | Description |
| :--- | :--- |
| no additional data |  |



