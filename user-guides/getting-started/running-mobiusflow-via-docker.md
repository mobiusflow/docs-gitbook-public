# Running MobiusFlow via Docker

MobiusFlow has been containerised and is run via docker.&#x20;

## Mobius v1.X.X

Below is an example docker-compose.yml file you could use when running MobiusFlow. In this example, an online version of MobiusFlow 1.19.1 is used. Note that, as well as the MobiusFlow service (labelled simply 'mobius'), the file also containers a reference to an nginx and mongodb containers.

The nginx container is used for port mapping, and mongodb container used as a database. Neither of these are required to run MobiusFlow.

```
version: "3.8"

volumes:
  mobius-data:
  mobius-licence:
  mongodb:

networks:
  frontend:
  backend:

services:
  mobius:
    platform: linux/amd64
    build: ./dist
    image: local/mobiusflow-docker:1.19.1_1.19.1
    container_name: mobiusflow
    privileged: false
    restart: always
    environment:
      - MOBIUS_HUB_RESET_PSKS=true
      - MOBIUS_ENABLE_CONFIG_UI=true
      - MOBIUS_HUB_ID=000001
      - MOBIUS_LOCAL_TIMEOUT=10000
      - MOBIUS_LOG_SERVICE_STATUS=
      - MOBIUS_LICENCE=38782095-410e7ab5-c3c36a84-dd39683f-c5a8062b-78f846c2-52588c49-fc8eecf4
      # - MOBIUS_LICENCE_KEY=
      # - MOBIUS_LICENCE_TOKEN=
      # - MOBIUS_LICENCE_RESET=
      - MOBIUS_ENGINE_API_PORT=8443
      - MOBIUS_ENGINE_API_AUTH_PROVIDER=local
    volumes:
      - mobius-data:/data
      - mobius-licence:/.licence
    networks:
      - backend
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "10"
  nginx:
    image: ghcr.io/mobiusflow/nginx-cloud:1.1.0
    container_name: nginx
    privileged: false
    restart: always
    environment:
      - NGINX_UI_CONTAINER=mobius
    ports:
      # these ports are for use with the nginx TLS terminator use in mobius-cloud-install
      - 8080:8080
      - 8443:8443
      - 1883:1883
      - 30814:30815
      - 30817:30817
    networks:
      - frontend
      - backend
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "10"
  mongodb:
    image: bitnami/mongodb:latest
    container_name: mongodb
    restart: always
    environment:
      - MONGODB_ROOT_PASSWORD=r5DybE57qug3WaHebeUy2bAvvVhKXUWHD
      - MONGODB_USERNAME=mobius
      - MONGODB_PASSWORD=RmzsXQYReLHaCS5wWGjAPjtJ7VnTw4qL
      - MONGODB_DATABASE=mobius
    volumes:
      - mongodb:/bitnami/mongodb
    networks:
      - backend
    logging:
      driver: none
```

This file can also be downloaded here:

{% file src="../../.gitbook/assets/docker-compose.yml" %}

## Licensing

It is important to include the correct licensing information within the environment variables of your docker-compose.yml file.

See the main [article](../../technical-docs/licencing/licensing-v1.19.1-and-later.md) on licensing for a full explanation of what is required for online and offline licensing as well updating a given licence.
