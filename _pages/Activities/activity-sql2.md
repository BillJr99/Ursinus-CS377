---
layout: activity
permalink: /Activities/SQL2
title: "CS377: Database Design - The Structured Query Language (SQL)"


info:
  prev: ./SQL
  goals: 
    - To instantiate a database engine using Docker
  additional_reading:
    - link: https://docs.docker.com/engine/install/ubuntu/
      title: Installing Docker
    - link: https://www.postgresqltutorial.com/postgresql-python/connect/
      title: postgres Tutorial
    - link: https://medium.com/@aedemirsen/execute-sql-commands-at-postgresql-db-startup-with-docker-2be0abadec48
      title: Execute SQL Commands at postgresql DB Startup with Docker
      
tags:
  - sql  
  - programming
  
---

## Installing and Using Docker

Begin by installing docker on your local computer, as follows:

```
# alternatively, add the docker apt repository and install using apt: 
# https://docs.docker.com/engine/install/ubuntu/
sudo apt install snapd
sudo snap install docker

sudo groupadd docker
sudo usermod -aG docker ${USER}
sudo chmod 666 /var/run/docker.sock
```

### Creating a Docker Compose File

We can configure the services and environment variables for our docker image, and pull them from dockerhub.  To do this, create the following `docker-compose.yml` file:

```
version: '3.1'

services:

  db:
    image: postgres
    container_name: pgdb
    restart: always
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
      POSTGRES_DB: mydb
    ports:
      - "5432:5432"

  adminer:
    image: adminer
    container_name: pgadmin
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: root
    ports:
      - "8080:8080"
```

To compose this image, execute `docker-compose up -d`.

## Exploring the Docker Image

Navigate to `localhost:8080`, which is a port opened on your local computer that forwards to port 8080 on the local image, per the `docker-compose.yml` configuration above.  In this example, you can log in to the database on the host named `db` (per the system name in the configuration file above), username `root`, password `root`, and database name `mydb`.

You can get a shell terminal into your image by running `docker exec -it pgdb bash`, where `pgdb` is the name of the container you just created via the compose file above.

## Connecting to the postgres Instance on the Docker Image

You can install the postgres client on your local computer via the following package installation command to install some prerequisite software:

```
sudo apt install postgresql-client postgresql-client-common postgresql-common libpq-dev
```

Using `psql`, you can connect to a postgresql instance by providing the hostname, port, username, and database instance.  You'll be prompted for your password (all of which we specified in the docker compose file above).

```
psql -h localhost -p 5432 -U root -d mydb
```

### Executing SQL Queries through psql

From here, you can execute SQL queries in the usual way.  For example:

```sql
CREATE TABLE accounts (
	user_id serial PRIMARY KEY,
	username VARCHAR ( 50 ) UNIQUE NOT NULL,
	password VARCHAR ( 50 ) NOT NULL,
	email VARCHAR ( 255 ) UNIQUE NOT NULL,
	created_on TIMESTAMP NOT NULL,
        last_login TIMESTAMP 
);

INSERT INTO accounts (username, password, email, created_on) VALUES ('user', 'pass', 'user@user.com', '10/16/2023');

SELECT * FROM accounts;
```

If you navigate back to the web interface, you'll see this table with options to create triggers and foreign keys directly through the interface.

### Executing SQL Queries through Python

Similarly, you can connect to your postgres instance programmatically, as expected:

```python
import psycopg2

try:
    conn = psycopg2.connect(host="localhost", database="mydb" user="root" password="root", port=5432)

    cur = conn.cursor()

    cur.execute('SELECT * FROM accounts')
    result = cur.fetchall()

    print(result)
except (Exception, psycopg2.DatabaseError) as e:
    print(e)
finally:
    if not (conn is None):
        conn.close()
```

#### Protecting Connection Parameters

The `configparser` library allows you to protect your connection parameters (for example, the password), by storing those parameters in a file that you can set to `600` permissions.  This way, only the file owner can read or write to the file.  Be sure to `chmod 600 dabase.ini` and to add this file to your `.gitignore` list so that it does not upload to any repositories you may have.  Additionally, you could encrypt this file using a private key on your computer, and decrypt it within the program, for additional protection.

You can use `configparser` by adding the following function to your program:

```python
# https://www.postgresqltutorial.com/postgresql-python/connect/
def config(filename='database.ini', section='postgresql'):
    # create a parser
    parser = ConfigParser()
    # read config file
    parser.read(filename)

    # get section, default to postgresql
    db = {}
    if parser.has_section(section):
        params = parser.items(section)
        for param in params:
            db[param[0]] = param[1]
    else:
        raise Exception('Section {0} not found in the {1} file'.format(section, filename))

    return db
```

This function returns a dictionary that you can pass as keyword arguments to `psycopg2.connect()`:

```python
conn = psycopg2.connect(**db_params) # replace the call above
```

Your `database.ini` file can contain your connection parameters:

```
[postgresql]
host=localhost
port=5432
database=mydb
user=root
password=root
```

## Initializing the Database at Startup via Docker Compose

Create a file called, say, `init.sql` in a directory `postgres/init` within your docker directory (the one containing your `docker-compose.yml` file).  This file can contain your initialization SQL statements (for example, your `CREATE TABLE` commands).  

Next, create a `Dockerfile` file with the following contents below.  This creates a `docker-entrypoint-initdb.d` directory which can contain startup scripts that postgres will execute when composed via docker.  This will copy your `postgres/init` directory to this location within the docker image.

```
FROM postgres

RUN mkdir -p /docker-entrypoint-initdb.d/
ADD postgres/init/init.sql /docker-entrypoint-initdb.d/init.sql
RUN chmod -R 775 /docker-entrypoint-initdb.d

ENV MYSQL_ROOT_PASSWORD root

```

Next, modify your `docker-compose.yml` file to make this `init` directory available to the volume.  We will add the `build: .` and `volumes` section to do this, as well add as a default `POSTGRES_ROOT_PASSWORD`.

```
  db:
    build: .
    image: postgres
    container_name: pgdb
    restart: always
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
      POSTGRES_DB: mydb
      POSTGRES_ROOT_PASSWORD: root
    ports:
      - "5432:5432"
    volumes:
      - ./postgres/init:/docker-entrypoint-initdb.d
```

This time, to build your image, first run `docker build .` and then your `docker-compose up -d` command as usual.  You may need to remove and re-initialize the containers and images (see below to remove all of them to start over as needed!).

## Removing the Docker Instance

If you'd like to remove your docker images permanently, you can do so with the following commands:

```
# List all containers (only IDs)
docker ps -aq
# Stop all running containers
docker stop $(docker ps -aq)
# Remove all containers
docker rm $(docker ps -aq)
# Remove all images
docker rmi $(docker images -q)
# Remove all volumes
docker volume rm $(docker volume ls)
```