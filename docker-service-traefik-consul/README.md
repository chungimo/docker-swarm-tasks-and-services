Docker Swarm task for Traefik + Consul
---
Task for deploying Traefik with consul while defining the number of replicas. Shell file to set the variables or take in from deployment.

* Create docker network
* Set environment variables
* Modify docker-compose file
* Deploy ``docker stack deploy -c traefik_consul.yml.yml traefik-consul``

```
#email for domain registrations
export EMAIL=test@domain.dev
#domain that will be used
export DOMAIN=basedomain.dev
#username and password to access basic auth for traefik and consul UI
export USERNAME=admin
export HASHED_PASSWORD=$(openssl passwd -apr1 $PASSWORD)
echo $HASHED_PASSWORD
#number of replicas you need
#consul: if only one node, set to 0 so there's only 1 leader
#traefik: can be set to number of nodes available
export CONSUL_REPLICAS=3
export TRAEFIK_REPLICAS=$(docker node ls -q | wc -l)
```
