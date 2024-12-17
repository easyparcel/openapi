## Oauth Authentication

EasyParcel's API uses the OAuth 2.0 authorization framework to ensure secure access to its services. OAuth 2.0 allows applications to authenticate and access the API on behalf of a user without directly exposing user credentials. 

- **OAuth Version**: OAuth 2.0
- **Grant Types Supported**: Authorization Code, Client Credentials
  
OAuth (Open Authorization) is an open standard protocol that allows secure authorization in a simple and standardized way from web, mobile, and desktop applications. EasyParcel uses OAuth to enable applications to securely access resources on behalf of the user without exposing the user's credentials.

OAuth involves three main components:
1. **Client**: The application requesting access to the user's resources.
2. **Resource Server**: The server hosting the protected resources.
3. **Authorization Server**: The server responsible for authenticating the user and issuing access tokens.

The OAuth 2.0 authorization flow consists of the following steps:
1. **Client Requests Authorization**: The client directs the resource owner to the authorization server to request authorization.
2. **Authorization Server Requests Login**: The authorization server prompts the resource owner to log into their EasyParcel account.
3. **User Logs In and Authenticates**: The resource owner logs into their EasyParcel account on the authorization server.
4. **Authorization Server Requests Consent**: The authorization server asks the resource owner for consent to grant access to the client.
5. **Authorization Grant**: The authorization server redirects the resource owner back to the client with an authorization grant.
6. **Client Requests Access Token**: The client requests an access token from the authorization server using the authorization grant.
7. **Authorization Server Issues Token**: The authorization server issues an access token to the client.
8. **Client Accesses Resource**: The client uses the access token to access the resource server on behalf of the resource owner.

## Security Considerations
Ensure to use HTTPS to protect communication between clients and servers to prevent eavesdropping and man-in-the-middle attacks.

### Oauth Authentication Flow
<img src="pictures/Oauth%20Flow%20chart.png" alt="Flow Chart" style="height: 350px;">


### Authorization Endpoint
The Authorization Endpoint is used by the client to obtain authorization from the resource owner via user-agent redirection.
#### Endpoint URL: 
`https://developer.easyparcel.com/ep_auth/login`

### Steps to get OAuth Authorization Access token

1.) Pass the above params to the urls
`https://developer.easyparcel.com/ep_auth/login`

Request:
- client_id
- redirect_uri
- state (optional)

| **Requested Parameters** | **Type** | **Required** | **Details**                                                                                                                   |
| ------------------------ | -------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| client_id                | string   | Yes          | client_id of your application                                                                                                 |
| redirect_uri             | string   | Yes          | The URI to which the client was redirected from the authorization server. The url of your app to redirect to                  |
| state                    | string   | Optional     | Generate and pass a unique string that helps ensure the response comes from the same client request, preventing CSRF attacks. |

2.) Will be prompt to login (these below steps are to authorize linking the application to your easyparcel account)
1. Login to your easyparcel account
   
		
	![Login%20Page.png](pictures/Login%20Page.png)

2. Select an account desire to link
   
		
   	![select account](pictures/select%20account.png)


3.  Allow access to Authorize link the account to with the application
   
		
	 ![allow access.png](pictures/allow%20access.png)


Respond param in redirect url Sample redirect url respond: 
`https://your-callback-url/callback?code=(code that requires to regenerate access token)`
- code(pass in get access token url)
- state (if got pass in auth url request)

| Responded Parameters | Type   | Required | Details                                                                                           |
|----------------------|--------|----------|---------------------------------------------------------------------------------------------------|
| Code                 | string | Yes      | The authorization code to pass to ep_auth to get the access token.                                |
| state                | string | (depend if got request on auth url) | A unique string that helps ensure the response comes from the same client request, preventing CSRF attacks. |

### Token Endpoint

The Token Endpoint is used by the client to obtain an access token by presenting its authorization grant.

**Endpoint URL**: 
`https://developer.easyparcel.com/ep_auth/token`

Pass the above params to get access token url or refresh access token url

Request:
- grant_type = “authorization_code”
- redirect_uri
- code
- refresh_token (if want refresh access token)
- state (optional)

| Requested Parameters | Type   | Required                              | Details                                                                                                 |
|----------------------|--------|---------------------------------------|---------------------------------------------------------------------------------------------------------|
| grant_type           | string | Yes                                   | The authorization_code to generate the access token.                                                    |
| redirect_uri code    | string | Yes                                   | The URI to which the client was redirected from the authorization server. The URL of your app to redirect to. |
| refresh_token        | string | (if want to refresh access token)     | The token that requests to generate a new access token once the current token expires. |
| state                | string | Optional                              | Request to check the state. A unique string that helps ensure the response comes from the same client request, preventing CSRF attacks. |


then will respond back with the access_token

```
{
	"token_type": "Bearer",
	"expires_in": 36000,
	"expires_at": "2024-12-12T13:03:23.013Z",
	"access_token": "your access token",
	"refresh_token": "Your refresh token",
	"refresh_token_expires_in": 31557600,
	"refresh_token_expires_at": "2025-12-12T09:03:23.013Z",
	
	"app": {
	"client_id": "your client-id",
	"callbackUrls": [],
	"redirectUris": [ "Your redirect uri"]
	}
}
```

L1 Respond

| Responded Parameters     | Type      | Details                                                                            |
| ------------------------ | --------- | ---------------------------------------------------------------------------------- |
| token_type               | string    | Token type                                                                         |
| expires_in               | int       | The token life span in seconds                                                     |
| expires_at               | date time | The Access token expiry date                                                       |
| access Token             | string    | The access token, required to access the API                                       |
| refresh_token            | string    | The new Refresh token for the next refresh (Depends if requested on ep_auth/token) |
| refresh_token_expires_in | int       | The refresh token life span in seconds                                             |
| refresh_token_expires_at | date time | The refresh token expiry date                                                      |
| App                      | array     | Refer to [L2 (App)](#App)                                                          |

L2 Respond
(**App**)
##### App

| Responded Parameters | Type   | Details                                                                               |
| -------------------- | ------ | ------------------------------------------------------------------------------------- |
| client_id            | string | Client ID of the application                                                          |
| callbackUris         | string | Destination that sends the user back after they have authenticated and granted access |
| redirectUris         | string | Redirect destination for the user after the authorization process                     |
