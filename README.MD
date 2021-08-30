## Practice Docker With Multiple Containers

### Build the docker image

```
docker build -t jenny/visits:latest .
```

```
docker run jenny/visits:latest
> start
> node index.js

Listening on port 8081
node:events:371
      throw er; // Unhandled 'error' event
      ^

Error: connect ECONNREFUSED 127.0.0.1:6379
    at TCPConnectWrap.afterConnect [as oncomplete] (node:net:1146:16)
Emitted 'error' event on RedisClient instance at:
    at RedisClient.on_error (/app/node_modules/redis/index.js:406:14)
    at Socket.<anonymous> (/app/node_modules/redis/index.js:279:14)
    at Socket.emit (node:events:394:28)
    at emitErrorNT (node:internal/streams/destroy:157:8)
    at emitErrorCloseNT (node:internal/streams/destroy:122:3)
    at processTicksAndRejections (node:internal/process/task_queues:83:21) {
  errno: -111,
  code: 'ECONNREFUSED',
  syscall: 'connect',
  address: '127.0.0.1',
  port: 6379
}
```

In order to solve this problem, tried to run another container docker run redis and then run my image again to start the container, and these two containers still can't communicate with each other.

## Run the docker compose

```
docker-compose up
Building node-app
[+] Building 4.1s (11/11) FINISHED                                                                       
 => [internal] load build definition from Dockerfile                                                0.0s
 => => transferring dockerfile: 148B                                                                0.0s
 => [internal] load .dockerignore                                                                   0.0s
 => => transferring context: 2B                                                                     0.0s
 => [internal] load metadata for docker.io/library/node:alpine                                      3.9s
 => [auth] library/node:pull token for registry-1.docker.io                                         0.0s
 => [1/5] FROM docker.io/library/node:alpine@sha256:1ee1478ef46a53fc0584729999a0570cf2fb174fbfe037  0.0s
 => [internal] load build context                                                                   0.0s
 => => transferring context: 26.22kB                                                                0.0s
 => CACHED [2/5] WORKDIR /app                                                                       0.0s
 => CACHED [3/5] COPY ./package.json .                                                              0.0s
 => CACHED [4/5] RUN npm install                                                                    0.0s
 => [5/5] COPY . .                                                                                  0.0s
 => exporting to image                                                                              0.0s
 => => exporting layers                                                                             0.0s
 => => writing image sha256:f9c2b0f20542623f012985a08ae68621bb309516bb8f99454625e7928dd13be2        0.0s
 => => naming to docker.io/library/practice-docker-multi-containers-visits_node-app                 0.0s
```