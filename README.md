# docker-dude


```
Attention! This is a server container, not a client!


```

Just type

```bash
docker run \
  --name dude \
  --detach \
  --restart unless-stopped \
  --volume /etc/localtime:/etc/localtime:ro --volume /etc/timezone:/etc/timezone:ro \
  --volume dude:/dude/data \
  --publish 180:180 \
  --publish 1443:1443 \
  --publish 514:514/udp \
  --publish 2210:2210 \
  --publish 2211:2211 \
  --health-cmd /healthcheck.sh --health-start-period 3s --health-interval 1m --health-timeout 1s --health-retries 3 \
  --log-opt max-size=10m --log-opt max-file=5 \
  lupael/dude
```

and your Dude is ready.

Ports published:

| Port | Description
| ---: | -----------
| 180 | HTTP
| 1443 | HTTPS
| 514/udp | Syslog
| 2210 | Insecure Dude
| 2211 | Secure Dude

You can stop your Dude with

```bash
docker stop dude
```

and run it again with

```bash
docker start dude
```

## Where is my data?

```bash
docker volume inspect --format '{{ .Mountpoint }}' dude
```

## Uninstall

```bash
docker rm --force dude
docker image rm lupael/dude
docker volume rm dude
```
