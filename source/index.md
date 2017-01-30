# Gluu Server Community Edition (CE) Docs
The Gluu Server is a free open source identity and access management 
(IAM) platform. The most common use case for the Gluu Server is Single 
Sign-On (SSO). Other common use cases include mobile authentication, 
API access management, two-factor authentication, customer identity
and access management (CIAM), and identity federation. 

The Gluu Server is a container distribution composed of software
written by Gluu and incorporated from other open source projects. Gluu
projects are frequently prefixed with **ox**, which is our open source
handle. Any code in the Gluu Server that we wrote is MIT license, 
and is available on [Github](https://github.com/GluuFederation/). 

SaaS, custom, open source and commercial software can be made more 
secure by leveraging a central authentication and authorization service. 
Because there are so many different kinds of apps, there is no way to 
"top down" implement proprietary security mechanisms. This is why
open standards are so important for IAM. Also, we don't want to lock you into 
the Gluu Server!

While there are many open protocols for IAM, Gluu focuses on just a few. 
Consolidation saves money, and one-off integrations should be avoided. 
Our goal was to support the most widely adopted older protocols, and the 
most promising new protocols. 

Currently the Gluu Server supports the following open web standards:

- OAuth 2.0    
- SAML 2.0   
- OpenID Connect    
- User Managed Access (UMA)    
- Simple Cloud Identity Management (SCIM)    
- FIDO Universal 2nd Factor (U2F)    
- Lightweight Directory Access Protocol (LDAP)   

If this is your first exposure to the Gluu Server, welcome to the 
community! We want to see the ecosystem flourish, and ultimately to make 
the Internet a safer, more privacy protected place. In order to do that, 
we believe we need to keep the Gluu Server free, so all kinds of 
organizations can use, contribute and benefit from the software. We 
couldn't do it without you! 

These docs are not perfect! Please help us make them so by submitting
any improvements to our [Documentation Github](https://github.com/GluuFederation/docs-3)!
If you're a Github pro, submit a pull request. If not, just open an issue
on any typos, bugs, or improvements you'd like to see. We need your
help... even if you're not a coder, you can contribute! 

###  oxd Client Software
Gluu offers commercial client software, called [oxd](https://oxd.gluu.org), to make securing applications easier. Your application can use any client software that implements the open standards the Gluu Server supports. But you may want to consider using oxd for the following reasons:
 
(1). oxd is super-easy and fun to use; 

(2). We keep updating oxd to address the latest security knowledge; 

(3). We can provide more complete end-to-end support if we know both 
the client and server software;

(4). oxd subscriptions help support this project, 
so you can see more enhancements faster; 

(5). There are oxd libraries for Php, Python,
Java, Node, Ruby, C#, Perl and Go; 

(6). There are oxd plugins for many popular open source projects like Wordpress, Drupal, Magento, OpenCart,
SugarCRM, SuiteCRM, Roundcube, Shopify, Kong and many more are being added! Next on the list are MatterMost, RocketChat, NextCloud, and 
Liferay.

###  Super Gluu multi-factor authentication
Gluu offers a free two-factor authentication mobile application for iOS and Android called [Super Gluu](https://super.gluu.org). Super Gluu can be used to achieve multi-factor authentication to applications that send users to a Gluu Server for login. The Gluu Server includes support for Super Gluu out-of-the-box. 

Super Gluu supports two workflows: It can be used as a one-step authentication to a website, where the person scans a QR code, and the Gluu Server looks up which person is associated with that phone. It can also be used for a two-step authentication, where the person logs into a website with a username and password, and then receives an out-of-band (OOB) push notification to the mobile device to authorize access. 

Learn [how to enable](./authn-guide/supergluu.md) Super Gluu in the Gluu Server.

Learn [how to use](https://super.gluu.org/docs) the Super Gluu mobile application.

In addition to Super Gluu, the Gluu Server can be configured to support any third-party authentication mechanism that either supports the FIDO U2F authentication standard, or exposes a web API that can be called over the Internet. Learn more in the [user authentication introduction](https://gluu.org/docs-3/admin-guide/user-authentications/). 

### Support

We are committed to free community support! You can browse or register and post 
questions on our [support site](https://support.gluu.org). All community
questions are public, and we do our best to answer them in a timely 
manner. 

Private support, guaranteed response times, and consultative 
support are available to organizations who purchase a support contract. For
more information, see [our website](gluu.org/pricing).

### License

All of Gluu's open source software is published under an
[MIT License](http://opensource.org/licenses/MIT). The licenses 
for other components are listed below.

|	Component	|	License	            |
|-----------------------|---------------|
|	Shibboleth IDP      | [Apache2](http://www.apache.org/licenses/LICENSE-2.0)|
|	OpenLDAP	        | [OpenLDAP Public License](http://www.openldap.org/software/release/license.html)|
|	Asimba		        | [GNU APGL 3.0](http://www.gnu.org/licenses/agpl-3.0.html)|
|	OpenDJ		        | [CDDL](https://forgerock.org/cddlv1-0/)|
|  UnboundID LDAP SDK	| [UnboundID LDAP SDK Free Use License](https://github.com/UnboundID/ldapsdk/blob/master/LICENSE-UnboundID-LDAPSDK.txt)|
| Passport-JS           | [MIT License](https://github.com/jaredhanson/passport/blob/master/LICENSE) |
| Jetty / Apache HTTPD  | [Apache2](http://www.apache.org/licenses/LICENSE-2.0)|
