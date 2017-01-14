#Release Changes

This section of the document will discuss about the changes in the release and its features. 

Gluu Server 3.0.0 has built with few new components which wasn't in its predecessors. With these changes and new components Gluu Server 3.0.0 has significant changes in commands, logs and path to libraries and jar. All these changes will be described in the next few sections.

## New Component Changes in Gluu Server CE 3.0.0

- Tomcat has been replaced with Jetty
- OpenDj is replaced with OpenLDAP
- Upgraded shibboleth IDP has been incorporated ad default outbound SAML service.

## Tomcat Vs Jetty
***Why Jetty over Tomcat as our application server?***

Here are the reason why we switched over to Jetty in place of Tomcat.

### Matches Gluu's container strategy

Jetty matches Gluu's container strategy lot more better than Tomcat, where each app which is incorporated (Identity,oxauth,Asimba, cas,passport, apache,etc) in Gluu can be deployed separately.

By which its gives more leverage to work on each app exclusively and restart the particular app, rather than restarting the whole Gluu Server.

### Manage memory per app

Since we have separated the apps container, it becomes easier to manage memory per app and provide memory as per usage of the app.

### Seperation of Logs

Logs have segregated according to the apps in separate folder and this section has been discussedelaborately under [logs management](../admin-guide/logs.md) section.

### Seperation Network made easy

- oxTrust is internal facing, where admin and admin assigned users and internal users could use the login UI
- oxAuth is internet facing. OxAuth is used by external users and used while multi-factor authentication is used.


# OpenDj Vs OpenLDAP

This version of the Gluu Server, includes the following new features to enable more security in SSO.

- Passport.js authentication, this method has been discussed in detail in [Passport](../authn-guide/passport.md) page
- HOTP/TOTP authentication.
- Improved centralized logging for clusters.
