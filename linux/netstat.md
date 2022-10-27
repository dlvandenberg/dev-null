# `netstat` command

Netstat, meaning _network statistics_, is a command to display detailed information about how your computer is communicating with other computers or network devices.

## Usage
```bash
$ netstat [-a] [-b] [-e] [-f] [-n] [-o] [-p potocol] [-r] [-s] [-t] [-x] [-y] [time_interval] [/?]
```
| option | description                                                                                                                            |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| -a     | Displays active _TCP_ connections, _TCP_ connections in the _listening_ state and _UDP_ ports that are being listened to.              |
| -b     | Displays the process's actual file name. **Might greatly extend netstat's execution time**.                                            |
| -e     | Shows statistics about your network connection. Includes _bytes_, _unicast packets_, _non-unicast packets_, etc.                       |
| -f     | Force netstat to display the _Fully Qualified Domain Name_ (FQDN) for each _foreign_ IP address when possible.                         |
| -n     | Prevent netstat from attempting to determine _host names_ for foreign IP addresses. **Might greatly reduce netstat's execution time**. |
| -o     | Display _process identifier_ (PID) associated with each displayed connection.                                                          | 

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
