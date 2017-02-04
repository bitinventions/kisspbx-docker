# kisspbx-docker
Docker installation for testing kisspbx 

Start containers with docker compose:
'''
docker-compose -p kisspbx up -d
'''

Create database:
'''
docker exec -it kisspbx_db_1 mysqladmin -u root --password="kisspbx" create asterisk
'''

Restart containers to allow application server to connect and rebuild database:
'''
docker-compose -p kisspbx restart
'''

Create AMI user to allow application server to connect to asterisk:

* Connect with a browser to http://localhost:81/kisspbx and enter user kisspbx:kisspbx
* Advanced -> Manager Users: create a new user clicking on '+'
* Settings -> Manager: enable manager in General tab and save
* Settings -> PBX: configure asterisk connection with host=asterisk and the user/password created previously in Manager Users.
* Apply clicking in red icon in the right upper side of the screen
* Restart containers for asterisk to take the new manager configuration

Now the dashboard can connect to asterisk and show time up and version. You can start configuring and testing the software. All the configuration is stored in volume kisspbx_mysql-storage and asterisk configuration in volume kisspbx_asterisk-config, so you can rebuild the containers keeping all the configuration.
