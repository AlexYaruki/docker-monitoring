# docker ps

## Reference: https://docs.docker.com/engine/reference/commandline/ps/
---

``` docker ps ```

Displays status of running containers

Example result:

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                        NAMES
b80286ad976d        glassfish           "/bin/sh -c 'asadmin…"   6 minutes ago       Up 6 minutes        4848/tcp, 8181/tcp, 0.0.0.0:8080->8080/tcp   suspicious_hawking
```
Columns:
* CONTAINER ID - Unique id of container on the local machine
* IMAGE - Docker image used in container
* COMMAND - Command used by container at startup
* CREATED - Time since creation of container
* STATUS - Current status of container. Possible statuses 
    - created 
    - restarting
    - running
    - removing
    - paused 
    - exited (displays also exit code)
    - dead
 * PORTS - Network ports for container. For example (4848/tcp, 8181/tcp, 0.0.0.0:8081->8080/tcp) means
    - container exposes port 4848 and 8181
    - container published its port 8080 to host port 8081
 * NAMES - Name of container. Random if not specified. For docker-compose, its base directory + service name
---
``` docker ps -a``` or ```docker ps --all```

Displays status of all containers

Example result:
```
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS                     PORTS                                        NAMES
b80286ad976d        glassfish                   "/bin/sh -c 'asadmin…"   37 minutes ago      Up 37 minutes              4848/tcp, 8181/tcp, 0.0.0.0:8080->8080/tcp   suspicious_hawking
9d6d5aa7423c        google/cadvisor             "/usr/bin/cadvisor -…"   23 hours ago        Exited (255) 2 hours ago   0.0.0.0:8080->8080/tcp                       monitoring_cadvisor_1
9ddb4ecbabbf        elasticsearch:6.6.1         "/usr/local/bin/dock…"   23 hours ago        Exited (78) 23 hours ago                                                monitoring_elasticsearch_1
b2dcf501e57a        monitoring_prometheusbeat   "/prometheusbeat -e …"   23 hours ago        Exited (1) 23 hours ago                                                 monitoring_prometheusbeat_1
5417d6f77145        monitoring_prometheus       "/bin/prometheus --c…"   23 hours ago        Exited (255) 2 hours ago   0.0.0.0:9090->9090/tcp                       monitoring_prometheus_1
47d62f55e47c        grafana/grafana             "/run.sh"                23 hours ago        Exited (255) 2 hours ago   0.0.0.0:3000->3000/tcp                       monitoring_grafana_1
1fa1b3db022a        kibana:6.6.1                "/usr/local/bin/kiba…"   23 hours ago        Exited (255) 2 hours ago   0.0.0.0:5601->5601/tcp                       monitoring_kibana_1
cb72eeaf3bb9        influxdb:1.7.4              "/entrypoint.sh infl…"   7 days ago          Exited (255) 4 days ago    0.0.0.0:8086->8086/tcp                       docker_monitoring_influxdb_1
9aacb6cddc89        google/cadvisor:v0.33.0     "/usr/bin/cadvisor -…"   7 days ago          Exited (255) 4 days ago    0.0.0.0:8080->8080/tcp                       docker_monitoring_cAdvisor_1
fa3ba21b4b61        grafana/grafana             "/run.sh"                7 days ago          Exited (255) 4 days ago    0.0.0.0:3000->3000/tcp                       docker_monitoring_grafana_1
```
---

```docker ps -s``` or ```docker ps --size```

Same as ```docker ps``` + SIZE column reporting used storage 

Example result:
```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                        NAMES                SIZE
b80286ad976d        glassfish           "/bin/sh -c 'asadmin…"   27 minutes ago      Up 27 minutes       4848/tcp, 8181/tcp, 0.0.0.0:8080->8080/tcp   suspicious_hawking   80.2MB (virtual 853MB)
```

For the example above 80.2MB (virtual 853MB):
* 80.2MB means how much data was written by container inside writable layer
* (virtual 853MB) means how much space used by image of container (read-only)

---
```docker ps --no-trunc```

Displays full info for container. This allows to get full-length container id and whole command. Otherwise, only shortned version will be displayed.

Example output:
```
CONTAINER ID                                                       IMAGE               COMMAND                                         CREATED             STATUS              PORTS                                        NAMES
b80286ad976db08c493c2b85e904aca7e355918d8f7e1819cca3d7ac5a43bed6   glassfish           "/bin/sh -c 'asadmin start-domain --verbose'"   44 minutes ago      Up 44 minutes       4848/tcp, 8181/tcp, 0.0.0.0:8080->8080/tcp   suspicious_hawking
```