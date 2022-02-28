# Authorization

### Introduction
This section describes how to **authorize** with an external application and how to use the provided **access token** for further usage.

### Workflow Description
To authorize any API calls, the standard **OAuth2.0** approach is used. Therefore the PSS®NMM is providing an endpoint which provides an access token to access any API. More information can be found here ([Microsoft Documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)).

![](/Images/Authorization.PNG)

### Function Description 
This section describes the necessary things to get an access token from the system.

###### Endpoint
> POST /connect/token

The token method requires different attributes:
###### Authorization
- Authorization Type: "Basic Auth"
- Username: "NMM_App"
- Password: "password" (this needs to be the shared secret, defined in the system)

###### Header
- Content-Type: "application/x-www-form-urlencoded"
- __tenant: "TenantName" (this is the tenant name defined in the system)

###### Body
    {
        "grant_type" : "password",
        "username" : "username",
        "password" : "password"
    }

###### Return
This function will return an object which holds the access token necessary for any further API calls.

    {
        "accesstoken" : string,
        "expires_in" : int,
        "token_type" : string,
        "refresh_token" : string,
        "scope" : string
    }
