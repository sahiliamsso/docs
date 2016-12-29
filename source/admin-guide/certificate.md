# Certificates 

Gluu Server components have cryptographic keys and X.509 certificates that are stored inside the
`chroot`. The details of the certificates are given below according to each component. The certificates
are available in the `/etc/certs` folder.

|ASIMBA		|Shibboleth	|APACHE		|OPENLDAP	|
|---------------|---------------|---------------|---------------|
|asimba.crt	|shibIDP.crt	|httpd.crt	|openldap.crt	|
|asimba.csr	|shibIDP.csr	|https.csr	|openldap.csr	|
|asimba.key	|shibIDP.jks	|httpd.key	|openldap.key	|
|asimba.key.orig|shibIDP.key	|httpd.key.orig	|openldap.key.orig|
|asimba.pkcs12	|shibIDP.key.orig|		|openldap.pem	|
|asimbaIDP.jks	|shibIDP.pkcs	|		|		|

The certificates for `Passport` authenticaiton are `passport-rp.jks, passport-rp.pem, passport-rs.jks`. The SCIM certificate is named `scim-rs.jks` and the OTP certificate is named `otp_configuration.json`.

Additionally the following `json` files are avaibale which are used in different custom scripts for multi-factor authentication.

* cert_creds.json
* duo_creds.json
* gplus_client_secrets.json
* otp_configuration.json
* oxauth-keys.json
* super_gluu_creds.json

# Updating Apache Certificate
The certificates require manual update from `/etc/certs/` folder. 

!!! Warning
    The private key cannot be password protected, and the public key must be base64 X.509. 

!!! Note
    Please backup your full `/etc/certs` directory and `cacerts` file under `/etc/pki/java/` folder before updating certificates.


Please follow these steps shown below to update the Apache SSL cert:

- Save the latest SSL httpd key and certificate in the `/etc/certs` folder
- Rename them to `httpd.key` and `httpd.crt` respectively
- Import 'httpd.der' into the java keystore
/ Convertion to DER, command:<br/> `openssl x509 -outform der -in httpd.crt -out httpd.der`
    - Import certificate in to Java Keystore(cacerts):<br/> `keytool -importcert -file httpd.der -keystore cacerts -alias <hostname_of_your_Gluu_Server>_httpd`
- Restart LDAP server, apache2/httpd and tomcat.

## Install Intermediate Certificates
Please follow the steps below to install intermediate certificates:

1. Log into your Gluu Server container.
2. Keep your intermediate certificate in the file `/etc/certs/`.
3. Modify `/etc/httpd/conf.d/https_gluu.conf`, and add<br/>
  `SSLCertificateChainFile /etc/certs/name_of_your_interm_root_cert.crt`.
4. Restart the service of the httpd server.
