# Dockefile
#Docker #DevOps

- Adding environment variable
```Dockerfile
FROM mysql:8.0-oracle

ENV MYSQL_ROOT_PASSWORD mypasswrd
```

- Best practice: pass the value of the variable as an argument.
```Dockerfile
FROM mysql:8.0-oracle

ARG password

ENV MYSQL_ROOT_PASSWORD $password
```

```bash
docker build -t joselpadilla/mysql:1.0 --build-arg password=mypassword .
```

- Setting up a less privileged user
```Dockerfile
…

#create group and user

RUN groupadd -r jose && useradd -g jose jose

#set ownership and permissions

RUN chown -R jose:jose /app

#switch to user

USER jose

CMD ["node", "index.js"]
```



| Variable  | Description | Default |
| DJANGO_DEBUG | Enables Django debug mode | False |
| PORT | Port Django listens on	| 8000 |
| LUAS_STOP | Default stop ID (e.g. win, ran) | win |

