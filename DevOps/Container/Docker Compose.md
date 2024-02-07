Is a command line tool to orchestrate [[Docker]] containers. It allows to define container from specific version of each images, volumes, network and dependency interaction between the containers.

## Docker compose down
Used to  stop and remove container and services of `docker-compose.yml` file. It is like a **off** button, where we can turn off all the components of an application.

- **`--rmi all`:** This option instructs Docker Compose to remove **all** unused Docker images used by your services. Think of these as empty boxes that your services might have been packaged in. Removing unused ones frees up disk space.
- **`--remove-orphans`:** This option tells Docker Compose to remove any containers, networks, or volumes that aren't defined in your `docker-compose.yml` file. Imagine finding leftover tools in your toolbox that don't belong to any set; this option cleans them up.
- **`--volumes`:** This option would normally remove **all** volumes used by your services, regardless of whether they're still needed. 

```sh
docker compose down --rmi all --remove-orphans --volumes
```