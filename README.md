# Udacity-Linux-Server-Configuration

**Description**
---------------
Linux server configuration project which involved taking an Amazon Lightsail instance with a baseline Linux distribution and configuring it to securely host and serve a web application. Configuration includes securing the server from multiple attack vectors and installing/configuring dependencies required by the web application, such as an Apache Web Server and PostgreSQL database.


**Server Instance Info**
---------------
**IP Address**: 52.26.33.201  
**DNS Domain**: ec2-52-26-33-201.us-west-2.compute.amazonaws.com  
**SSH Port**: 2200  
**Web App Link**: [Item Catalog App](http://ec2-52-26-33-201.us-west-2.compute.amazonaws.com/catalog)  


**Server Config Changes**
---------------
1. Updated software packages  
2. Change ssh port from default (port 22) to port 2200  
3. Set up UFW (Uncomplicated Firewall)  
   1. Deny all incoming connections  
   2. Allow all outgoing connections  
   3. Allow specific connections for web app  
     * SSH - TCP: Port 2200  
     * HTTP - TCP: Port 80  
     * NTP - UDP: Port 123  
   4. Enable UFW  
4. Set up key-based authentication and disabled password-based authentication  
   1. Locally generated ssh key pairs for server accounts and placed public keys on server  
     * Modified file and folder permissions of location of public keys, as required by ssh  
   2. Modified sshd_config file to disable password-based login  
5. Created additional server account with sudo access and ensured remote root login is disabled  
