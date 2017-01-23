# DUO Security
## Overview
There are a few properties in the [DUO][duo] Authentication Script.

|	Property	|Status		|	Description	|	Example		|
|-----------------------|---------------|-----------------------|-----------------------|
|duo_creds_file		|Mandatory     |Path to ikey, skey, akey|/etc/certs/duo_creds.json|
|duo_host		|Mandatory    |URL of the DUO API Server|api-random.duosecurity.com|
|audit_attribute	|Optional|Attribute to determine user group|memberOf		|
|duo_group		|Optional|Attribute to enable DUO for specific user|memberOf	|
|audit_group		|Optional|Notify administrator via email upon user login|memberOf|
|audit_group_email	|Optional|Administrator email		| admin@organization.com|

## Configure DUO Account

1. Sign up for a Duo account.

2. Log in to the Duo Admin Panel and navigate to Applications.

3. Click Protect an Application and locate Web SDK in the applications list. Click Protect this Application to get your integration key, secret key, and API hostname.

4. Generate an `akey` value for your instance. [Click here to know more ](https://duo.com/docs/duoweb#1.-generate-an-akey)

For additional info on Duo's Web SDK check [this atricle](https://duo.com/docs/duoweb) 

## Configure CE Chroot
1. Prepare the DUO credential file `/etc/certs/duo_creds.json` 
with **ikey, akey & skey**

**Configure oxTrust**

Follow the steps below to configure the DUO module in the oxTrust Admin GUI.

1. Click on Manage Custom Scripts under Configuration on the Main Menu.

2. Scroll down to [DUO][duo] authentication script<br/>
![duo-script](../img/admin-guide/multi-factor/duo-script.png)

3. Change the value of `duo_host` to your API

4. Enable the script by ticking the check box
![enable](../img/admin-guide/enable.png)

5. Change the dufault authenticaiont method to [DUO][duo]
![duo](../img/admin-guide/multi-factor/duo.png)
