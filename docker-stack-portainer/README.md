Portainer on Traefik
---
[Portainer](https://github.com/portainer/portainer) is a lightweight management UI which allows you to easily manage your different Docker environments (Docker hosts or Swarm clusters). Portainer is meant to be as simple to deploy as it is to use. It consists of a single container that can run on any Docker engine (can be deployed as Linux container or a Windows native container, supports other platforms too). Portainer allows you to manage your all your Docker resources (containers, images, volumes, networks and more) ! It is compatible with the standalone Docker engine and with Docker Swarm mode.

#### Setup
Portainer stack requires the agent deployed to each node that will be required to modify system settings. This agent will reside on an agent_network that exposes the host at tcp 9001. The Portainer container will be limited to manager nodes only and be accessible through Traefik proxy.

Setup these environment variables:
```
export HOSTDOMAIN=domain.com
export TRAEFIK_NETWORK=traefik-public
```

#### Optional things to configure on agent
```
environment:
  AGENT_CLUSTER_ADDR Should be equal to the service name prefixed by "tasks." when deployed inside an overlay network
  AGENT_CLUSTER_ADDR: tasks.agent
  AGENT_PORT: 9001
  LOG_LEVEL: debug
  AGENT_SECRET: NDOWndwa8idh2QG2b
  CAP_HOST_MANAGEMENT: 1
volumes:
  -/:/host
```

- environment - AGENT_SECRET only used when bypassing ad-hoc deploy connection.
- environment - CAP_HOST_MANAGEMENT enables additional host features like filesystem and hardware management.
- volumes - host option enables additional host features like filesystem and hardware management.

#### Networks needed for agent
`docker network create --driver overlay --attachable agent_network`

#### Docker stack deploy
`docker stack deploy -c portainer-agent-stack-traefik.yml portainer`

#### Bug fixes with Traefik and Portainer
[Traefik label fixes](https://github.com/containous/traefik/issues/563#issuecomment-421360934)
