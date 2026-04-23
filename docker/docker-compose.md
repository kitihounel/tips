# docker-compose

- [Restart containers after changes in configuration](#restart-containers-after-changes-in-configuration)
- [Remove volumes to avoid silly problems](#remove-volumes-to-avoid-silly-problems)

## Restart containers after changes in configuration

Use the `--build` option of `docker compose up`.

```sh
docker compose up -d --build
```

## Remove volumes to avoid silly problems

Sometimes, you need to change some configuration variables for a container and restart it.
Doing `docker compose down` is not enough since it does not delete volumes and old configuration
can persist. To be sure that volumes are deleted, use the `-v` option of `docker compose`.

```sh
docker compose down -v
```
