# Security and OAuth2 #
[OAuth2.0 RFC6749](https://datatracker.ietf.org/doc/html/rfc6749)

OAuth is an open secure protocol for authorizing users between unrelated services. It enables one service to access resources hosted on other services without having to share user credentials. 
- Parties involved: 
  - Resource Owner/User: The person who gives permission to access their protected resources hosted by a third-party provider. 
  - Client: The web service acting on behalf of the user to access the resources hosted by a third party provider. 
  - Authorization Server: The third party server contacted by the client that displays a prompt for the user to authorize the client to act on the user's behalf. 
  - Resource server: The third party server hosting the protected resources owned by the user.

Any web application acting as a client should register their web application with the OAuth2 provider by supplying the following information: 
1. Name of the application 
2. Where the application is hosted. 
3. A URI endpoint - also called as Redirect URI or Callback URI. 

After registration, the OAuth2 provider gives the following information to the Web Application: 
1. ClientID
2. ClientSecret
3. Authorization Server URI - a URI for the client to request authorization
4. Access Token URI - to obtain access token in exchange for the authorization code.  
5. Resource Server URI - a URI for the client to access the protected resource with the access token. 

## OAuth2 Web application flow ##
The Web application flow for deploying OAuth2 in a web application has three basic steps: 
1. Authorize
2. Fetch Access Token
3. Obtain user info

### Authorize ###
The web application requests access from the user to authorize access to their account hosted at a third-party OAuth2 provider. 
Client-request permission: The URL contains the following information: 
- Response Type - grant or code
- ClientID - to identify the web application
- Redirect URI - where the user is redirected to 
- Scope - The level of authorization
- State - randomly generated string that can be passed to the authorization server, that will be passed back again for validation to mitigate fraud. 
```http
https://api.authorization-server.com/authorize
  ?response_type=code
  &client_id=123
  &redirect_uri=https://your-web-app.com/redirect
  &scope=photos
  &state=1234-zyxa-9134-wpst
```
After the user authorizes the web application to access the protected resource -> Following information is provided: 
1. Code: a short-lived authorization code that the web application expects from the server. 
2. State: the state credential passed earlier from the client. 

The web application should check that the state value matches the one that it sent to prevent any malicious attempts from hackers and CSRF attacks. 

### Fetch Access Token ###
To exchange the authorization token for an access token.
Client-exchange: The client web application sends a HTTP POST request to the authorization server's token endpoint with the following: 
1. Grant Type - tells the authorization server which grant or flow to use. 
2. Code - authorization code received by the web application from the authorization server. 
3. Redirect URI
4. ClientID
5. ClientSecret
```http
https://api.authorization-server.com/token
  grant_type=authorization_code
  &code=123456
  &redirect_uri=https://your-web-app.com/redirect
  &client_id=123
  &client_secret=456
```
> Authorization server grants token: After checking every parameter sent, the authorization server generates and sends back an access token.

### Obtain User info ###
Client-requests resources: The web application sends a HTTP GET request to the resource server with the credentials obtained from the authorization server. 
```http
GET /user HTTP/1.1
Host: api.resource-server.com
Authorization: Bearer access_token
```
Resource Server sends resources: The resource server validates the access token and sends back the requested data. 


## JWTs - JSON Web Tokens - [RFC7519](https://datatracker.ietf.org/doc/html/rfc7519) ##

