# Docker Swarm Cluster Testing

This README provides instructions for testing a Docker Swarm cluster.

## Prerequisites

- Docker installed on all nodes
- Docker Swarm initialized
- Nodes joined to the Swarm

## Steps to Test Docker Swarm Cluster

### 1. Initialize Docker Swarm

On the manager node, run:
```sh
docker swarm init
```

### 2. Join Worker Nodes

On each worker node, run the command provided by the `docker swarm init` output, for example:
```sh
docker swarm join --token <token> <manager-ip>:2377
```

### 3. Deploy a Service

Deploy a simple service to the Swarm:
```sh
docker service create --name hello-world --replicas 3 nginx
```


### initiaise with yml
```sh
docker stack deploy -c docker-compose.yml my_stack
```

### check running services
docker service ls

### 4. Verify Service Deployment

Check the status of the service:
```sh
docker service ls
```

Verify that the tasks are running:
```sh
docker service ps hello-world
```

### 5. Scale the Service

Scale the service to 5 replicas:
```sh
docker service scale hello-world=5
```

### 6. Remove the Service

Remove the service when testing is complete:
```sh
docker service rm hello-world
```

## Conclusion

You have successfully tested your Docker Swarm cluster. For more information, refer to the [Docker Swarm documentation](https://docs.docker.com/engine/swarm/).


docker swarm init --advertise-addr 127.0.0.1


Swarm initialized: current node (1bmcydieskw9l3bi10ades2kj) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-48k6e6spoip7u0dvusxfveop4o8yugdgrrb0icmfixk4rk1xa3-f3gqzjr0swojg9wg3wmssttqn 127.0.0.1:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.



Since we are testing on a single machine, add all roles to the same node:

bash
Copy
Edit
docker node update --label-add role=primary $(docker node ls --format "{{.ID}}")
docker node update --label-add role=secondary $(docker node ls --format "{{.ID}}")


docker node update --label-add role=backup $(docker node ls --format "{{.ID}}")



ajith@ajith-OMEN-by-HP-Laptop-16-c0xxx:~/work/docker_swarn$ docker node ls
ID                            HOSTNAME                           STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
y6lbxqs0068x31i8i0w8xdl6h     DEV-VISHNU-P-LAP                   Ready     Active                          27.5.1
1bmcydieskw9l3bi10ades2kj *   ajith-OMEN-by-HP-Laptop-16-c0xxx   Ready     Active         Leader           27.4.1

ajith@ajith-OMEN-by-HP-Laptop-16-c0xxx:~/work/docker_swarn$ docker inspect y6lbxqs0068x31i8i0w8xdl6h


docker stack deploy -c docker-compose.yml my_stack