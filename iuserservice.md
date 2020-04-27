# IUserService

You have to create a Userservice and [specify a userServiceClass in your modulesettings](installation-and-usage.md#configuration).  This  UserService needs to have three methodes, according to `cbauth.interfaces.IUserService`

```javascript
interface{

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

If you want to implement a UserService for `cbauth` combined with `cbsecurity` you will find your interface specification in `cbsecurity.interfaces.IUserService`.  Methods in this spec are equal.

The user component returned by both `retrieve..` methods needs to respond to `getId()` as specified by the [IAuthUser](iauthuser.md) interface. 

{% hint style="warning" %}
Combined with `cbsecurity` or `cbguard` you might have to specify additional methods for checking roles or permissions.
{% endhint %}



