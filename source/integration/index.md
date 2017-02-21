# Gluu Server Integration Guide

The integration guide includes three sections that will help you integrate custom developed, open source, off-the-shelf, and popular SaaS applications with your central Gluu Server authentication and authorization service.  

## SaaS Applications 
SaaS integrations are fairly straightforward. Presumably the app in question already supports either SAML or OpenID Connect and provides documentation for configuring your IDP (Gluu Server) for SSO. We have documentation for configuring a few very popular SaaS applications like Google and Salesforce. 

If we do not have a guide for configuring the app in question, simply goolge `{SaaS Provider} SAML` or `{SaaS Provider} OpenID Connect`. Follow the provider's instructions for configuring your IDP for SSO and test. 

## Non-SaaS Applications

Two design patterns have emerged for securing custom developed, open source, and off-the-shelf applications:

1. Use a web server filter / reverse proxy; or,
2. Call the federation APIs directly in your application with the help of Client SDKs.

In this integration guide we document how to use supported software to implement both approaches. Which to pick depends on a trade-off between easier devops (option 1), and how deeply you want to integrate centralized security policies into your application (option 2).

### Web Server Filter / Reverse Proxy
The most commonly used approach for enterprise SSO has been the Web Server Filter / Reverse Proxy option where you install an Apache Web Server “mod”, or an IIS “ISAPI Filter” to enforce the presence of a token in a HTTP Request. If no token is present, the Web server may re-direct the person, or return a meaningful code or message to the application. 

### Client SDKs
The other option is to use Client SDKs to call the federation APIs directly in your application. In general, calling the API’s directly will enable the application to make “smarter” decisions. For example, you could implement transaction level security more easily. This can have a positive impact on usability. Giving developers more ability to leverage centralized policies may also increase re-use of policies, and ultimately result in better security.

!!! Note
    Given the security implications of getting the API implementation correct, we strongly encourage you to use our commercial OAuth 2.0 client software: [oxd](./oauth2/). 
    
