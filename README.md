# Docker Hosting with Automatic SSL Certificate Generation for Nginx-Proxy
_based on https://github.com/nginx-proxy/acme-companion_


This repo contains the `docker-compose.yml` files used to set up my vServer to host multiple docker containers all with SSL. 
A complete documentation can be found in the original repo.


## Setting up

First you need to create a docker network with the following command:

```bash 
    docker network create nginx_network
```

Before you can start the containers with

```bash 
    docker-compose up --build -d
```


## Setting up `docker-compose.yml` file

In order to serve a container to a specified domain, follow those steps.
The sub folder `./grafana/` contains a simple Grafana setup.

1) Change your DNS settings to point the domain to your server
2) Add the following lines the end of your `docker-compose.yml`:

   ```yml
    networks:
        nginx_network:
            external:
                name: nginx_network
    ```

3) For each service add the following settings: 

   ```yml
    environment:
      VIRTUAL_HOST: monitoring.emeal.ch # your domain name
      LETSENCRYPT_HOST: monitoring.emeal.ch # your domain name
      LETSENCRYPT_EMAIL: info@emeal.ch # a valid mail address
    networks:
      - nginx_network
    ```

