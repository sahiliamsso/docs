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
standards are so important for IAM. Also, we don't want to lock you into 
the Gluu Server!

While there are many open protocols for IAM, Gluu focuses on just a few. 
Consolidation saves money, and one-off integrations should be avoided. 
Our goal was to support the most widely adopted older protocols, and the 
most promising new protocols.

If this is your first exposure to the Gluu Server, welcome to the 
community! We want to see the ecosystem flourish, and ultimately to make 
the Internet a safer more privacy protected place. In order to do that, 
we believe we need to keep the Gluu Server free, so all kinds of 
organizations can use, contribute and benefit from the software. We 
couldn't do it without you! 

These docs are not perfect! Please help us make them so by submitting
any improvements to our [Documentation Github](https://github.com/GluuFederation/docs-3)!
If you're a Github pro, submit a pull request. If not, just open an issue
on any typos, bugs, or improvements you'd like to see. We need your
help... even if you're not a coder, you can contribute! 

###  oxd Client Software
Gluu offers commercial client software. Your application can use any 
client software that implements the open standards we support. But you 
may want to consider using [oxd](https://oxd.gluu.org) for a few reasons:
 
(1). we tried to make it super-easy and fun to use. 

(2). we keep updating it to address the latest security knowledge. 

(3). we can provide more complete end-to-end support if we know both 
the client and server software.

(4). oxd subscription revenue helps provide money to support this project, 
so you can see even more enhancements even faster! [oxd](https://oxd.gluu.org) has libraries for Php, Python,
Java, Node, Ruby, C#, Perl and Go. We also have oxd plugins for many
popular open source projects like Wordpress, Drupal, Magento, OpenCart,
SugarCRM, SuiteCRM, Roundcube, Shopify, Kong and many more are being 
added! Next on the list are MatterMost, RocketChat, NextCloud, and 
Liferay.

### Support

We are committed to free community support, just register and post your 
questions on our [Support site](https://support.gluu.org). All community
questions are public, and we do our best to answer them in a timely 
manner. 

Private support, guaranteed response times, and consultative 
support are available to organizations who purchase a contract. For
more information, see [our website](gluu.org/pricing).

### License

Gluu's open source software is 
[MIT License](http://opensource.org/licenses/MIT) license. The licenses 
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
