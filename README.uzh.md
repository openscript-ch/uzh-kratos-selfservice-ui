1. Make sure you have Docker (>= 25.0.3) and Buildx (>=0.13.1) installed
1. Build images from this projects root
   1. Selfservice app `docker build -t local/weltentdecker/uzh-kratos-selfservice-ui-node:prod .`
1. Push image to production environment with `docker save local/weltentdecker/uzh-kratos-selfservice-ui-node:prod | ssh -C pebbles.uzh podman load`
   - If you have [`pv`](http://ivarch.com/programs/pv.shtml) you can display some progress with `docker save local/weltentdecker/uzh-kratos-selfservice-ui-node:prod | pv -s $(docker image inspect local/weltentdecker/uzh-kratos-selfservice-ui-node:prod --format='{{.Size}}') | ssh -C pebbles.uzh podman load`
   - Make sure you are connected to the UZH VPN
   - Make sure you have the ssh connection set up for the hostname `pebbles.uzh` or change the host in the command above
1. Reload container with `systemctl --user restart 'podman-compose@uzh-pebbles-infra'`
