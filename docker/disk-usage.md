# Disk usage

- [Get information about used disk space](#get-information-about-used-disk-space)
- [Get log files size](#get-log-files-size)
- [Clear log file](#clear-log-file)
- [Limit logs size](#limit-logs-size)

## Get information about used disk space

The `docker system df` command displays information regarding the amount of disk space used by the Docker daemon.

By default the command displays a summary of the data used:

```txt
docker system df

TYPE                TOTAL               ACTIVE              SIZE                RECLAIMABLE
Images              5                   2                   16.43 MB            11.63 MB (70%)
Containers          2                   0                   212 B               212 B (100%)
Local Volumes       2                   1                   36 B                0 B (0%)
```

Use the `-v, --verbose` flag to get more detailed information:

```txt
docker system df -v

Images space usage:

REPOSITORY  TAG       IMAGE ID        CREATED         SIZE        SHARED SIZE    UNIQUE SIZE   CONTAINERS
my-curl     latest    b2789dd875bf    6 minutes ago   11 MB       11 MB          5 B           0
my-jq       latest    ae67841be6d0    6 minutes ago   9.623 MB    8.991 MB       632.1 kB      0
<none>      <none>    a0971c4015c1    6 minutes ago   11 MB       11 MB          0 B           0
alpine      latest    4e38e38c8ce0    9 weeks ago     4.799 MB    0 B            4.799 MB      1
alpine      3.3       47cf20d8c26c    9 weeks ago     4.797 MB    4.797 MB       0 B           1

Containers space usage:

CONTAINER ID   IMAGE           COMMAND    LOCAL VOLUMES   SIZE     CREATED           STATUS                      NAMES
4a7f7eebae0f   alpine:latest   "sh"       1               0 B      16 minutes ago    Exited (0) 5 minutes ago    hopeful_yalow
f98f9c2aa1ea   alpine:3.3      "sh"       1               212 B    16 minutes ago    Exited (0) 48 seconds ago   anon-vol

Local Volumes space usage:

NAME                                                               LINKS    SIZE
07c7bdf3e34ab76d921894c2b834f073721fccfbbcba792aa7648e3a7a664c2e   2        36 B
my-named-vol                                                       0        0 B
```

- `SHARED SIZE` is the amount of space that an image shares with another one (i.e. their common data)
- `UNIQUE SIZE` is the amount of space that's only used by a given image
- `SIZE` is the virtual size of the image, it's the sum of `SHARED SIZE` and `UNIQUE SIZE`

**Note:** Network information isn't shown, because it doesn't consume disk space.

**Source:** Docker [docs](https://docs.docker.com/reference/cli/docker/system/df). 

## Get log files size

Because the native `docker ps --size` command does not include log file sizes, you must locate the explicit
disk path of the log file using docker inspect and check it with `du`:

```sh
docker inspect --format='{{.LogPath}}' <container_name_or_id> | xargs sudo du -sh
```

**Note:** We need to run the second part of the command as root because a standard uer may not have the rights to access
the logs files.

To list every container's active log file size alongside its corresponding name, run:

```sh
sudo du -sh $(docker inspect --format='{{.LogPath}}' $(docker ps -qa)) 2>/dev/null
```

## Clear log file

Do not delete the physical log file manually. Doing so can break the connection to the
logging daemon. Instead, safely truncate the file down to 0 bytes while the container
is actively running:

```sh
sudo truncate -s 0 $(docker inspect --format='{{.LogPath}}' <container_name_or_id>)
```

## Limit logs size

A good way to prevent logs from taking all your space is to add this to your docker-compose:

```yaml
services:
  some-service:
    image: some-image
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
```

The actual options depend on the driver used and a description can be found in the documentation.

**Source:**: [SO](https://stackoverflow.com/a/59765205).
