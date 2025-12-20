# 1 - Install Docker Engine on Ubuntu

## References
- [Docker engine] :(https://docs.docker.com/engine/install/ubuntu/)

## 1.1 - Uninstall old versions
Before you can install Docker Engine, you need to uninstall any conflicting packages.
- Run the following command to uninstall all conflicting packages:
  ```bash
  sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc podman-docker containerd runc | cut -f1)
  ```
**Note:** Images, containers, volumes, and networks stored in `/var/lib/docker/` aren't automatically removed when you uninstall Docker.

## 1.2 - Install using the apt repository
- Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker apt repository. Afterward, you can install and update Docker from the repository.

## 1.3 - Set up Docker's apt repository.
```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```

## 1.4 - Install the Docker packages.
- To install the latest version, run:
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 1.5 - The Docker service starts automatically after installation. To verify that Docker is running, use:
```bash
sudo systemctl status docker
```

## 1.6 - Some systems may have this behavior disabled and will require a manual start:
```bash
sudo systemctl start docker
```

## 1.7 - Verify that the installation is successful by running the hello-world image:
```bash
sudo docker run hello-world
```
**Note:** This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.

```text
root@ip-172-31-35-219:~# sudo docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

root@ip-172-31-35-219:~#
```
**Note:** You have now successfully installed and started Docker Engine.
