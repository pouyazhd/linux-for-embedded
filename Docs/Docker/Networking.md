# Docker Networking

As a container deployed, it has to run in a network. Docker has 7 types of netowrking plans.

1. Bridge
2. User-defined
3. host
4. MACVLAN
5. MACVLAN trunk
6. IPVLAN (L2)
7. IPVLAN (L3)

## Show the networks

As docker create it's own networks, it also let the users see the networks. To see current networks use command:

```bash
docker network ls
```

To inspect a running container:

```bash
docker inspect <container name>
```

look at the section networks and you will find the networks which this container connected to.

## Bridge

Default network of docker. If you deploy an image, by default it will be `bridge` type. To access the machine from outside the docker, user must expose the port using `-p` flag in docker run command.

> You can expose multiple port from a container.

## User-defined network

Docker let you create multiple netowrks. It is recommended that containers related to an application/product be located on a separate network. This type of network are also `bridge` type but they are separate. To create a network:

```bash
docker network create <your-defined-network-name>
```

> Check if the network created using `docker network ls` command.

And to connect an application to this network, pass `--network` flag to docker run command:

```bash
docker run --network <your-defined-network-name> [Other options and flags] <imageName:imageTag>
```

## Host network

Docker also let the users to connect their applications to host netowrk. It means the container use the same netowrk the host use. In this network, no defining port is needed.

```bash
docker run --network host [Other options and flags] <imageName:imageTag>
```
