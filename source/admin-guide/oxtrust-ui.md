# oxTrust Administrative Graphical User Interface (GUI)
The administration interface (oxTrust) is accessible by navigating to 
`https://hostname` (the one you provided during setup). When you 
first complete an installation, the default username is `admin` and 
the password is the same as the `LDAP superuser` password.

## Welcome Page
After successful authentication the administrator is taken to the 
Dashboard. Some basic information about the VM/server is displayed as 
well as the server version, free memory, and disk space. In the top 
right there is a user icon which can be used to log out of oxTrust. 
The left hand menu is used to navigate the admin interface.

![welcome-page.png](../img/oxtrust/welcome-page.png "Welcome to Gluu Server")

## Configuration   
From the configuration tab, the Gluu Server administrator can manage 
certain non-protocol related tasks.

### Organization Configuration

There are three sections in the organization configuration page:       

1. [System Configuration](#system-configuration)         
2. [SMTP Server Configuration](#smtp-server-configuration)         
3. [oxTrust Settings](#oxtrust-settings)             

#### System Configuration

![system-config-options](../img/oxtrust/system-config-options.png)

- Self-service password reset: Allow users to reset their password via email. In order for this feature to work, the admin will also need to perform [SMTP Server Configuration](#smtp-server-configuration).      

- SCIM Support: Enable SCIM Support if you plan on using the SCIM protocol to move identity data from applications to Gluu and vice versa.      

- DNS Server(s): If the organization uses any custom `DNS Server(s)`, the address should be added here. 

- Maximum Log Size (MB): By default the maximum size of the log file is 200 mb. This value can be increased or decreased depending on the organizations requirements.     

- User can edit their own profile: oxTrust has a profile section for each user. If this option is enabled, users will be able to log into oxTrust and edit the values associated with their user.      

- Contact Email: This email will be displayed on all error pages with a note instructing users to contact for troubleshooting and  assistance.        

#### SMTP Server Configuration     

![smtp-config](../img/oxtrust/smtp-config.png "SMTP Configuration")

The Gluu Server needs a mail server in order to send notifications. 
The fields on this page are self-explanatory, such as hostname, user, 
password, ssl-requirement, authentication requirement, sending name and address. 
All fields are manadory and the configuration can be tested before confirmation.

| Fields | Description |
|--------|-------------|
| SMTP Host | HostName of the SMTP server |
| From Name | Name of the sender|
| From Email Address | Email Address of the Sender|
| Requires Authentication | This Checkbox is enables authentication of the sender |
| SMTP User Name | User Name of the SMTP |
| SMTP Password | Password for the SMTP |
| Requires SSL | This checkbox is to enable the SSL |
|SMTP Port | Port number of the SMTP server |
     
#### oxTrust Settings  

![oxtrust-settings](../img/oxtrust/oxtrust-settings.png "OxTrust Settings")

From the oxTrust Settings page the administrator can find the oxTrust build date and number, and manage the organization name, logo, and favicon. This page also contains the name of the Gluu Server administrator group. Users added to this group will have administrator access to the Gluu Server.

### JSON Configuration      
There are three tabs included in the `JSON Configuration` menu:

![json-config-head](../img/oxtrust/json-config-head.png "JSON Configuration Headers")

#### oxTrust Configuration
From this tab you can access and edit the oxtrust JSON configuration file. 
Click the update button at the bottom of the changes to save any changes. 

#### oxAuth Configuration
The oxAuth JSON configuration page gives easy access to the different endpoints used by Gluu Server CE. 
This page also contains the supported response, grants, and algorithms. 

#### oxTrust Import Person Configuration
The oxTrust Import Person Configuration page contains the configuration for 
the file method of importing users into the Gluu Server. The administrator 
can import users from an `xls` file which must be defined in this tab to import 
data in the LDAP attributes. The default format should contain the following fields: 

### Manage Authentication
This section allows the Gluu Server administrator to define how and
where the server should connect to authenticate users. If it is a remote
LDAP/Active Directory server, the values are required. Put the details
of the data source that you are trying to connect with Gluu Server. For
example, the data source can be your back-end Active Directory, or your
local LDAP server.

![Manage LDAP Authentication](../img/oxtrust/admin_manage_ldap.png)

* _Name:_ This field contains the name of the authentication server.

* _Bind DN:_ The *Username* for the authentication server (local
  LDAP/remote LDAP/remote Active Directory) goes here.

* _Max Connections:_ This option can be used to define the total number
  of simultaneous connections allowed for reading local LDAP/remote Active
  Directory/remote LDAP.
  
* _Primary Key:_ This field contains the primary key to connect to the
  authentication server (i.e. SAMAccountName/uid/mail etc.). 

* _Local Primary Key:_ This field contains the Gluu Server's internal LDAP primary key. Generally the key is either *uid* or *mail*. 

* _Server:_ The unique name of the authentication server and port number
  (e.g. auth.company.org:636) goes here.

* _Base DN:_ Add base DNs in this field to allow the Gluu Server to
  connect and search the LDAP server. Every directory tree should be added
  separately using the *Add Base DN* option.

* _Change Bind Password:_ This button assignes a password to
  authenticate the *Authentication Server*.

* _Use SSL:_ Enable SSL if the authentication server requires a secured port (e.g. 636).

* _Enabled:_ This check-box is used to enable the keys that are inserted
  in their respective fields.

* _Deactivate:_ This button *Deactivates/Activates* the Gluu Server
  accessibility for authentication.

* _Test LDAP Connection:_ Use this button to check whether the provided
  information is sufficient to connect to the authentication server. The
  scan is done in real time.

#### Default Authentication Method

This allows the Gluu Server administrator to select both the default
authentication mode, and level for person authentication. Both modes are
set to "Default" until additional authentication mechanisms are enabled
via [custom scripts](#manage-custom-scripts). 

|Authentication Method|Description|
|---|---|
|Authentication mode|This mode is used when users login to applications via Gluu|
|oxTrust authentication mode|This mode is used for authentication to the Gluu Server GUI|


Gluu Server uses oxAuth as the first step of authentication in all kind 
of SSO protocols ( OpenID Connect, SAML, CAS )

![default](../img/admin-guide/auth-management/default.png)

* Authentication mode: This mode defines the mode used for general authentication with Service Providers. The mode defined under this tab will not affect the users accessing the oxTrust administrator interface.
* oxTrust authentication mode: This mode is used when the user is accessing the oxTrust administrator interface using the gluu server hostname.
* Passport Support: This mode uses third-party authentication e.g. Google+, Twitter, Facebook to authenticate users in Gluu Server.
* Custom Script Authenticaiton: This mode uses custom script and enabled in the oxTrust Admin UI.

### Manage Custom Scripts
The Gluu Server exposes interception scripts in places where it is common 
for organizations to implement custom workflows, or changes to the 
look and feel of the Gluu Server. The most commonly used scripts are 
for authentication, authorization and identity synchronization. Each
type of script has its own interface--in other words what methods are
available. For more information, see the reference page detailing how
[to write a custom authentication script](./user-authentications.md).

### Manage Registration
The Gluu Server is shipped with a very basic user registration 
feature. For custom enrollment requirements, you may want to write
a registration page and use the SCIM endpoint
to add the user to the Gluu Server. Also, in some cases oxTrust is not Internet facing,
which makes it a bad option for user registration. Use this feature
only if you have very basic requirements! 

This tabs has two options:
1. `Disable Captcha for registration form`
2. `Configure Registration Form Attributes`

**Disable Captcha for registration form**    
![registration](../img/admin-guide/manage_registration.png)

This option adds a required CAPTCHA to the registration form.     

**Configure Registration Form Attributes**    
![attr_filter](../img/admin-guide/config_registration.png)

This section allows you to filter the list of attributes to be displayed 
in the registration form. Search, select, add, and order desired attributes here.

### Attributes
Available user attributes are found on this page. By default, only the active attributes are visible.  
Use the `Show All Attributes` to display the inactive attributes too. 
Custom attributes can be added by clicking the `Add Attribute` button 
and filling in a simple form. Note that attributes must already be
present in the LDAP server. Adding an attribute here is like registering 
it in the Gluu Server. In order to release an attribute during a SAML or 
OpenID Connect transaction, the Gluu Server needs to know it exists.  
How to create and configure [SAML Attributes](./saml/#saml-Attributes) 
and [OpenID Connect Scopes](./openid-connect/#scopes) are 
discussed later under each section of this document.

### Cache Refresh
Cache Refresh, a.k.a. LDAP Synchronization, is the process of connecting an existing backend LDAP server, like Microsoft Active Directory, with the Gluu Server's local LDAP server. `Cache Refresh` 
periodically searches these data sources, compares the results to 
previous searches, and if a changed user account is found, it is updated.
The frequency of cache refresh is also set from this page via the 
`Polling interval (minutes)`. The `key attribute(s)` is used to correlate
a user if the user is found in more then one LDAP server. In this case, the two entries
are joined. The source attributes specify which attributes will be 
pulled from the backend LDAP server. The backend server address, bind DN 
and other connection information is speciifed in the `Source Backend 
LDAP Servers` tab. More information on [LDAP Syncronization](./user-group.md/#ldap-synchronization)

### Configure Log Viewer / View Log File
This tool can be used to view file system logs. If you don't like to 
ssh, Log Viewer is your friend! Several common logs are preconfigured,
or you can define new logs by specifying the path.

### Server Status
This page provides some basic information about the Gluu Server such as the 
hostname, IP address, free memory & disk space. The number of users in the 
backend is also available in this page.

### Certificates
The certificate page shows some summary information about the SSL
and SAML certificates.

## SAML
If you chose to deploy the Shibboleth SAML IDP during installation, 
you will see this menu to manage all SAML related functionalities. 
In addition, if you chose to deploy the Asimba SAML Proxy, you will see a sub menu for inbound SAML.

### Outbound

![saml](../img/oxtrust/saml.png)

The `Trust Relationships` page, as the name suggests, will allow the administrator to 
view the created trust relationships (TRs) by searching using the search button. 
There is a button to add relationship with the same name. All the available TRs can be 
searched by using two (2) spaces in the search bar. There are some information that the 
administrator needs to gather before creating any new TR in Gluu Server. The metadata of the 
Service Provider (SP) connected using TR must be gathered along with the required attributes. 
The creation of TR will be covered in detail later under [SAML](./saml.md).

### Inbound

## OpenID Connect
The [OpenID Connect protocol](http://openid.net/specs/openid-connect-core-1_0.html) is supported by default in all Gluu Server deployments. The scopes page contains the `Add Scope` button which can be used to add new scopes in Gluu Server. Additionally the available scopes can be searched by name or listed using two (2) spaces in the search bar.

![scopes](../img/oxtrust/scopes.png)

The OpenID Connect clients are accessible from the `Clients` page under `OpenID Connect` tab. 
The structure is similar to the scopes page with the functionality to search by name or use two (2) spaces 
to list all the available clients. New clients can be added by clicking 
the `Add Client` button. This section is detailed in [OpenID Connect](./openid-connect.md) 

![clients](../img/oxtrust/clients.png)

## UMA
[UMA](./uma.md) or (User-Managed Access) is an access management protocol supported by Gluu Server.
The available scopes can be searched using the search bar on the top of the page. 
New scope descriptions can be added using the `Add Scope Description` button.
![uma-scopes](../img/oxtrust/uma-scopes.png)

UMA resources page also has a searchbar on the top of the page and can be used 
to search for resource sets. New resource sets can be added by clocking on the `Add Resource Set` button.
![uma-resources](../img/oxtrust/uma-resources.png)

## Users
Users tab allows Gluu admin to do various task, including add admin, search users, Import users from file.

## Personal
Personal tab allows the individual person to view his basic profile and modify certain fields.
