# Installation and usage

## Requirements

* Lucee 5+
* Adobe ColdFusion 2016+
* Coldbox 4.3 +

## Installation

`cbauth` requires ColdBox 4.3 or higher for [module parent settings](https://github.com/ortus-docs/coldbox-docs/blob/v4.x/intro/introduction/whats-new-with-4.3.0.md).

`cbauth` can be installed with

```javascript
box install cbauth
```

## Configuration

cbauth needs a UserService which has to be specified in the module settings. By default,  cbauth uses the sessionStorage `sessionStorage@cbstorages`  and requestStorage `RequestStorage@cbstorages` .  Your config settings will look like this:

```javascript
	moduleSettings = {
			cbAuth: {
				userServiceClass: "UserService",
				//optional, override when required
				requestStorage: "RequestStorage@cbstorages",
				sessionStorage: "SessionStorage@cbstorages"  
			},
			//..... other module settings 
	}
```

You can specify other requestStorage or sessionStorage \(e.g distributed cache\) as long as your new storages follow the Interface definitions as defined e.g

```javascript
interface name="SessionStorageInterface" {
	public any function getVar( required string name, any defaultValue );
	public void function setVar( required string name, required any value );
	public boolean function deleteVar( required string name );
	public boolean function exists( required string name );
}
```

{% hint style="info" %}
You don't have to formally implement the interface in your code.
{% endhint %}

## Usage

Before you can use `cbauth` you have to create a UserService which implement the [IUserInterface](iuserservice.md).  

{% code title="cbauth.interfaces.IUserService" %}
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
{% endcode %}

You also have a User class which implements the [IauthUser](iauthuser.md) interface. If you use `cbauth` combined with `cbsecurity` or `cbguard` there are some additional method requirements for the User. Please check the corresponding docs for details.

{% code title="cbauth.interfaces.IAuthUser" %}
```javascript
interface{

    /**
     * Return the unique identifier for the user
     */
    function getId();

}
```
{% endcode %}

When you have create your User and UserService and configured the moduleSettings you are ready to use the AuthenticationService. You can inject the authentication service using Wirebox.

```javascript
property name="auth" inject="authenticationService@cbauth";

// OR

var auth = wirebox.getInstance( "authenticationService@cbauth" );
```

Or, the quick way, you can just use the `auth()` helper method \(which is actually just a shortcut to a wirebox injection\). The `auth()` helper is very useful in views. And since Wirebox handles singleton management, you don't have to worry about calling `auth()`too many times.

The Authentication service provides you with all methods for handling user sessions, e.g:

```javascript
auth.authenticate( username, password );
auth.isLoggedIn();
auth.getUser();
auth.logout();
```

After login your userID is stored in sessionstorage. Your user object will be cached in the requeststorage, so you only have to hit your database once per request to access user information. 

The full list of methods is described in the [Authentication Service](authentication-service.md) section.

