# Wordpress, Nginx and Let’s Encrypt with Docker Compose
## Intro:
I use this setup for my blog, its adapted from <a href='https://github.com/evgeniy-khist/letsencrypt-docker-compose'>this step up from evgeniy-khist</a>

## Prerequsites:
You must own a domain name and have a DNS (A record) pointing to an IP address.

## Run as test:
Set the variables in config.env.example then rename it to config.env.

Create the required volumes:
```bash
docker volume create --name=nginx_ssl
docker volume create --name=certbot_certs
```

Then run:
```bash
# See if it works
docker-compose --env-file config.env up --build
# Run it properly
docker-compose --env-file config.env up --build -d
```

Test the site and make sure its all working before moving to production.  

## Run as Production:

Re-create the volume for Let's Encrypt certificates:
```bash
# Destroy the cert bot container and volume
docker-compose down
# docker rm {COMPOSE_PROJECT_NAME}_certbot_1 {COMPOSE_PROJECT_NAME}_nginx_1
# example
docker rm wptest_certbot_1 wptest_nginx_1

docker volume rm certbot_certs
docker volume create --name=certbot_certs
```

Change the CERTBOT_TEST_CERT value to 0 in config.env

Start the containers:
```bash
docker-compose --env-file config.env up --build
docker-compose up -d --env-file config.env
```