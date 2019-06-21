Docker Swarm task for Traefik + Consul
---
[Traefik](https://github.com/containous/traefik) (pronounced traffic) is a modern HTTP reverse proxy and load balancer that makes deploying microservices easy. Traefik integrates with your existing infrastructure components (Docker, Swarm mode, Kubernetes, Marathon, Consul, Etcd, Rancher, Amazon ECS, ...) and configures itself automatically and dynamically. Pointing Traefik at your orchestrator should be the only configuration step you need.

#### Setup
Task for deploying Traefik with consul while defining the number of replicas. Shell file to set the variables or take in from deployment.

Set these environment variables:
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

#### Docker stack deploy
`docker stack deploy -c traefik_consul.yml traefik_consul`
