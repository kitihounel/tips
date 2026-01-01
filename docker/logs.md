# Container logs

- [View container logs](#view-container-logs)

## View container logs

### View all logs for a container

```
docker logs <container_name_or_id>
```

### Follow logs in real-time (tail)

```
docker logs -f <container_name_or_id>
```

### View the last N lines of logs

```
docker logs --tail <N> <container_name_or_id>
```

### View logs since a specific time/duration

```
docker logs --since 15m <container_name_or_id>
```

### Show timestamps with each entry

```
docker logs -t <container_name_or_id>
```

### View logs for a compose service

```
docker compose logs <service_name>
```

### Save logs to a file

```
docker logs <container_name_or_id> > logs.txt
```
