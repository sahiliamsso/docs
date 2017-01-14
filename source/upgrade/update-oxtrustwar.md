#Updating oxTrust to latest release

keeping the oxTrust updated to the latest release is really important to have Gluu Server upto date and free from issues and bugs.

!!! Warning
	Before updating you must aware of any changes to schema or JSON properties. However, assuming none, the process should work.
	
Follow the below steps to update oxTrust with the latest release of oxTrust:

1. Login to chroot.

`service gluu-server-3.0.0 login`
	
2. Enter the below command to stop identity service.

`service identity stop`
	
3. Navigate to the path

`cd /opt/gluu/jetty/identity/webapps`
	
4. Take a back up of existing identity.war

`tar -zxvf identity.tar.gz`
	
5. Download and install the latest release of oxTrust

`wget http://ox.gluu.org/maven/org/xdi/oxtrust-server/3.0.0-SNAPSHOT/oxtrust-server-3.0.0-SNAPSHOT.war -O identity.war`
	
6. Once the process is complete, verify for the new identity.war in the webapps directory.

7. Start the identity service using the below command.

`service identity start`