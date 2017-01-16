# Gluu Server Community Edition (CE) Docs
The Gluu Server is a free open source identity and access management 
(IAM) platform. The most common use case for the Gluu Server is Single 
Sign-On (SSO). Other common use cases include mobile authentication, 
API access management, two-factor authentication, customer identity
and access management (CIAM), and identity federation. 

The Gluu Server is container distribution that is composed of software
written by Gluu and incorporated from other open source projects. Gluu
projects are frequently prefixed with **ox**, which is our open source
handle. Any code in the Gluu Server that we wrote is MIT license, 
available on [Github](https://github.com/GluuFederation/). 

There is a wide array of applications that need to use a centralized 
authentication and authorization service. The security of SaaS, custom, 
open source and commercial software can be improved by levering a central
authentication and authorization service. Due to this diversity, Gluu 
only supports open standards. There is no way to "top down" implement 
security on applications that you didn't write. Also, we don't want to 
lock you into the Gluu Server! 

While there are many open protocols for IAM, Gluu focuses on just a few. 
Consolidation saves money, and one-off integrations should be avoided. 
Our goal was to support the most widely adopted protocols, and the 
most promising new protocols.

If this is your first exposure to the Gluu Server, welcome to the 
community! Gluu is dedicated to keeping the Gluu Server free, to
help this ecosystem flourish, and ultimately to make the Internet
a safer place!

These docs are not perfect! Please help us make them so by submitting
any improvements to our [Documentatoin Github](https://github.com/GluuFederation/docs-3)!
If you're a github pro, submit a pull request. If not, just open an issue
on any typos, bugs, or improvements you'd like to see. We need your
help... even if you're not a coder, you can contribute! 

# oxd Client Software
Gluu offers commercial client software. Your application can use any
software that supports the open standards we implemented. But you may 
want to consider using [oxd](https://oxd.gluu.org) for a few reasons: 
(1) we tried to make it super-easy and fun to use! (2) we keep updating
it to address the latest security knowledge; (3) we can provide more
complete end-to-end support if we know both the client and server 
software; (4) using our commercial client software helps provide money
to support this project, so you can see even more enhancements even
faster! [oxd](https://oxd.gluu.org) has libraries for Php, Python,
Java, Node, Ruby, C#, Perl and Go. We also have oxd plugins for many
popular open source projects like Wordpress, Drupal, Magento, OpenCart,
SugarCRM, SuiteCRM, Roundcube, Shopify, Kong and many more are being 
added even as your read this! 

# Support

We are committed to free community support, just register and post your 
question on our [Support site](https://support.gluu.org). All community
questions are public, and we do our best to answer them in a timely 
manner. Private support, guaranteed response times, and consultative 
support is available to organizations who purchase a contract. For
more information, see [our website](gluu.org/pricing).

# License

Software used in the Gluu Server is 
[MIT License](http://opensource.org/licenses/MIT) license. The license for 
other components are listed below.

During installation you will also have the option to install third party software components which have the following licenses:

|	Component	|	License	            |
|-----------------------|---------------|
|	Shibboleth IDP      | [Apache2](http://www.apache.org/licenses/LICENSE-2.0)|
|	OpenLDAP	        | [OpenLDAP Public License](http://www.openldap.org/software/release/license.html)|
|	Asimba		        | [GNU APGL 3.0](http://www.gnu.org/licenses/agpl-3.0.html)|
|	OpenDJ		        | [CDDL](https://forgerock.org/cddlv1-0/)|
|  UnboundID LDAP SDK	| [UnboundID LDAP SDK Free Use License](https://github.com/UnboundID/ldapsdk/blob/master/LICENSE-UnboundID-LDAPSDK.txt)|
| Passport-JS           | [MIT License](https://github.com/jaredhanson/passport/blob/master/LICENSE) |
| Jetty / Apache HTTPD  | [Apache2](http://www.apache.org/licenses/LICENSE-2.0)|
