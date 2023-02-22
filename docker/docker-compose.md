# docker-compose

- [Restart Containers After Changes in Configuration](#restart-containers-after-changes-in-configuration)
- [Remove Volumes to Avoid Silly Problems](#remove-volumes-to-avoid-silly-problems)

## Restart Containers After Changes in Configuration

Use the `--build` option of `docker compose up`.

```sh
docker compose up -d --build
```

## Remove Volumes to Avoid Silly Problems

Sometimes, you need to change some configuration variables for a container and restart it.
Doing `docker compose down` is not enough since it does not delete volumes and old configuration
can persist. To be sure that volumes are deleted, use the `-v` option of `docker compose`.

```sh
docker compose down -v
```
