# User Authentication Introduction

The Gluu Server is most frequently used to protect web-accessible resources. People navigate to a protected webpage and the application redirects the person to the Gluu Server for authentication and authorization. The Gluu Server determines who the person is, and whether the person has the right to access the protected page. The Gluu Server then redirects the user back to the protected page with an authenticated session.

The Gluu Server is very flexible in handling authentication. By default, the Gluu Server uses username and password authentication. However, using the Gluu Server's interception script infrastructure, you can define multiple authentication methods and business logic for complex multi-step authentication workflows. You can have multiple authentication mechanisms active at the same time--Web or mobile clients can request a certain authentication type by using standard OpenID Connect request parameters.

Interception scripts allow you to configure authentication processes and customize how they are applied. Sophisticated authentication logic can implement adaptive authentication. For example, you can add extra authentication steps based on contextual information such as fraud scores, location, or browser profiling. You can also customize the look and feel of a web authentication: html, css, images and javascript can be externalized and managed by your organization.

## Default Authentication

By default, LDAP is used to authenticate usernames and passwords. You can set a default authentication method for access to external applications, as well as access to the Gluu Server UI. Until additional authentication mechanisms are enabled via custom scripts, default authentication will always be some variation of username and password. 

## Configuring Social Authentication

During deployment of the Gluu Server you are presented with an option to deploy Passport.js. With over 300 existing "strategies", Passport.js provides a crowd-sourced approach to supporting social login at many popular consumer IDPs. Passport not only normalizes authentication, it also provides a standard mapping for user claims.

Learn [how to use Passport.js](../authn-guide/passport.md/) to configure social login. 

## Configuring Multi-Factor Authentication

A number of multi-factor authentication scripts are shipped in the Gluu Server by default, including support for FIDO U2F tokens (like Vasco and Yubikey), Gluu's free mobile two-factor application Super Gluu, certificate authentication, and Duo Security.  

## Configuring Account Lockout


## Customizing the Login Page 

Learn how to customize the look and feel of Gluu Server pages in the [Design Customizations](todo) section of the Operations Guide. 


