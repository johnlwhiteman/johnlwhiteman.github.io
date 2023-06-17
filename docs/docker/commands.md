# Docker - Commands

# Running
```bash
# Pull image
docker pull cyberxsecurity/ansible

# Run image to create container
# Warning: Each time run, a new container created
docker run -ti cyberxsecurity/ansible:latest bash

# List all images
docker images -a

# List all containers
sudo docker container list -a

# List running containers
sudo docker ps

# Start container by ame
docker start stoic_bule

# Attach to container if running
docker attach stoic_bule
```

## Purging
```bash
docker stop $(docker ps -a -q)
docker rm -f $(docker ps -a -q)
docker system prune --all -f
docker rmi $(docker images -a -q)
docker volume prune -f
docker rm $(docker volume ls -q)
docker network prune -f
```

## References

