# Testing Asimba with Gluu Server
This guide outlines how to test Asimba with Gluu Server.
The authentication flow for this test is as follows
**[https://sp.gluu.org] --> [https://upgrade.gluu.org] -->[https://test.gluu.org] -->[https://upgrade.gluu.org] -->[https://sp.gluu.org]**

## Required Setup

|Setup hostname|Description|
|--------------|-----------|
|https://sp.gluu.org|This is a shibboleth SP connected to _https://upgrade.gluu.org_|
|https://upgrade.gluu.org| This is a Gluu Server SAML IdP with Asimba|
|https://test.gluu.org|This is a second Gluu Server SAML IdP connected to _https://upgrade.gluu.org_ |

**Note:** Ideally all SPs and IdPs should be connected to Asimba server. 
In this case we are following that rule as well.

## https://sp.gluu.org Setup
Please follow the following steps to setup https://sp.gluu.org.

* Install Shibboleth SP following the guides available for 
[CentOS](./integration/saml-sp/#configuring-apache-shibboleth-sp-in-centos) 
or [Ubuntu](./integration/saml-sp/#super-quick-ubuntu-shib-apache-install).

* Configure `shibboleth2.xml` to include the metadata and metadata link 
for the Asimba Server, in this case _https://upgrade.gluu.org_<br/>
Two code snippets are given below <br/>
```
<SSO entityID="https://upgrade.gluu.org/asimba/profiles/saml2"
```
```
<MetadataProvider type="XML" validate="true" file="/etc/shibboleth/asimba_metadata.xml"/>
```
**Note:** Deployer need to download Asimba server's metadata inside SP and provide the absolute path in `MetadataProvider` section

## https://upgrade.gluu.org setup
* Install Gluu Server with Asimba following the [Deployment Guide](../installation-guide/install.md) 
and select 'Asimba' during installation. 

### Add IdP
* Add `https://upgrade.gluu.org`, as self IdP, and `https://test.gluu.org`, 
as remote IdP, inside Asimba server as authentication servers. 
**N.B.:** In the screenshot given below, `https://upgrade.gluu.org/idp/shibboleth` 
is added as one of the authentication servers. Follow this template to add 
`https://test.gluu.org` as well.
![image](../img/admin-guide/asimba/asimba.png)

**Note:** The certificates below can be found in the `/etc/certs/` 
folder in the Gluu Server CE environment

* Convert `shibIDP.crt` to `shibIDP.der`
   - code: ```openssl x509 -outform der -in shibIDP.crt -out shibIDP.der```

* Import abvoe DER into the `asimbaIDP.jks`
   - code: ```keytool -importcert -file shibIDP.der -keystore asimbaIDP.jks -alias <entityID_of_ID>```

* Restart  oxauth and identity Service using below commands:

```
    # service identity stop
    # service identity start
    
    # service oxauth stop
    # service oxauth start
    
```
### Add SP
* Navigate to `Configuration` > `SAML` > `Asimba` > `SP Requestors` 
![image](../img/admin-guide/asimba/sp-requestor.png)

* Click on Add SP Requestor 

![image](../img/admin-guide/asimba/add-sp-requestor.png)

* Download the SP Metadata from _https://sp.gluu.org_ and provide 
the absolute path link in the Metadata File location 
![image](../img/admin-guide/asimba/add-sp-requestor1.png)

* Click `Update` and Restart identity and oxauth Server

## https://test.gluu.org setup
In this Gluu Server, add the Asimba Server, _https://upgrade.gluu.org_ as a 
trusted party through a Trust Relationship.

* Click on Add Trust Relationship 
![image](../img/admin-guide/asimba/admin_saml_create.png)

* Setup the Trust Relationship as given below in the screenshot
![image](../img/admin-guide/asimba/tr.png)

* Configure Relaying Party
![image](../img/admin-guide/asimba/rp_configuration.png)
