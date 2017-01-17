# What's new in Version 3?

We've made some big changes to Gluu Sever 3.0 to make it more modern, 
faster and easier to manage. Following is an overview of these changes.

## Jetty replaces Tomcat as servlet container

Here are some of the reasons we made this change

 - Memory management: easier to allocate memory per app.
 - Restart: Easier to restart for individual components, without affecting
   others. For example, Asimba requires more restarts when some
   configuration is updated.
 - Logs: `wrapper.log` was getting to busy. It's better to have
   the top-level log smaller. See [logs management](../admin-guide/logs.md) 
   for more informatoin.
 - Network: oxAuth is Internet facing; oxTrust is an admin application
   which may be internal facing.
 - Docker: Deploying each application in it's own servlet container 
   aligns with our strategy to deploy each application in its own 
   container.

## OpenDj Vs OpenLDAP

Gluu uses LDAP for persistence. While we will continue to support 
several LDAP servers, we will now ship with OpenLDAP. Here are a few
reasons we made that decision.

 - OpenLDAP has better license, and Symas (the company behind OpenLDAP),
   has a clear commitment to free open source software.
 - After OpenLDAP LMDB backend is super fast and crash-resistant 
 - Less impact on Java Garbage collection.
 - Affordable support options from Symas.
 - Proxy Capabilities: Using OpenLDAP Gold, which is a commercial 
   distribution from Symas, we can break data into different replicated 
   topologies, and use the proxy to route operations. Using this strategy
   we can increase the write performance of the ldap service. 

## Shibboleth IDP version 3

 - Re-architected to use Spring
 - Version 2.0 was end of life
 - For more information, see the [Release Notes](https://wiki.shibboleth.net/confluence/display/IDP30/ReleaseNotes)

## New Features

 - Passport.js component makes over 300 websites for social login. See
   the [Passport](../authn-guide/passport.md) docs page for more information.
 - One Time Password authentication: Using any standard HOTP or TOTP OATH 
   software, like [Google Authenticator](https://support.google.com/accounts/answer/1066447?hl=en).
 - Centralized logging, useful for clusters.
 - Improved audit logging capabilities for OAuth 2.0