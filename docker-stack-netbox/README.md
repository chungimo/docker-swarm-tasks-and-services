Netbox on Traefik
---
[The Github repository](https://github.com/netbox-community/netbox-docker) houses the components needed to build Netbox as a Docker container.

This is a compose file to launch Netbox utilizing Traefik reverse proxy.

#### Setup
Configure these environment variables that sets the rules for Traefik.

Setup these environment variables:
```
export HOSTNAME=netbox.domain.com
export TRAEFIK_NETWORK=traefik-public
```

#### Nginx config by default storage driver
`/var/lib/docker/volumes/netbox_netbox-nginx-config/_data`

#### Docker stack deploy
`git clone -b master https://github.com/netbox-community/netbox-docker.git`

Copy this docker-traefik-netbox.yml file into the directory and deploy.

`docker stack deploy -c docker-traefik-netbox.yml netbox`
