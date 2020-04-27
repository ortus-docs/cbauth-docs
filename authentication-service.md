# Authentication Service

The authentication service can be used by injecting it using WireBox:

```javascript
property name="auth" inject="authenticationService@cbauth";

// OR

var auth = wirebox.getInstance( "authenticationService@cbauth" );
```

Or, the quick way, you can just use the `auth()` helper method \(which is actually just a shortcut to a wirebox injection\). The `auth()` helper is very useful in views. And since Wirebox handles singleton management, you don't have to worry about calling `auth()`too many times.

{% hint style="success" %}
The `auth()` helper is available in handlers, layouts, and views.  You will need to use the injection if you need cbauth in other models.
{% endhint %}

## Methods

### login

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| user | any | `true` |  | The user component to log in. The component must respond to the `getId()` method. |

Logs a user in to the system. The returned user component must respond to the `getId()` method \(as defined in the [`IAuthUser`](iauthuser.md) interface\). Additionally, the user is cached in the `request` scope. If a user is already in the session, this will replace it with the given user. This method returns the passed in `user` object.

### logout

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| No arguments |  |  |  |  |

Logs a user out of system. This method can be called regardless of if there is currently a logged in user.

### authenticate

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| username | string | `true` |  | The username to attempt to log in. |
| password | string | `true` |  | The password to attempt to log in. |

Attempts to log a user by calling the `retrieveUserByUsername` and `isValidCredentials` on the provided `userServiceClass`. If `isValidCredentials` returns `false`, it throws a `InvalidCredentials` exception.

If it succeeds, it returns the logged in `user` object. If it succeeds, it also sets the user id \(obtained by calling `getId()` on the returned user component\) in the configured `sessionStorage` and the returned user component in the configured `requestStorage`.

### isLoggedIn

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| no arguments |  |  |  |  |

Returns `boolean` whether a user is logged in to the system. 

### check

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| no arguments |  |  |  |  |

Alias for `isLoggedIn`

### guest

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| no arguments |  |  |  |  |

Returns whether a user is logged out of the system.  Opposite of `check()` and `isLoggedIn()`.

### getUser

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| no arguments |  |  |  |  |

Returns the currently logged in user component.

If there is no logged in user, it throws a `NoUserLoggedIn` exception.

If there is a user object in the configured `requestStorage`, it is returned.

If the user object has not been fetched this request, it uses the id set in the configured `sessionStorage` to fetch the user \(using `retrieveUserById`\). It then sets the user in the configured `requestStorage` so subsequent calls to `getUser` don't re-fetch the user.

### user

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| no arguments |  |  |  |  |

Alias for `getUser`

### getUserId

| argument | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
|  |  |  |  |  |

Returns the currently logged in user id.

If there is no logged in user, it throws a `NoUserLoggedIn` exception.

