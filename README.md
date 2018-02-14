## Docker WP Example

(Using HTML5 Blank Theme Boilerplate)

With [docker](https://www.docker.com/get-docker) installed, simply run in the root of the project:

```bash
docker-compose up
```

and visit http://localhost.

You will see that the current directory is mounted as a theme, and you can develop on it freely as you would.

Behind the scenes, docker used the `docker-compose.yml` file to generate an ubuntu/apache container that houses the wordpress files, as well as a MYSQL container that is directly linked to the apache container.

You can read more about the source of this docker image at [docker wordpress](https://hub.docker.com/_/wordpress/).


## Other Commands

You can see the running containers by executing `docker ps`.  You can find the container_name using this.

```bash
docker-compose down                                     # Destroys the database and the apache image
docker-compose stop                                     # Stops the images without destroying them
docker-compose restart                                  # Restarts an image
docker exec -it {container_name} /bin/bash              # Bash into a container
```

## Want more?

You can also attach a WP-CLI container to these running containers, to run things like a core install, plugin install, etc.

Examples:

```bash
# Core Install
docker run -it --rm --volumes-from {container_name} --network container:{container_name} -u 33 wordpress:cli core install --url=localhost --title=Test --admin_user=admin --admin_password=admin --admin_email=admin@admin.com

# List Users
docker run -it --rm --volumes-from {container_name} --network container:{container_name} -u 33 wordpress:cli user list

# Install Plugin
docker run -it --rm --volumes-from {container_name} --network container:{container_name} -u 33 wordpress:cli plugin install edit-flow --activate
```
