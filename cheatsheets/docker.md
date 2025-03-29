# Docker

Always build with tag to avoid dangling images:

```sh
docker build -t hugo-ext-test:latest .
```

Avoid having tons of containers which you then have to remove:

```sh
# start new named container and open shell, stops when you exit shell
docker run it --name hugo-ext-test hugo-ext-test sh

# once it stopped, restart (don't use docker run) and login
docker start -i hugo-ext-test

# or login later if you start it w/o "-i", it remains running when you exit
docker exec -it hugo-ext-test sh
```
