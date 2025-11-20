# ps

- [Better output format](#better-output)

## Better output format

Create the following alias in your `.bash_aliases`:

```sh
alias dpsx="docker ps --format '{{printf \"%-12s\" \"CONTAINER ID\"}} | {{.ID}}\t{{printf \"%-12s\" \"IMAGE\"}} | {{.Image}}\t{{printf \"%-12s\" \"COMMAND\"}} | {{.Command}}\t{{printf \"%-12s\" \"CREATED\"}} | {{.CreatedAt}}\t{{printf \"%-12s\" \"STATUS\"}} | {{.Status}}\t{{printf \"%-12s\" \"PORTS\"}} | {{.Ports}}\t{{printf \"%-12s\" \"NAMES\"}} | {{.Names}}' | awk 'BEGIN {FS=\"\t\"} {printf(\"-[Container %2d]------------------------------------------------\n\", NR); for(i=1;i<=NF;i++) print \" \" \$i}'"
```
