Swarmprom on Traefik
---
[Swarmprom](https://github.com/stefanprodan/swarmprom) is a starter kit for Docker Swarm monitoring with Prometheus, Grafana, cAdvisor, Node Exporter, Alert Manager and Unsee.

#### Setup
Services:
- Prometheus (metrics database) http://<swarm-ip>:9090
- Grafana (visualize metrics) http://<swarm-ip>:3000
- Node-exporter (host metrics collector)
- Cadvisor (containers metrics collector)
- Dockerd-exporter (Docker daemon metrics collector, requires Docker experimental metrics-addr to be enabled)
- Alertmanager (alerts dispatcher) http://<swarm-ip>:9093
- Unsee (alert manager dashboard) http://<swarm-ip>:9094
- Caddy (reverse proxy and basic auth provider for prometheus, alertmanager and unsee)

Setup these environment variables:
```
export ADMIN_USER=username
export ADMIN_PASSWORD=password
export HASHED_PASSWORD=$(openssl passwd -apr1 $ADMIN_PASSWORD)
export DOMAIN=domain.com
export TRAEFIK_PUBLIC_TAG=traefik-public
export SLACK_URL=https://hooks.slack.com/services/TOKEN
export SLACK_CHANNEL=devops-alerts
export SLACK_USER=alertmanager
```

#### Docker stack deploy
`docker stack deploy -c docker-compose.traefik.yml swarmprom`

#### Testing URLs
```
http://grafana.domain.com
http://alertmanager.domain.com
http://prometheus.domain.com
http://unsee.domain.com
```
