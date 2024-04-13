# Docker Compose
Docker Compose is a tool used to run multi-container Docker applications. It allows you to define and run multiple containers as a single application, providing an easy way to manage, configure, and deploy your containers

# Compose Commands

- ` docker compose version `
- ` docker compose config ` - validates and displays the configuration of the services defined in the docker-compose.yml file.
- ` docker compose start ` - starts the containers for the services defined in the docker-compose.yml file.
- ` docker compose stop ` - stops the containers for the services defined in the docker-compose.yml file.
- ` docker compose restart ` - restarts the containers for the services defined in the docker-compose.yml file.
- ` docker compose run ` 
- ` docker compose create `
- ` docker compose rm ` - removes the stopped containers for the services defined in the docker-compose.yml file.
- ` docker compose attach `
- ` docker compose pause ` - pauses the containers for the services defined in the docker-compose.yml file.
- ` docker compose unpause ` - unpauses the containers for the services defined in the docker-compose.yml file.
- ` docker compose wait `
- ` docker compose up ` - starts all the services defined in the docker-compose.yml file.
- ` docker compose down ` - stops and removes all the containers, networks, and volumes created by docker-compose up.
- ` docker compose ps ` - lists all the running containers for the services defined in the docker-compose.yml file.
- ` docker compose top `
- ` docker compose events `
- ` docker compose logs ` - shows the logs of the containers for the services defined in the docker-compose.yml file.
- ` docker compose images `
- ` docker compose build ` -  builds or rebuilds the Docker images of the services defined in the docker-compose.yml file.
- ` docker compose push `
- ` docker compose cp `
- ` docker compose exec ` - runs a command inside a running container for a service defined in the docker-compose.yml file.
- ` docker-compose pull ` - pulls the latest images for the services defined in the docker-compose.yml file.
- ` docker-compose kill ` - sends a SIGKILL signal to the containers for the services defined in the docker-compose.yml file.


# Compose File

Docker Compose relies on a YAML configuration file, usually named compose.yaml., written in YAML language.

Use the following links to navigate key sections of the Compose Specification.
1. [Version and name top-level elements](https://docs.docker.com/compose/compose-file/04-version-and-name/)
2. [Services top-level elements](https://docs.docker.com/compose/compose-file/05-services/)
3. [Networks top-level elements](https://docs.docker.com/compose/compose-file/06-networks/)
4. [Volumes top-level elements](https://docs.docker.com/compose/compose-file/07-volumes/)
5. [Configs top-level elements](https://docs.docker.com/compose/compose-file/08-configs/)
6. [Secrets top-level elements](https://docs.docker.com/compose/compose-file/09-secrets/)


### Docker Compose Service Configuration
A Docker Compose service can be configured with the following options:

- `build:` Specifies the path to the Dockerfile used to build the service image.
- `image:` Specifies the name of the Docker image to use for the service.
- `container_name:` Specifies the name of the container.
- `ports:` Specifies the port mapping between the host system and the container.
- `environment:` Specifies environment variables to be set in the container.
- `networks:` Specifies the networks to connect the container to.
- `volumes:` Specifies the volumes to mount in the container.


### Docker Compose File Structure
A Docker Compose file consists of the following sections:

1. **Version:** The version of the Docker Compose file format to use.Example: version: '3'
2. **Services:** The services to run as part of the Docker Compose application.Example:
```
services:
  app:
    build: .
    ports:
      - "8000:8000"
    environment:
      DEBUG: "true"
```
3. **Networks:** The networks to create and connect the services in the Docker Compose application.

- `networks:` Defines a list of custom networks to create.
- `driver:` Specifies the network driver to use.
- `name:` Specifies the name of the network.
- `external:` Specifies an existing network to connect to.


Example:
```
networks:
  app-network:
    driver: bridge 
```

4. **Volumes:** The volumes to create and share between the containers in the Docker Compose application.

- `volumes:` Defines a list of named volumes to create.
- `driver:` Specifies the volume driver to use.
- `name:` Specifies the name of the volume.
- `external:` Specifies an existing volume to use.


Example:
```
volumes:
  data:
    driver: local
```

# Examples
### Example 1: Simple web application

```
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"

```
This configuration defines a single service named "web" that builds an image from the Dockerfile in the current directory and exposes port 5000 on the host machine.

### Example 2: Multi-container application with custom network and volumes
```
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - type: bind
        source: ./app
        target: /app
    networks:
      - mynet
  db:
    image: postgres
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - mynet
networks:
  mynet:
volumes:
  db_data:

```
This configuration defines two services named "web" and "db" that use a custom network named "mynet" and a named volume named "db_data". The "web" service builds an image from the Dockerfile in the current directory, exposes port 5000 on the host machine, mounts the ./app directory as a volume in the container, and connects to the "mynet" network. The "db" service uses the "postgres" image, mounts the "db_data" volume, and connects to the "mynet" network.

