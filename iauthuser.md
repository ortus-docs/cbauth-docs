# IAuthUser

You have to create a User component which responds to the `getId()` method. This user will be retrieved by the retrieve methods from your [`IUserService`](iuserservice.md)

```javascript
interface {

    /**
     * Return the unique identifier for the user
     */
    function getId();

    /**
     * Verify if the user has one or more of the passed in permissions
     *
     * @permission One or a list of permissions to check for access
     *
     */
    boolean function hasPermission( required permission );

    /**
     * Shortcut to verify it the user is logged in or not.
     */
    boolean function isLoggedIn();

}
```

{% hint style="warning" %}
Combined with [`cbsecurity`](https://coldbox-security.ortusbooks.com/usage/authentication-services#user-interface) or [`cbguard`](https://www.forgebox.io/view/cbguard) you might have to specify additional methods for checking roles or permissions.
{% endhint %}
