# Docker

## Start


### Run a docker file
```bash
docker run hello-docker
```

### Version
```bash
# 查看版本
docker version
```

### Make a app to docker file
Add a *Dockerfile* with no extensions
```bash
# This is an exmaple dockerfile to run a javascript app.

# Start FROM an image already on hub.docerk.com / dockerhub
FROM linux
# : means the version/tag
# FROM node:alpine

# Copy the current files in to the container file system. 
# Here the example means to copy all files in the current dir in to the /app directory in the container. 
COPY . /app

# This make the following cmds to run under /app, no need to implict write /app/name.app
WORKDIR /app

# Below are the cmds to run the app in the container.
CMD node app.js
```

### Pack the docker file
```bash
# -t: tag
docker build -t hello-docker .
```

### List all images
```bash
docker images
# docker images ls
```

## Update
```bash

```