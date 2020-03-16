# Apache Guacamole in a Container Secured with TLS

This Docker Compose setup makes it very easy run [Apache Guacamole](https://guacamole.incubator.apache.org/) behind a NGINX reverse proxy. TLS secured.

## Unique Features

* Unlike other examples with compose this setup is much simpler to setup and is inline with common docker practice.
* This composition is using official Apache Guacamole Docker Images [guacamole/guacamole:latest](https://hub.docker.com/r/guacamole/).
* Automatically created and configured Nginx Reverse Proxy in front of the Guacamole Service.
* Minimal configuration of only *two* mandatory environment variables.

## Run

Before you start the service configure two mandatory parameters.
The easiest way is to create a `.env` file in your working directory eg.:

*Step 1*
```sh
git clone https://github.com/ajeeth/containerized-guacamole.git
cd containerized-guacamole
```

*Step 2*

```ini
cat > .env <<EOF
POSTGRES_PASSWORD=*****
VIRTUAL_HOST=workshop.8gears.com
EOF
```

It is advised to run the service `init-guac-db` once before starting all other services. This one off job will export the application database schema so Postgres can pick it up when it starts and init the database with those values accordingly.

*Step 3*
```sh
docker-compose up init-guac-db
```

*Step 4* Start Guacamole Services:

```sh
docker-compose up -d
```

Now go to your application https://workshop.domain.org/guacamole and login as guacadmin/guacadmin. 
Don't forget to change the password in the next step.
