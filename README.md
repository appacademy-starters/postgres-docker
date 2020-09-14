# Postgres Docker for local development

This is a docker-compose.yml file and setup instructions for running
postgreSQL in docker for local development.

## Install Docker Desktop

Install [Docker Desktop](https://www.docker.com/products/docker-desktop)

## Clone this repository

`git clone <repo url>`

## Start the container with docker-compose in the background

```shell
docker-compose up -d
```

If you reboot your computer you will probably have to issue this command in order to get your container going again.

## If your container doesn't start

you can find out more info about what happened with this command

```shell
docker-compose logs
```

## Stopping the container

```shell
docker-compose down
```

## Connecting via psql

To connect via psql you need to connect to localhost using
the postgres user with the default password `password` (You can change this in the docker-compose.yml file before you run the container for the first time)

```shell
psql -h localhost -U postgres
```

If you want to be able to type `psql` without specifying localhost or the user you can set the following environment variables in your shell startup file:

```shell
export PGHOST=localhost
export PGUSER=postgres
```

Then you can simply type `psql` by itself and it will connect

If you want to not have to type the password copy the `.pgpass` file to your home directory. (If you've changed the password in docker-compose.yml you'll also need to change it in this file)

```shell
cp -v .pgpass ~/.pgpass
```

You also have to give this file proper permissions for it to work with this command once you've copied it.

```shell
chmod 0600 ~/.pgpass
```

After this should you be able to type `pgsql` and it should connect without prompting you for anything.

## Starting over

This docker-compose.yml keeps your postgres data in a docker `volume` called `postgres-data`. If you want to start over with a clean postgres database, you can remove the container AND volume with this docker command:

```shell
docker-compose down -v
```

and then just start it back up.

```shell
docker-compose up
```
