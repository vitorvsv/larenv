# Development docker environment to Laravel Framework

This environment contains the following configurations:

* PHP + Apache  = larenv_php_apache
* MariaDB 	= larenv_mysql
* Postgres 	= larenv_postgres
* PhpMyAdmin    = larenv_phpmyadmin

# Network

By default, the environment uses the 10.10.10.0/16 network (larenv_network)

* 10.10.10.2 = PHP + Apache     = larenv_php_apache
* 10.10.10.3 = MariaDB/Postgres = larenv_mysql/larenv_postgres
* 10.10.10.4 = PhpMyAdmin       = larenv_phpmyadmin

# Considerations

* At the larenv_php_apache there is an user called application, who has access to the folder '/shared'
that is shared with others containers and with the host. If you want to use this feature, pass the --user=application
flag when make docker exec.
* All volumes shared between the host and the container will be configured with the ':Z' or ':z' flags in the end of the line. 
The ':Z' flag indicates shared in the host and the container only. The ':z' indicates shared with other containers.


# Configurations

<h2>Step 1 - Network</h2>

If you want to change the default network, is necessary to change the file docker-compose.yml

use the following command to change the network, changing the network and the name as you wish.

```sudo docker network create --subnet 10.10.10.0/16 larenv_network ```

Change the line that contains the name of your network

```
networks:
  default:
    external:
      name: larenv_network
```

<h2>Step 2 - Folders for scripts and databases</h2>

You can use scripts and database dump's inside the container. The container will make them available to you.

If the folders scripts and bases don't exist in the folder larenv_mysql/larenv_postgres, create that. Use the following command:

mkdir larenv_mysql/scripts && mkdir larenv_mysql/bases
mkdir larenv_postgres/scripts && mkdir larenv_postgres/bases


<h2>Step 3 - Docker Compose</h2>

The docker-compose is responsible for building all development environment, than we can configure.

The line bellow configures the path to your project or folder to apache root. Normally use the path '../' if you clone this
repository inside your project.

``` ../:/app ```

change to the local where the database files are (The databases are stored out of container).

``` ~/bases_larenv:/var/lib/mysql ```

This line configures one folder that is shared to all containers.

``` ./shared/:/shared ```

OBS: The directory /shared is available inside the container.

<h2>Starting containers...</h2>

To start the container use the following command:

``` sudo docker-compose up -d```

<h2>Step 4 - config </h2>

Is necessary to configure your database connection to use the IP of the container database.

<h2>Step 5 - Configuring Database</h2>

If you put your databases dump's in larenv_mysql/bases or larenv_postgres/bases, you can execute the following command
to create your databases (the name of the database will be the name of the file .sql)

``` sudo docker exec -it larenv_db_1 bash create_db```

You can either create your database using phpmyadmin, or put your dump in the shared folder, to get the file
in your container and restore it using mysql/postgres command line.

That is all, guys!
