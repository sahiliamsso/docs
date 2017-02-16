# FIDO U2F

## Overview
FIDO Universal 2nd Factor (U2F) is an open authentication standard that strengthens and simplifies two-factor authentication using specialized USB or NFC devices based on similar security technology found in smart cards. Learn more about the U2F standard [on Gluu's website](https://www.gluu.org/resources/documents/standards/fido-u2f/).

The FIDO U2F script for the Gluu Server enables you to require that a user present their FIDO U2F compliant device in order to access a protected resource. The login can be configured as a one-step authentication, where you simply prompt for U2F authentication. Or it can be layered as a two-step authentication, where you first request a username and password and then a FIDO U2F device. 

Following the documentation below will implement a two-step authentication where the user is first required to enter their username and password, then enroll (on the first authentication) and present their FIDO U2F device to complete the authentication. 

Some well known U2F devices and manufacturers include:           
- [Vasco DIGIPASS SecureClick](https://www.vasco.com/products/two-factor-authenticators/hardware/one-button/digipass-secureclick.html)      
- [Yubico](https://www.yubico.com/)      
- [HyperFIDO](http://hyperfido.com/)       
- [Feitian Technologies](http://www.ftsafe.com/)      

For a comprehensive list of available U2F devices, simply [check Amazon](http://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=U2F). 

## Properties
The script has the following properties

|	Property	|	Description		|	Example	|
|-----------------------|-------------------------------|---------------|
|u2f_server_uri		|URL of the u2f server		|`https://idp.gluu.info`|
|u2f_server_metadata_uri|URL of the u2f server metadata|`https://idp.gluu.info`|

## Configure U2F

Follow the steps below to configure the U2F module in the oxTrust Admin GUI.

1. Navigate to `Configuration` > `Manage Custom Scripts`.    

2. Click on the `Person Authentication` tab
![person-auth](../img/admin-guide/multi-factor/person-auth.png)
3. Select the U2F script
![u2f-script](../img/admin-guide/multi-factor/u2f-script.png)
4. Enable the script by ticking the check box
![enable](../img/admin-guide/enable.png)
5. Click `Update`
6. Change the `Default Authentication Method` to `u2f`
![u2f](../img/admin-guide/multi-factor/u2f.png)
