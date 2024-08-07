# Docker_dev_tools
Reference: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04 
### Introduction to Docker on Ubuntu 20.04

Docker simplifies managing application processes in containers, which are resource-isolated and more portable than virtual machines. This tutorial covers installing Docker Community Edition (CE) on Ubuntu 20.04, working with containers and images, and pushing an image to a Docker Repository.

### Prerequisites

- Ubuntu 20.04 server with a sudo non-root user and a firewall
- Docker Hub account for creating and pushing images

### Installation Steps
The Docker installation package available in the official Ubuntu repository may not be the latest version. To ensure we get the latest version, we’ll install Docker from the official Docker repository. To do that, we’ll add a new package source, add the GPG key from Docker to ensure the downloads are valid, and then install the package.

First, update your existing list of packages:
### Step-by-Step Docker Installation on Ubuntu 20.04

#### 1. **Update Package List**
First, update your existing list of packages:
```bash
sudo apt update
```

#### 2. **Install Prerequisites**
Install a few prerequisite packages which let `apt` use packages over HTTPS:
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

#### 3. **Add Docker’s GPG Key**
Add the GPG key for the official Docker repository to your system:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

#### 4. **Add Docker Repository**
Add the Docker repository to APT sources:
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

This updates our package database with Docker packages from the newly added repo.

#### 5. **Verify Docker Repository**
Ensure you are about to install from the Docker repo instead of the default Ubuntu repo:
```bash
apt-cache policy docker-ce
```
**Output Example:**
```
docker-ce:
  Installed: (none)
  Candidate: 5:19.03.9~3-0~ubuntu-focal
  Version table:
     5:19.03.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
```

#### 6. **Install Docker**
Finally, install Docker:
```bash
sudo apt install docker-ce
```

#### 7. **Check Docker Status**
Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:
```bash
sudo systemctl status docker
```
**Output Example:**
```
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2020-05-19 17:00:41 UTC; 17s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 24321 (dockerd)
      Tasks: 8
     Memory: 46.4M
     CGroup: /system.slice/docker.service
             └─24321 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```
### Step-by-Step: Executing Docker Command Without Sudo (Optional)

#### 1. **Understanding Default Permissions**
By default, the `docker` command can only be run by the root user or a user in the `docker` group. Attempting to run it otherwise results in:
**Output:**
```
docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See 'docker run --help'.
```

#### 2. **Add User to Docker Group**
To avoid using `sudo` with `docker`, add your username to the `docker` group:
```bash
sudo usermod -aG docker ${USER}
```

#### 3. **Apply Group Membership**
Log out and back in, or use:
```bash
su - ${USER}
```
Enter your user’s password to continue.

#### 4. **Verify Group Membership**
Confirm your user is added to the `docker` group:
```bash
groups
```
**Output:**
```
sammy sudo docker
```

#### 5. **Add Another User (if needed)**
To add a different user to the `docker` group:
```bash
sudo usermod -aG docker username
```

#### 6. **Run Docker Commands**
Now, you can run Docker commands without `sudo`. If not, prepend commands with `sudo`.








### Using Docker Commands

Docker commands follow this structure:
```bash
docker [option] [command] [arguments]
```
To see all subcommands, use:
```bash
docker
```
For help on a subcommand:
```bash
docker docker-subcommand --help
```

### Working with Docker Images

Check Docker Hub access:
```bash
docker run hello-world
```

Search for images:
```bash
docker search ubuntu
```

Download an image:
```bash
docker pull ubuntu
```

List downloaded images:
```bash
docker images
```

### Running a Docker Container

Run a container interactively:
```bash
docker run -it ubuntu
```
Exit the container with:
```bash
exit
```

### Managing Docker Containers

List active containers:
```bash
docker ps
```

List all containers:
```bash
docker ps -a
```

Start a stopped container:
```bash
docker start container_id
```

Stop a running container:
```bash
docker stop container_id
```

Remove a container:
```bash
docker rm container_id
```

### Committing Changes to a Docker Image

Save container state to a new image:
```bash
docker commit -m "message" -a "author" container_id repository/new_image_name
```

### Pushing Docker Images to a Repository

Login to Docker Hub:
```bash
docker login -u docker-registry-username
```

Tag the image if necessary:
```bash
docker tag local-image:tagname new-repo:tagname
```

Push the image:
```bash
docker push docker-registry-username/image-name
```

### Conclusion

You have now installed Docker, worked with images and containers, and pushed an image to Docker Hub. For more details and advanced tutorials, visit DigitalOcean's community tutorials.

For the complete tutorial, refer to the [original guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04).
