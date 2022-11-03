# `netstat` command

Netstat, meaning _network statistics_, is a command to display detailed information about how your computer is communicating with other computers or network devices.

## Usage
```bash
$ netstat [-ral] [-tuwx] [-enWp]
```

| option | description   |
| ------ | ------------- |
| `-t`   | Routing table |
|        |               |

## Examples
### Show all open ports
```bash
$ netstat -tunlp
```
```bash
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:5432            0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.2:19001         0.0.0.0:*               LISTEN      -
tcp        0      0 :::5432                 :::*                    LISTEN      -
```
