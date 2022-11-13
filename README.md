# Overte Domain Server Docker Images

Contained in this repo are two docker images which are used to build and run the Overte domain server as a docker image.

Also contained is a docker-compose.yml file to run the domain server on your server using docker-compose.

# Build Instructions

To build the domain server runtime image (Dockerfile.runtime), you must first build the overte server builder image (Dockerfile.build).

- Build the builder image by running the following command (lengthy process): 
```sh 
docker build -t domain-server-builder -f ./Dockerfile.build .
```
- Upon completion of the above, build the runtime container with the following command:
```sh 
docker build -t domain-server -f ./Dockerfile.runtime .
```

- Once the build is completed, you will be able to run the domain server either with docker-compose (see the contained file and change the `image` to `domain-server`), or by running the following:
```sh
docker run -d --name overte-server -p 40100-40102:40100-40102 -p 40100-40102:40100-40102/udp -p 48000-48006:48000-48006/udp -v $(pwd)/logs:/var/log -v $(pwd)/data:/root/.local/share/Overte --restart unless-stopped domain-server
```

# Prebuilt Image

If you would prefer, a prebuilt image for amd64 environments can be used by replacing `domain-server` with `akamicah/overte-domain-server:latest` in either the `docker run` command or the `docker-compose.yml` file.

