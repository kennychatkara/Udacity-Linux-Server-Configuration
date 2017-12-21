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


**Server Installed Software**
---------------
* Apache Web Server (with mod_wsgi module)
* PostgreSQL Database
* Python Package Installer (pip)
* Git


**Server Config Changes**
---------------
1. Updated software packages  
2. Change ssh port from default (port 22) to port 2200  
3. Set up Ubuntu UFW (Uncomplicated Firewall)  
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
   2. Modified 'sshd_config' file to disable password-based login  
5. Created additional server account with sudo access and ensured remote root login is disabled  
6. Installed Apache Web Server package  
7. Installed mod_wsgi Apache module, which helps Apache host WSGI spec-compliant Python applications  
   * Created new Apache config file 'catalog.conf' to configure new Apache VirtualHost to use the WSGI module to handle requests
8. Installed PostgreSQL Database package  
9. Set system local timezone to UTC  
10. Item Catalog app dependencies configuration  
    1. Enabled a python virtual environment for the web application  
    2. Installed the app's python module dependencies to the virtual environment  
     * Python modules: flask, sqlalchemy, flask-sqlalchemy, psycopg2, oauth2client, requests  
    3. Created PostgreSQL 'itemcatalog' database and 'catalog' user with limited (create DB only) permissions to app's database  
    4. Modified PostgreSQL config file 'pg_hba.conf' to use md5 instead of peer authentication for local database connections  
11. Downloaded and modified [Item Catalog app's source code](https://github.com/kennychatkara/fullstack-nanodegree-vm) to run on server in Python virtual environment using PostgreSQL database  
    1. Changed database usage from SQlite to PostgreSQL in database.py at SQLAlchemy create_engine operation  
    2. Updated connection to PostgreSQL 'itemcatalog' database with 'catalog' user  
    3. Updated client_secrets.json path in application.py to use absolute path of server's app hosting directory  
    4. Added server IP address and DNS domain to Google Cloud Client Credentials and update server client_secrets.json file  


**Resources**
---------------  
* https://modwsgi.readthedocs.io/en/develop/user-guides/virtual-environments.html
* https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps  
* https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps
* http://docs.sqlalchemy.org/en/latest/dialects/postgresql.html  
