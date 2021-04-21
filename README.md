Docker Swarm with statefulset
---

1. install rexray (third-party ebs)`docker plugin install rexray/ebs EBS_ACCESSKEY=access_key EBS_SECRETKEY=secret_key`
2. check plugin is installed `docker plugin ls`
3. test it `docker volume ls`
4. create volume `docker volume create --driver=rexray/ebs --name=<volume-name> --opt=size=<gigabyte> --opt=type=<gp2/gp3-default-standart>`
5. claim volume in compose
```
version: '3.3'

volumes:
  rexray-volume:
    external: true

services:
  nginx:
    image: nginxdemos/hello
    ports:
       - 8080:80
    volumes:
       - rexray-volume:/usr/share/nginx/html
```

6. run stack `docker stack deploy --compose-file <docker-compose-file> <stack-name>`
7. scale if needed `docker service scale <stack-name>_<service-name>=<scale-count>`
8. get into one container `docker exec -it <container-id-1> /bin/sh`
9. get into volume binding `cd /usr/share/nginx/html`
10. modifying any file
11. exiting container, and get into another container `docker exec -it <container-id-2-or-any> /bin/sh`
12. get into volume binding `cd /usr/share/nginx/html`
