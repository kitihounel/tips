# docker-compose

- [List all compose projects](#list-all-compose-projects)
- [List all services in a project](#list-all-services-in-a-project)
- [Restart containers after changes in config](#restart-containers-after-changes-in-config)
- [Remove volumes to avoid silly problems](#remove-volumes-to-avoid-silly-problems)

## List all compose projects

```sh
docker compose ls --all
```

The `-a` or `--all` flag forces the command to include stopped projects in the output.

## List all services in a project

To view a list of all service names defined in the current compose config file
without showing container states, use the `config` command:

```sh
docker compose config --services
```

## Restart containers after changes in config

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
