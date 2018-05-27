# Development docker enviroment to Laravel Framework

This enviroment contains the following configurations:

* PHP + Apache  = larenv_php_apache
* MariaDB 	    = larenv_db
* PhpMyAdmin    = larenv_phpmyadmin

# Network

To default the enviroment use the 10.10.10.0/16 networks (larenv_network)

* 10.10.10.2 = PHP + Apache  = larenv_php_apache
* 10.10.10.3 = MariaDB 	     = larenv_db
* 10.10.10.4 = PhpMyAdmin    = larenv_phpmyadmin

# Considerations

* At the larenv_php_apache there is an user called application, he has access to an folder (/shared)
that is shared with others containers and with the host. If is necessary use this feature, pass the --user=application
flag when make docker exec.

# Configurations

<h2>Steep 1 - Network</h2>

If will change the default network, is necessary change the file docker-compose.yml

use the following command to change the network changing the network and the name.

```sudo docker network create --subnet 10.10.10.0/16 larenv_network ```

Change the line to contains the name of your network

```
networks:
  default:
    external:
      name: larenv_network
```

<h2>Steep 2 - Folders</h2>

if don't exists in folder larenv_db the folders scripts and bases, create that. Use the command bellow

mkdir larenv_db/scripts && mkdir larenv_db/bases

<h2>Steep 3 - Docker Compose</h2>

The docker-compose is responsible to build all developer enviroment, than we can configure.

In line bellow configure the path to your project or folder to apache root.

``` /home/vitor/www_vitor/vitor:/app ```

change too the local where the database files are.

``` ~/bases_larenv:/var/lib/mysql ```

This line configure one folder that is shared to all containers.

``` /home/vitor/www_vitor/vitor/larenv/enviroment/shared/:/shared ```

OBS: In the container is make a directory /shared

<h2>Starting containers...</h2>

To start the container use the following command:

``` sudo docker-compose up -d```

<h2>Steep 4 - config </h2>

Is necessary configure your database connection to use the IP of you container db.

<h2>Steep 5 - Configuring Database</h2>

If you put yours dumps' databases in larenv_db/bases, you can execute the followind command
to create your databases (the script put the name file how database name)

``` sudo docker exec -it larenv_db_1 bash create_db``

Or you can create your database using phpmyadmin, or put your dump in shared folder and than
get this file in your container and make dump up using mysql command line.

That is all, guys!
