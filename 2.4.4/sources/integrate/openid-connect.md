# Table of Contents 

# Overview
[OpenID Connect](http://openid.net/connect) ("Connect") is an authentication layer built on OAuth 2.0. 
It is both a profile and extension of OAuth. The authorization server (or "OpenID Provider" in this case) holds information about a person. OAuth is used to protect this information, enabling a third-party application (client) to access it on behalf of a person. To authorize the release of information, the person is authenticated, and the OpenID Provider provides details to the client about when and how that authentication happened.

## OpenID Connect Architecture

Some OpenID Connect jargon to keep in mind:

- The *end user* or *subject* (a.k.a. OAuth 2.0 resource owner) is the person whose user information the application needs to access.

- The *OpenID Provider* is the OAuth authorization server which issues the tokens and generally provides the user infromation. The role is similar to a SAML identity provider (IDP).

- The *User Agent* is normally a browser, but could also be a native application. 

- The *Relying Party (RP)* (a.k.a. OAuth 2.0 client) needs access to the end user's protected user information. The RP can be either server side (like a typical web application), or client side (for example a JavaScript application residing in the User Agent).

The Gluu Server is an OpenID Provider. The OP holds information about the user and allows the end user to consent to providing the RP with access to user information (unless the RP has been "pre-authorized", in which case the OP may just release information automatically). OpenID Connect defines a unique identification for an account (subject identifier + issuer identifier), and the RP can use this as a key to its own user profile. 

OpenID Connect defines some optional dynamic features. It makes it possible to discover OpenID Provider metadata, and to register RP client applications on the fly. For example, hypothetically, a person should be able to shop at a new online store, and authenticate at their home domain by providing nothing more then an email address. From the email domain, a discovery request and client registration can happen, and the person can be redirected to authenticate at their home domain.

# OpenID Connect Support in the Gluu Server
The Gluu Server has passed all [conformance profiles for an OpenID Connect Provider](http://openid.net/certification/). As an OpenID Provider, the Gluu Server enables OpenID Connect clients to discover its capabilities, handle both dynamic and static registration of relying parties, respond to relying party requests with authorization codes, access tokens, and user information according to the code, implicit and hybrid flows.

## OpenID Connect Implicit Flows
This flow is used only for user-agent based clients--primarily JavaScript--where you cannot hide a client secret, so client authentication makes no sense. The main difference between the OAuth and OpenID Connect implicit flows is the use of the *id_token*, which provides extra contextual information about the subject and authentication event. Properly validated, the *id_token* also adds additional security to the transaction. For example, the *nonce* can be verified, and the *at_hash* can be used to check the integrity of the returned token. For more information, read the [OpenID Connect Implicit Client Implementer's guide](http://openid.net/specs/openid-connectimplicit-1_0.html).

## OpenID Connect Authorization Code Flows
The OpenID Connect Authorization Code Flow specifies how the relying party interacts with the OpenID Provider based on use of the OAuth 2.0 authorization grant. The authorization code flow is more secure than the implicit flow because the tokens are never exposed to the web browser and because the client is authenticated. As with the implicit flow, the id_token should be validated and adds extra security over an OAuth2 code flow.

## OpenID Connect Hybrid Flows 
Hybrid flow is one of the least understood Connect features, but it's really not that bad. The `response_type` for hybrid flow always includes code, plus either token, `id_token`, or both. The hybrid flow can be used to achieve higher security levels--by returning the `id_token` from the authorization endpoint, the client can verify the integrity of the code by verifying the `id_token` claim `c_hash`. The most logical hybrid flow `response_type` is `code id_token`. You can also get back and access token from the authorization endpoint in the hybrid flow.

## Discovery 

The first thing you want to know about any OAuth2 API is where are the
endpoints (i.e. what are the uris where you call the APIs).
OpenID Connect provides a very simple mechanism to accomplish this: 
[OpenID Connect Discovery](http://openid.net/specs/openid-connect-discovery-1_0.html).

In order for an OpenID Connect Relying Party to utilize OpenID Connect
services for an End-User, the RP needs to know where the OpenID Provider is.
OpenID Connect uses WebFinger [WebFinger](http://en.wikipedia.org/wiki/WebFinger)
to locate the OpenID Provider for an End-User.

Once the OpenID Provider has been identified, the configuration information
for the OP is retrieved from a well-known location as a JSON document,
including its OAuth 2.0 endpoint locations.

If you want to try a discovery request, you can make the following
WebFinger request to discover the Issuer location:

```
GET /.well-known/webfinger?resource=https%3A%2F%2Fidp.gluu.org&rel=http%3A%2F%2Fopenid.net%2Fspecs%2Fconnect%2F1.0%2Fissuer HTTP/1.1
Host: idp.gluu.org

HTTP/1.1 200
Content-Type: application/jrd+json

{
    "subject": "https://idp.gluu.org",
    "links": [{
        "rel": "http://openid.net/specs/connect/1.0/issuer",
        "href": "https://idp.gluu.org"
    }]
}
```

Using the Issuer location discovered, the OpenID Provider's configuration information can be retrieved.

The RP makes the following request to the Issuer https://<domain>/.well-known/openid-configuration to obtain its
Configuration information:

```
GET /.well-known/openid-configuration HTTP/1.1
Host: idp.gluu.org

HTTP/1.1 200
Content-Type: application/json

{
    "issuer": "https://idp.gluu.org",
    "authorization_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/authorize",
    "token_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/token",
    "userinfo_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/userinfo",
    "clientinfo_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/clientinfo",
    "check_session_iframe": "https://idp.gluu.org/oxauth/opiframe",
    "end_session_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/end_session",
    "jwks_uri": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/jwks",
    "registration_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/register",
    "validate_token_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/validate",
    "federation_metadata_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/federationmetadata",
    "federation_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/federation",
    "id_generation_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/id",
    "introspection_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/introspection",
    "scopes_supported": [
        "clientinfo",
        "email",
        "openid",
        "profile",
        "address",
        "uma_protection",
        "user_name",
        "uma_authorization",
        "mobile_phone",
        "phone"
    ],
    "response_types_supported": [
        "code",
        "code id_token",
        "token",
        "token id_token",
        "code token",
        "code token id_token",
        "id_token"
    ],
    "grant_types_supported": [
        "authorization_code",
        "implicit",
        "urn:ietf:params:oauth:grant-type:jwt-bearer"
    ],
    "acr_values_supported": [""u2f", "duo", "basic", "mt", "oxpush2", "gplus", "internal"],
    "auth_level_mapping": {"-1": [["internal"]]},
    "subject_types_supported": [
        "public",
        "pairwise"
    ],
    "userinfo_signing_alg_values_supported": [
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "userinfo_encryption_alg_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "userinfo_encryption_enc_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "id_token_signing_alg_values_supported": [
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "id_token_encryption_alg_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "id_token_encryption_enc_values_supported": [
        "A128CBC+HS256", "A256CBC+HS512",
        "A128GCM", "A256GCM"
    ],
    "request_object_signing_alg_values_supported": [
        "none",
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "request_object_encryption_alg_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "request_object_encryption_enc_values_supported": [
        "A128CBC+HS256", "A256CBC+HS512",
        "A128GCM", "A256GCM"
    ],
    "token_endpoint_auth_methods_supported": [
        "client_secret_basic",
        "client_secret_post",
        "client_secret_jwt",
        "private_key_jwt"
    ],
    "token_endpoint_auth_signing_alg_values_supported": [
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "display_values_supported": [
        "page",
        "popup"
    ],
    "claim_types_supported": ["normal"],
    "claims_supported": [
        "birthdate",
        "country",
        "name",
        "email",
        "email_verified",
        "given_name",
        "gender",
        "inum",
        "family_name",
        "updated_at",
        "locale",
        "middle_name",
        "nickname",
        "phone_number_verified",
        "picture",
        "preferred_username",
        "profile",
        "zoneinfo",
        "user_name",
        "website"
    ],
    "service_documentation": "http://gluu.org/docs",
    "claims_locales_supported": ["en"],
    "ui_locales_supported": [
        "en", "es"
    ],
    "scope_to_claims_mapping": [
        {"clientinfo": [
            "name",
            "inum"
        ]},
        {"email": [
            "email_verified",
            "email"
        ]},
        {"openid": ["inum"]},
        {"profile": [
            "name",
            "family_name",
            "given_name",
            "middle_name",
            "nickname",
            "preferred_username",
            "profile",
            "picture",
            "website",
            "gender",
            "birthdate",
            "zoneinfo",
            "locale",
            "updated_at"
        ]},
        {"address": [
            "formatted",
            "postal_code",
            "street_address",
            "locality",
            "country",
            "region"
        ]},
        {"uma_protection": []},
        {"user_name": ["user_name"]},
        {"uma_authorization": []},
        {"mobile_phone": ["phone_mobile_number"]},
        {"phone": [
            "phone_number_verified",
            "phone_number"
        ]}
    ],
    "claims_parameter_supported": true,
    "request_parameter_supported": true,
    "request_uri_parameter_supported": true,
    "require_request_uri_registration": false,
    "op_policy_uri": "http://ox.gluu.org/doku.php?id=oxauth:policy",
    "op_tos_uri": "http://ox.gluu.org/doku.php?id=oxauth:tos",
    "http_logout_supported": "true",
    "logout_session_supported": "true"
}
```

The following is an example using the [oxAuth-Client](https://ox.gluu.org/maven/org/xdi/oxauth-client/) lib:

```
String resource = "acct:mike@idp.gluu.org";
}
```

The following is an example using the [oxAuth-Client](https://ox.gluu.org/maven/org/xdi/oxauth-client/) lib:

```
String resource = "acct:mike@idp.gluu.org";

OpenIdConnectDiscoveryClient openIdConnectDiscoveryClient = new OpenIdConnectDiscoveryClient(resource);
OpenIdConnectDiscoveryResponse openIdConnectDiscoveryResponse = openIdConnectDiscoveryClient.exec();

.....

OpenIdConfigurationClient client = new OpenIdConfigurationClient(configurationEndpoint);
OpenIdConfigurationResponse response = client.execOpenIdConfiguration();
```

See [org.xdi.oxauth.ws.rs.ConfigurationRestWebServiceHttpTest](https://github.com/GluuFederation/oxAuth/blob/master/Client/src/test/java/org/xdi/oxauth/ws/rs/ConfigurationRestWebServiceHttpTest.java)

## Scopes

In SAML, the IdP releases attributes to the SP. OpenID Connect provides
similar functionality, with more flexibility in case the person needs to
self-approve the release of information from the IdP to the website (or
mobile application). In OAuth2, scopes can be used for various purposes.
OpenID Connect uses OAuth2 scopes to "group" attributes. For example, we
could have a scope called "address" that includes the street, city,
state, and country user claims. By default the Gluu Server defines nine
scopes: `address`, `clientinfo`, `email`, `mobile_phone`, `openid`, `permission`, `phone`, `profile`, `user_name`

![Scopes Screenshot](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_scope.png)

The Gluu Server administrator can easily add more scopes in the GUI.
Click *Add Scope* and you will be presented with the following screen:

![Add Scopes](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/openid_connect/oxtrust_scope_screenshot.png)

You will have the ability to provide a Display Name, Description,
whether or not the scope is provided by default, and the claims that are
included in the scope.

Default Scope needs some further explanation. When a client uses dynamic
client registration, the OpenID Connect specification says that the
`openid` scope should always be released, which contains an identifier
for that person, normally the username. If you want to release another
scope automatically, set the Default Scope to `true` for that scope. You
can always explicitly release a scope to a certain client later on, but
this will require some manual intervention by the domain administrator.

To add more claims, simply click "Add Claim" and you will be presented
with the following screen:

![Add Claims](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_scopeadd.png)

## Client Registration

A client in OAuth2 could be either a website or mobile application.
OpenID Connect has an API for [Dynamic Client
Registration](http://openid.net/specs/openid-connect-registration-1_0.html)
which efficiently pushes the task to the application developer. If you
do not want to write an application to register your client, there are a
few web pages around that can do the job for you. Gluu publishes the
[oxAuth-RP](https://ce-dev.gluu.org/oxauth-rp) and there is also another in [PHP
RP](http://www.gluu.co/php-sample-rp).

If you cannot get the developer to help themselves, or if your domain
doesn't want to allow dynamic client registration, you can use the
oxTrust admin GUI to manually add trusted clients.

Available **Clients** can be seen by hitting the **Search** button
leaving the search box empty.

![Client List](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_clientlist.png)

A new client can be added by clicking the **Add Client** link.

![Add Client](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_addclient.png)

Clicking on the _Add Client_ link allows the Gluu Server administrator
to add a new client. The search box can be used to look up previously
added clients as well. The screenshot below shows the interface to add a
new client.

![Add new client](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_newclient.png)

* _Client Name:_ This contains the recognizable display name
  of the client, which is presented to the End-User in the authorization
  dialogue.

* _Client Secret:_ This is the Data Encryption Standard scheme used by
  Confidential Clients to authenticate to the token endpoint. The value for
  the secret can be inserted manually, but it is highly recommended to use
  the Dynamic Client Registration Endpoint. The Gluu oxAuth provides a
  random, generated Client Secret in the Dynamic Client Registration
  procedure.

* _Application Type:_ There are two types of applications, Web and
  Native. The default, if omitted, is web when using the Dynamic
  Client Registration Endpoint. The different configuration for the
   different application types are given below.

	* _Web:_ The Dynamic Client Registration is the default for web. In
    this type the redirect_uri for implicit grant type must be a real
    hostname with HTTPS. This type is not approved any localhost or HTTP.
    The web application uses the authorization code flow for clients which
    can maintain a client secret between the uris and the authorization
    server.

	* _Native:_ Custom uri for Native type application have to follow HTTP
    with localhost. This is suitable for a mobile app which cannot maintain
    the client secret between itself and the authorization server.

* _Pre Authorization:_ The Gluu Server disables this option by default,
  but it is possible to allow pre-authorized Client Applications according to the
  Organization Policy by the Gluu Server administrator.

* _Logo URI:_ The URL of the logo for the client application.
  If present, the server will display this image to the End-User during approval.

* _Client URI:_ The URL of the home page of the client.

* _Policy URI:_ URL that the Relying Party Client provides to the End-User to read about
  the how the profile data will be used. The value of this field must point
  to a valid web page. The OpenID Provider will display this URL to the End-User if it is given.

* _Terms of Service URI:_ URL that the Relying Party Client provides to the End-User to
  read about the Relying Party's terms of service. The value of this field must point to
  a valid web page. The OpenID Provider will display this URL to the End-User if it is given.

* _JWKS URI:_ The URL for the Client's JSON Web Key Set document.
  If the Client signs requests to the Server, it contains the signing key(s) the Server uses to
  validate signatures from the Client. The JWK Set may also contain the Client's encryption keys(s),
  which are used by the Server to encrypt responses to the Client.
  When both signing and encryption keys are made available, a use (Key Use) parameter value is
  required for all keys in the referenced JWK Set to indicate each key's intended usage.
  Although some algorithms allow the same key to be used for both signatures and encryption,
  doing so is NOT RECOMMENDED, as it is less secure.
  
* _JWKS:_ Client's JSON Web Key Set document, passed by value.
  The semantics of the jwks parameter are the same as the jwks_uri parameter, other than that the
  JWK Set is passed by value, rather than by reference.
  This parameter is intended only to be used by Clients that, for some reason, are unable to use
  the jwks_uri parameter, for instance, by native applications that might not have a location to
  host the contents of the JWK Set.
  If a Client can use jwks_uri, it must not use jwks. One significant downside of jwks is that it
  does not enable key rotation (which jwks_uri does).
  The jwks_uri and jwks parameters MUST NOT be used together.

* _Sector Identifier URI:_ URL using the https scheme to be used in calculating Pseudonymous
  Identifiers by the OP.
  The URL references a file with a single JSON array of redirect_uri values.
  Providers that use pairwise sub (subject) values should utilize the sector_identifier_uri
  value provided in the Subject Identifier calculation for pairwise identifiers.
  
* _Subject Type:_ The subject type requested for responses to this Client.
  The subject_types_supported Discovery parameter contains a list of the
  supported subject_type values for this server. Valid types include pairwise and public.

* _JWS alg Algorithm for signing the ID Token:_ JWS alg algorithm for signing the ID Token issued to this Client.
  See [Algorithms section](#algorithm) for options.

* _JWE alg Algorithm for encrypting the ID Token:_ JWE alg algorithm for encrypting the ID Token issued to this Client.
  See [Algorithms section](#algorithm) for options.

* _JWE enc Algorithm for encrypting the ID Token:_ JWE enc algorithm for encrypting the ID Token issued to this Client.
  See [Algorithms section](#algorithm) for options.

* _JWS alg Algorithm for signing the UserInfo Responses:_ JWS alg algorithm for signing UserInfo Responses.
  If this is specified, the response will be JWT serialized, and signed using JWS.
  The default, if omitted, is for the UserInfo Response to return the Claims as a UTF-8 encoded JSON object
  using the application/json content-type.
  See [Algorithms section](#algorithm) for options.

* _JWS alg Algorithm for encrypting the UserInfo Responses:_  JWE alg algorithm for encrypting UserInfo Responses.
  See [Algorithms section](#algorithm) for options.

* _JWE enc Algorithm for encrypting the UserInfo Responses:_ JWE enc algorithm for encrypting UserInfo Responses. 
  See [Algorithms section](#algorithm) for options.

* _JWS alg Algorithm for signing Request Objects:_ JWS alg algorithm used for signing Request Objects sent to the OP.
  This algorithm is used both when the Request Object is passed by value (using the request parameter) and when it is
  passed by reference (using the request_uri parameter).
  The default, if omitted, is that any algorithm supported by the OP and the RP can be used.
  The value none can be used.
  See [Algorithms section](#algorithm) for options.

* _JWE alg Algorithm for encrypting Request Objects:_ JWE alg algorithm the RP is declaring that it use for
  encrypting Request Objects sent to the OP.
  See [Algorithms section](#algorithm) for options.

* _JWE enc Algorithm for encrypting Request Objects:_ JWE enc algorithm the RP is declaring that it may use for
  encrypting Request Objects sent to the OP.
  See [Algorithms section](#algorithm) for options.

* _Authentication method for the Token Endpoint:_ Requested Client Authentication method for the Token Endpoint.
  The options are client_secret_post, client_secret_basic, client_secret_jwt, private_key_jwt, and none.
  If omitted, the default is client_secret_basic, the HTTP Basic Authentication Scheme.

* _JWS alg Algorithm for Authentication method to Token Endpoint:_ JWS alg algorithm used for signing the JWT
  used to authenticate the Client at the Token Endpoint for the private_key_jwt and client_secret_jwt
  authentication methods. The value none cannot be used.
  The default, if omitted, is that any algorithm supported by the OP and the RP can be used.
  See [Algorithms section](#algorithm) for options.

* _Default Maximum Authentication Age:_ Specifies that the End-User must be actively authenticated if the End-User was
  authenticated longer ago than the specified number of seconds.
  If omitted, no default Maximum Authentication Age is specified.

* _Require Auth Time:_ Specifies whether the auth_time Claim in the ID Token is required.
  If omitted, the default value is false.

* _Persist Client Authorizations*:_ Specifies whether to persist user authorizations.

* _Initiate Login URI:_ URI using the https scheme that a third party can use to initiate a login by the RP.

* _Request URIs:_ Array of request_uri values that are pre-registered by the RP for use at the OP.
   The Server cache the contents of the files referenced by these URIs and not retrieve them at
   the time they are used in a request.
   If the contents of the request file could ever change, these URI values should include the base64url
   encoded SHA-256 hash value of the file contents referenced by the URI as the value of the URI fragment.
   If the fragment value used for a URI changes, that signals the server that its cached value for that URI
   with the old fragment value is no longer valid. 

* _Logout URIs:_ Redirect logout URLs supplied by the RP to which it can request that the End-User's
  User Agent be redirected using the post_logout_redirect_uri parameter after a logout has been performed.

* _Logout Session Required*:_ Specifies whether the RP requires that a sid (session ID) query parameter
  be included to identify the RP session at the OP when the logout_uri is used.
  If omitted, the default value is false.

* _Client Secret Expires:_ Time at which the client will expire or 0 if it will not expire.

**Buttons at the bottom**

* _Add Login URI:_ This option can be used to add the login URL.
![Add Login URI](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth_loginuri.png)

* _Add Scopes:_ This option can be used to add the required scopes in the Gluu Server.
![Add Scopes](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_addscope.png)

  The available scopes can be listed by hitting the *Search* button, and
  keeping the search phrase blank. Furthermore, from this the Gluu Server
  administrator can select the required scopes.

* _Add Response Type:_ There are three types of responses in the Gluu
  Server and they are Code, Token and ID Token. The Gluu Server
  Administrator can select all of them for testing purposes.
![Response Type](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_response.png)

* _Add Grant Type:_ There are 3 grant type available in this option `authorization_code, implicit, refresh_token`
![Grant Type](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_grants.png)

* _Add Contact:_ Use this option to add the email address for the Client contact

* _Add Default ACR value:_ Use this option to define the default ACR Value. This value is used to include multi-factor authentication in registered clients.

* _Add Request URI:_ Use this option to add the Request URI

### Multi-Factor Authentication for Clients
The `acr_values` parameter is used to specify the use of specific multi-factor authentication for each client. If a scenario is presented where different clients use different authentication mechanism, then the `acr_value` parameter is used to specify the choice. Out of the box, GLuu Server supports U2F, DUO, Basic, oxPush/SuperGluu, Google+ and internal LDAP authentication. While registering new clients, put the mode in `Add Default ACR value` to chosen mechanism. The authentication mechanism must be enabled in the `Custom Scripts` section as well.

**Supported ACR Values in Client Registration: "u2f", "duo", "basic", "mt", "oxpush2", "gplus", "internal"**

The values appear in order of preference and the successful authentication is sent as the acr claim value in the issued ID Token. The table below explains the acr values. Please click on the description to access the specific how-to guide for the ACR declared authentication.

|  ACR Value  	| Description			|
|---------------|-------------------------------|
|  u2f		| [FIDO U2F Device](../multi-factor/u2f)|
|  duo		| [Duo soft-token authentication](../multi-factor/duo)|
|  basic	| Username/Password authentication from LDAP Server|
|  oxpush2	| [Multi-factor authentication](../multi-factor/oxpush2)|
|  gplus	| [Google+ authentication](../customize/social-login-google)|
|  internal	| Use Gluu Server LDAP to authenticate users|

### Algorithm
oxAuth supports various types of signature and encryption
algorithms for authorizing request parameter passing, ID token signature
and encryption, signing return responses, Encrypt User Info Endpoints
etc.

**Note:** It is a good practice to implement ID Token Signatures with the RSA
SHA-256 algorithm (algorithm value RS256). Additionally, oxAuth also
supports other algorithms that are listed below.

_Available Signature Algorithms:_ none, HS256, HS384, HS512, RS256, RS384, RS512, ES256, ES384, ES512.

_Encryption, Key Encryption Algorithms:_ RSA1_5, RSA-OAEP, A128KW, A256KW.

_Block Encryption Algorithms:_ A128CBC+HS256, A256CBC+HS612, A128GCM, A256GCM,

### Custom Client Registration

Using interception scripts you can customize client registration
behavior. For example, by default oxAuth allows new clients to access to
default scopes only. With a custom client registration interception
script it is possible to allow access to more scopes. For instance, we
can use `redirect_uri` to determine if we need to allow access to
additional scopes or not.

To access the interface for custom scripts in oxTrust, navigate to
Configuration --> Custom Scripts --> Custom Client Registration.

Take a look at our [example client registration
script](../customize/sample-client-registration-script.py)
for further reference.

### Search clients
![](http://www.gluu.org/docs/img/openid_connect/oxtrust_search_clients.png "Screenshot of oxTrust browse / search clients")

### View client

![](http://www.gluu.org/docs/img/openid_connect/oxtrust_view_client.png "Screenshot of oxTrust view client")

## Session management

OpenID Connect lets the relying party track whether the end user is logged in at the provider, and also initiate end user logout at the provider. The specification has the relying party monitor session state using an invisible iframe and communicate status using the HTML 5 postMessage API.

However, be forewarned that there is no perfect answer to logout that
satisfies all requirements for all domains on the Internet. For
example, large OpenID Providers, like Google, need a totally stateless
implementation--Google cannot track sessions on the server side for
every browser on the Internet. But in smaller domains, server side
logout functionality can be a convenient solution to cleaning up
resources.

The OpenID Connect [Session
Management](http://openid.net/specs/openid-connect-session-1_0.html) is
still marked as draft, and new mechanisms for logout are in the works.
The current specification requires JavaScript to detect that the session
has been ended in the browser. It works... unless the tab with the
JavaScript happens to be closed when the logout event happens on another
tab. Also, inserting JavaScript into every page is not feasible for some
applications. A new proposal is under discussion where the OpenID
Connect logout API would return `IMG` HTML tags to the browser with the
logout callbacks of the clients. This way, the browser could call the
logout uris (not the server).

The Gluu Server is very flexible, and supports both server side session
management, and stateless session management. For server side
logout, the domain admin can use [Custom Logout scripts](./custom-script.md#application-session-management). This can be
useful to clean up sessions in a legacy SSO system (i.e. SiteMinder), or
perhaps in a portal.

The key for logout is to understand the limitations of logout, and to
test the use cases that are important to you, so you will not be
surprised by the behavior when you put your application into production.

## OpenID Connect Relying Party Registration
Relying parties can register with the Gluu Server both statically, by the Gluu Server admin, and dynamically, as specified by OpenID Connect Discovery. To allow dynamic registration, you register an initial OAuth 2.0 client that other relying parties can use to get access tokens for registration. You can also enable OpenID Connect relying parties to register dynamically without having to provide an access token. If dynamic registration is enabled, make sure to limit or throttle registrations as it could be used as a form of DDOS.

# Client Code
Although you can use generic OAuth 2.0 client libraries to call OpenID Connect endpoints, you would have to implement code to take advantage of some of OpenID Connect's features. For example, there is no id_token in OAuth 2.0, so you won't find any code for id_token validation in an OAuth 2.0 library. A good OpenID Connect client will do much of the heavy lifting for you. 

## JavaScript Client
A JavaScript client is one of the easiest ways to use OpenID Connect, although it's not the most secure. The client we recommend was forked from a sample application written to demonstrate how easy it is to use Connect. Gluu forked the code, and has enhanced it since the time of its original publishing. The project can be found on [Github](https://github.com/GluuFederation/openid-implicit-client).

It's not a fancy app--it sends the person to the authorization endpoint to be authenticated, and then prints the claims tha are returned in the id_token. Currently the client does not handle dynamic client registration. 

You'll have to add the client manually to the Gluu Server via the GUI. When completing the `add client` form, you can use the following configuration:

```
Client Name: Implicit Test Client
response_type: token id_token
Application Type: Web
Pre-Authorization: Enabled
Subject Type: public
Scopes: openid, profile, email
Response Types: token id_token
Grant Types: implicit
```

Once you have registered the client in the Gluu Server, all you need to do is update the `client_id`, `redirect_uri`, and `providerInfo` values in the login page html. Assuming you've checked out the project into a web accessible folder, then navigate to the page and test! 

## Server-Side libraries
Many applications are "server-side", meaning the web page displays content but most of the dynamic business logic resides on the web server. The OpenID Foundation maintains a list of client libraries on [their website](http://openid.net/developers/libraries). However, our experience has been that the quality of these libraries varies widely. Some are not well documented, other are not updated frequently, and some do not implement essential security features available in OpenID Connect. In addition, if a wide array of client libraries are used it becomes difficult to monitor and patch security vulnerabilities. For this reason, we recommend that you use our OpenID Connect middleware software called [oxd](http://oxd.gluu.org).  

oxd is not open source, but it is very reasonably priced at $0.33 per day per server--or ~$10/month. The code is available on [GitHub](https://github.com/gluufederation/oxd), and there are free open source oxd libraries available for PHP, Java, Python, C#, Node, Ruby, Perl and Go. There are also plugins available for several popular open source applications.

[Watch the oxd demo](http://gluu.co/oxd-demo).

[Get an oxd license for free](http://oxd.gluu.org)

## Apache HTTPD module
A popular approach to protecting web applications is to use a web server filter to intercept the request, and make sure the person using that connection is authenticated and authorized. The web server with the filter may directly serve the application, or may proxy to a backend service. Leveraging the web server is a well established pattern, used by older access management platforms like CA Siteminder and Oracle Access Manager. 

One of the advantages of the web server filter approach is that the application developer does not need to know that much about the security protocols--if the request makes it through to the application, the person has been authenticated and the request is authorized. Another advantage is that the application security is administered by the system administrators, not by developers. For example, it may be easier to manage and audit apache configuration than to read a bunch of code. 

One of the best OpenID Connect relying party implementations was written by Hans Zandbelt, called [mod_auth_openidc](https://github/com/pingidentity/mod_auth_openidc). It is an authentication and authorization module for the Apache 2.x HTTP server that authenticates users against an OpenID Connect Provider (OP). The software can be found on GitHub and is included in the package management system for several Linux distributions. There are binary packages available, and if you are good at compiling C code, you can build it yourself from the source. 

Note: if you are an Nginx fan, there is a similar [Lua implementation](https://github.com/pingidentity/lua-resty-openidc) to make NGINX operate as an OpenID Connect RP or OAuth 2.0 RS. 

## AppAuth for Mobile Applications
One of the most compelling reasons to use Connect is to authenticate people from a mobile application. The IETF draft ["OAuth 2.0 for Native Apps"](https://tools.ietf.org/html/draft-ietf-oauth-native-apps-06) provides an overview of an improved design for mobile security. In additio to the security features of OpenID Connect, this draft suggests the use of a PKCE and custom URI schemes (i.e. an application can register a URI such as myapp:// instead of https://).

In 2016, Google released and then donated code to the OpenID Foundation called AppAuth for [Android](https://github.com/openid/AppAuth-android) and [iOS](https://github.com/openid/AppAuth-iOS). The AppAuth projects also include sample applications. Simulataneously, Google announced that it was deprecating the use of WebViews--a strategy used by mobile app developers which is vulnerable to malicious application code. Not only does AppAuth provide secure authentication, it enables SSO across the system browser and mobile applications. It accomplishes this by leveraging new operating system features that enable the system browser to be called by an application in an opaque view that does not enable an app developer to steal a person's credentials, or other applications to steal codes or tokens. Using this approach, mobile app developers can use the authorization code or hypbrid flow (as described earlier). 

The Gluu Server is the only free open source OpenID Connect Provider that currently supports AppAuth. 

# oxAuth RP

The Gluu Server ships with an optional OpenID Connect relying party web application, which is handy for testing.  It's called oxauth-rp. During Gluu Server setup, you'll be asked if you want to install it--which you should on a development environment. It will be deployed on `https://<hostname>/oxauth-rp`. Using this tool you can exercise all of the OpenID Connect API's, including discovery, client registration, authorization, token, userinfo, and end_session. 

# oAuth 2 Grants

There are two additional flows that the Gluu Server supports for user
and client authentication, which are not part of the OpenID Connect
specification. The flows are explained in the following page.

* [oAuth 2 Grants](./oauth2grants.md)
