# Docker

## Build

Always build with tag to avoid dangling images:

```sh
docker build -t hugo-ext-test:latest .
```

Rebuild ignoring cache:

```sh
docker build --no-cache -t hugo-ext-test:latest .
```

## Run

Avoid having tons of containers which you then have to remove:

```sh
# start new named container and open shell, stops when you exit shell
docker run it --name hugo-ext-test hugo-ext-test sh

# once it stopped, restart (don't use docker run) and login
docker start -i hugo-ext-test

# or login later if you start it w/o "-i", it remains running when you exit
docker exec -it hugo-ext-test sh
```

## Remove

List dangling images:

```sh
docker images -f "dangling=true"
```

Remove dangling images:

```sh
docker images -f "dangling=true" -q | xargs docker rmi
```

## Dockerfile

```Dockerfile
# always executed on `docker run`, can not be overwritten
ENTRYPOINT ["sh", "run.sh"]

# serves as arguments to above, can be overwritten, can be used alone
CMD ["--opt", "hello"]
```
