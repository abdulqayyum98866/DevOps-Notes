# Docker daily using commands

> **Note:** $indicates a normal user shell prompt.
Do not type $ while running the command.

**Note:** Depending on your Docker system configuration, you may be required to preface each `docker` command with `sudo`. 
To avoid having to use `sudo` with the `docker` command, your system administrator can create a Unix group called `docker` and add users to it.

- Note : Add the hostname in the docker group

```bash
sudo vim /etc/group
```
```md
[Adding hostname(ubuntu) in docker group]
```
<img width="733" height="347" alt="image" src="https://github.com/user-attachments/assets/09ca3478-924f-4c28-b846-915fe25dd2f7" />


**OR**
- Try this
```bash
ubuntu@ip-172-31-35-219:~$ sudo usermod -aG docker ubuntu
```
```bash
ubuntu@ip-172-31-35-219:~$ id ubuntu
```
---
**Output**
```text
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),4(adm),24(cdrom),27(sudo),30(dip),105(lxd),113(docker)
ubuntu@ip-172-31-35-219:~$
```

## References
- [Docker hub] :(https://hub.docker.com/)
- [Docker_commands] :(https://docs.docker.com/reference/cli/docker/)

## 1 - Check the docker service are running or not
```bash
systemctl status docker
```

## 2 - List all the images

```bash
docker images
```

## 3 - Create and run a new container from an image
```bash
docker run hello-world
```

## 4 - Running container
```bash
docker ps
```

## 5 - Exited(dead) container
```bash
docker ps -a
```

## 6 - Pull the image from docker hub

## References
- [Docker Nginx] :(https://hub.docker.com/_/nginx)
```text
docker pull imagename
```

**Example:**
```bash
docker pull nginx
```

## 7 - Give the name of the image and run the background
```text
--name -> image name

-d(ditach mode)     -> run in background (continuous process not like hello-world )

-p stands for port mapping (port publishing).

Nginx runs on 80 port
```

```bash
docker run --name myweb -p 7090:80 -d nginx
```

**Additionally**
- To run the nginx website
- Turn on the EC2 intance security group Type: `All traffic`  Source: `0.0.0.0/0` bellow image has been shown.
  
**Edit inbound rules**

<img width="1366" height="451" alt="Screenshot 2025-12-17 024125" src="https://github.com/user-attachments/assets/f0161e91-d8f2-4cf5-ae23-a335389fed48" />

## 8 - Stop the container
```text
docker stop "container name or ID"
```

## 9 - Start the container
```text
docker start "container name or ID"
```

**Note:** Container is a process
```bash
ps -ef
```
**Note: Nginx process is running**

<img width="652" height="94" alt="image" src="https://github.com/user-attachments/assets/b48cf553-1271-4a79-9d62-0bc02c961347" />

- Container running from a dir

<img width="651" height="177" alt="image" src="https://github.com/user-attachments/assets/0c9beeb0-4a7c-41b3-8416-6f71a2f7146a" />

- Container runs directly from the images
  
<img width="654" height="142" alt="image" src="https://github.com/user-attachments/assets/958b3f5c-9fdd-4ca1-86e2-e81099f7d53d" />

## 10 - Execute the container
```md
docker exec "container ID or name"
```
## 11 - Execute and see container dirs
```md
docker exec "container name or ID" ls /
```
<img width="291" height="238" alt="image" src="https://github.com/user-attachments/assets/1c1f4874-bdd5-47ca-a5c5-c40b1f7ed129" />

## 12 - Attach container(cmd runs into the container)
```md
docker exec "container name or ID" /bin/bash
```
## 13 - Connect the command
```md
docker exec -it "container name or ID" /bin/bash
```

```text
-i  → interactive
-t  → allocate a pseudo-TTY (terminal)
```

**Note:** 
**What happens?**

- Opens a bash shell inside the running container

- You can type commands interactively

- Feels like you “SSH into” the container (but it’s NOT SSH)

**What is a pseudo-TTY?**

- TTY = Teletype / Terminal

- A pseudo-TTY (pseudo terminal) is a software-based terminal that behaves like a real terminal.

---

**Output**

<img width="696" height="98" alt="image" src="https://github.com/user-attachments/assets/fe12a945-f9f6-4114-b15c-4405c6b6293b" />

**Note** 
- Container is light weight.
- So most of the packages not there.
- This is debian based container.
- apt update then download the packages.

<img width="729" height="539" alt="image" src="https://github.com/user-attachments/assets/5167e2f7-3b32-43f3-9385-87e438e118cd" />

- Then install the ps package `# apt install procps -y`
- See the PID 1 nginx process.
- 34 /bin/bash process.
- Then exit the cmd, the /bin/bash process has been exited.
- Some containers have no bash shell, you give sh.

<img width="520" height="100" alt="image" src="https://github.com/user-attachments/assets/5b00fe6a-29c4-4a84-9e92-4ed68b72c081" />

## 14 - Remove the image
```md
docker rmi "image ID"
```
## 15 - Remove the container
```md
docker rm "container name or ID"
```

**Note:** 
- Some process running in /bin/bash shell.
- So we interact with /bin/bash shell.
- `docker pull ubuntu` this ubuntu container process runs on /bin/bash shell.
- When we run `docker run ubuntu` it goes exited state.
- Then we run the container in interactive mode.

```bash
docker run -it ubuntu /bin/bash
```

**For more see the below image**

<img width="716" height="297" alt="image" src="https://github.com/user-attachments/assets/1705587d-21aa-4df7-8762-1983a84e421c" />

## 16 - Restart the container
```md
docker restart "container name or ID"
```

## 17 - Details of container & image
```md
docker inspect "container or ID"
```







