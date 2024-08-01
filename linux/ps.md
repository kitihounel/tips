# ps

## Forest Option

The `ps` command offers the `--forest` that displays processes in a tree.

```bash
ps -ef --forest
```

Here an example output (from a docker container):

```txt
UID        PID  PPID  C STIME TTY          TIME CMD
node        85     0  0 14:11 pts/0    00:00:00 /bin/sh
node        97    85 99 14:37 pts/0    00:00:00  \_ ps -ef --forest
node         1     0  0 14:10 ?        00:00:00 /sbin/docker-init -- /bin/sh -c npm install && npm run start:debug
node         7     1  0 14:10 ?        00:00:00 /bin/sh -c npm install && npm run start:debug
node        49     7  0 14:10 ?        00:00:00  \_ npm run start:debug
node        60    49  0 14:10 ?        00:00:00      \_ sh -c nest start --debug 0.0.0.0:9229 --watch
```
