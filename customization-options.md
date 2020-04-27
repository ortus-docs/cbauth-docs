# Customization Options

`cbauth` is quite flexible. In your `IUserService` implementation you can define how you want to retrieve your `IAuthUser` implementation: from a database, LDAP or any other authentication provider. You can define any properties you want to store, permissions or roles, and additional data for your authenticated user.   

The current user will be retrieved and cached in a configured `requestStorage`. The userID will be stored in a configured `sessionStorage`.  Both `sessionStorage` and `requestStorage` can be anything you want, as long as they implement the required methods. A common scenario, for example, is when you don't want to use ColdFusion or Lucee sessions for API applications, but instead use a distributed cache.

```javascript
interface name="SessionStorageInterface" { // or "RequestStorageInterface"
	  public any function getVar( required string name, any defaultValue );
    public void function setVar( required string name, required any value );
	  public boolean function deleteVar( required string name );
	  public boolean function exists( required string name );
}
```

Additional information for your user can be stored after authentication in your sessio- or request storage by using the [interception points](interception-points.md) announced by cbauth.

