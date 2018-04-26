This is a [`docker-compose`](https://docs.docker.com/compose/) repository for a SilverStripe development environment running:

* nginx:latest
* PHP-FPM 5.6
* MySQL 5.6

---

## Getting set up

Clone this repository to a folder somewhere on your machine:

```
git clone git@github.com:robbieaverill/docker-silverstripe-nginx.git ~/path/to/docker-ss-nginx
cd ~/path/to/docker-ss-nginx
```

**Important:** Export the `SS_ROOT_PATH` environment variable to tell the container where to find your SilverStripe source code:

```
export SS_ROOT_PATH="~/path/to/silverstripe"
```

Finally, run the containers:

```
docker-compose build
docker-compose up
```

This will build and run three containers (one for each service) and bind the output to your terminal so you will get (for example) the nginx access and error logs as you use your container.

If you don't care about the logs, you can run in detached mode:

```
docker-compose up -d
```

You can still access the logs when running detached using the `docker logs [container_name]` command, e.g. `docker logs ss_nginx`.

## Using the containers

Map a local hostname to the IP of your docker container:

```
# Get the IP
docker-machine ip default
# E.g. 192.168.99.100

# As ROOT user:
echo "192.168.99.100 ss.local" >> /etc/hosts
```

By default the nginx container will run on port 80 (and 443, although I haven't implemented the SSL configuration for it yet - feel free to contribute). If you want to change this, modify `docker-images/nginx/Dockerfile` and `docker-compose.yml`, then run `docker-compose build` and `up` again.

From inside the php or nginx containers you will be able to access the mysql container via the `mysql` host name on port 3306.

By default, these are the database server credentials to use in your `_ss_environment.php` configuration file:

|Parameter|Value|
|---|---|
|Username|`root`|
|Password|`pw`|
|Host|`mysql`|



