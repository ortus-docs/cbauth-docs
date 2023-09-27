# IUserService

You have to create a `UserService` and [specify a `userServiceClass` in your `moduleSettings`](installation-and-usage.md#configuration).  This  `UserService` needs to have three methods, according to `cbauth.interfaces.IUserService`

```javascript
interface {

	/**
	 * Verify if the incoming username/password are valid credentials.
	 *
	 * @username The username
	 * @password The password
	 */
	boolean function isValidCredentials( required username, required password );

	/**
	 * Retrieve a user by username
	 *
	 * @return User that implements IAuthUser
	 */
	function retrieveUserByUsername( required username );

	/**
	 * Retrieve a user by unique identifier
	 *
	 * @id The unique identifier
	 *
	 * @return User that implements IAuthUser
	 */
	function retrieveUserById( required id );
}
```

{% hint style="info" %}
If you want to implement a `UserService` for `cbauth` combined with `cbsecurity` you will find your interface specification in [`cbsecurity.interfaces.IUserService`](https://coldbox-security.ortusbooks.com/usage/authentication-services#authentication-service-interface).  Methods in this spec are equal.
{% endhint %}

The user component returned by both `retrieve...` methods needs to respond to `getId()` as specified by the [IAuthUser](iauthuser.md) interface.&#x20;

{% hint style="warning" %}
Combined with [`cbsecurity`](https://coldbox-security.ortusbooks.com/usage/authentication-services#authentication-service-interface) or [`cbguard`](https://www.forgebox.io/view/cbguard) you might have to specify additional methods for checking roles or permissions.
{% endhint %}

