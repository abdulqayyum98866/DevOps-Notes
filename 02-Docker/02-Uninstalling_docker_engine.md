# Uninstall Docker Engine
## References
- [Docker engine uninstalling] :(https://docs.docker.com/engine/install/ubuntu/)
> **Note:** $indicates a normal user shell prompt.
Do not type $ while running the command.

## 1 - Uninstall the Docker Engine, CLI, containerd, and Docker Compose packages:
```bash
sudo apt purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

## 2 - Images, containers, volumes, or custom configuration files on your host aren't automatically removed. To delete all images, containers, and volumes:
```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

## 3 - Remove source list and keyrings
```bash
sudo rm /etc/apt/sources.list.d/docker.sources
sudo rm /etc/apt/keyrings/docker.asc
```

**Note:** You have to delete any edited configuration files manually.
