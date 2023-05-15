# docker-compose
flask redis multi-tier application using docker-compose



##  flask and redis sample application using docker-compose 


### Python/Flask application

Project structure:
```
.
├── compose.yaml
├── app
    ├── Dockerfile
    ├── requirements.txt
    └── app.py

```

[_compose.yaml_](compose.yaml)
```
version: "3.3"
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
    environment:
      FLASK_DEBUG: "true"
  redis:
    image: "redis:alpine"
```

## Deploy with docker compose

```
docker-compose up -d
Creating network "docker-compose_default" with the default driver
Creating docker-compose_web_1   ... done
Creating docker-compose_redis_1 ... done

```

## Expected result

Listing containers must show two containers are running and the port mapping as below:
```
 docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED         STATUS         PORTS                                       NAMES
7b211ffdb5b5   redis:alpine         "docker-entrypoint.s…"   7 seconds ago   Up 5 seconds   6379/tcp                                    docker-compose_redis_1
6a483dffc9b6   docker-compose_web   "flask run"              7 seconds ago   Up 5 seconds   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp   docker-compose_web_1
```

After the application starts, open the web browserand type `http://localhost:5000`
```
curl localhost:5000
Hello World! FROM UNNATI I have been seen 1 times.

curl localhost:5000
Hello World! FROM UNNATI I have been seen 2 times.
```

Stop and remove the containers
```
$ docker compose down
```
