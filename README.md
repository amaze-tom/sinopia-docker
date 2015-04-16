## Sinopia (Docker Image)

[Sinopia](https://github.com/rlidwka/sinopia) is a private npm repository server.

This repo uses [v1.2.1](https://github.com/rlidwka/sinopia/tree/v1.2.1) release with a minor modification to lib/index.js which allows a trust proxy for an nginx container. The maintained repo can be found [here](https://github.com/RnbWd/sinopia/tree/v1.2.1)

Using with iojs v1.7.1 - let me know if there's any issues with this version. The storage path is also changed in the [config.yaml](https://github.com/RnbWd/sinopia-docker/blob/master/config.yaml) to handle the edge case where htpasswd is installed via npm.

### Options

- To run default container on port 4873

`docker run --name sinopia -d -p 4873:4873 rnbwd/sinopia`

- to sync storage

`docker run --name sinopia -d -p 4873:4873 -v <local-path-to-storage>:/sinopia/storage rnbwd/sinopia`


- To attach a custom [config.yaml](https://github.com/RnbWd/sinopia-docker/blob/master/config.yaml)

    docker run -v <local-path-to-config>:/sinopia/config.yaml \
    -d -p 4873:4873 rnbwd/sinopia`

- To modify config.yaml, update local config then restart

`docker restart sinopia`

### Building Custom Containers

- From github repository

```
git clone https://github.com/RnbWd/sinopia-docker.git
cd sinopia-docker
docker build -t sinopia .
docker run -d -p 4873:4873 sinopia
```

- Nginx support

Use [nginx-proxy](https://registry.hub.docker.com/u/rnbwd/nginx/) or [jwilder/nginx-proxy](https://registry.hub.docker.com/u/jwilder/nginx-proxy/)

After running the nginx-proxy, run the sinopia container with env var VIRTUAL_HOST

```
docker run -e VIRTUAL_HOST=foo.bar.com \
  -v <local-path-to-config>:/sinopia/config.yaml \
  --name sinopia -d -P rnbwd/sinopia
```

## Links

* [rnbwd/sinopia](https://github.com/RnbWd/sinopia)
* [nginx-proxy](https://registry.hub.docker.com/u/jwilder/nginx-proxy/)
