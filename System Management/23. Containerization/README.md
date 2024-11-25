# Containerization 
Containerization is a method of packaging and running applications in isolated environments such as containers, virtual machines, or serverless setups. This approach ensures efficient, secure, and portable application deployment. Below is a comprehensive guide to understanding containerization and its core components, with a focus on Docker and Linux Containers (LXC).

---

## Overview of Containerization
- **Isolation**: Applications run independently of the host system.
- **Efficiency**: Lightweight, scalable, and suitable for running multiple applications simultaneously.
- **Security**: Reduces the risk of malicious activity affecting the host system.
- **Portability**: Easily deployable across different environments.

---

## Dockers
Docker is an open-source platform that automates the deployment of applications in containers. It utilizes a layered filesystem and resource isolation to provide flexibility and portability.

### **Installing Docker Engine**
To install Docker Engine on an Ubuntu host, use the following script:

```
#!/bin/bash
```

### **Preparation**
```
sudo apt update -y
sudo apt install ca-certificates curl gnupg lsb-release -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### **Install Docker Engine**
```
sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

### **Add user to the Docker group**
```
sudo usermod -aG docker $(whoami)
echo '[!] Log out and log back in for group changes to take effect.'
```

### **Test Docker installation**
```
docker run hello-world
```

### **Creating a Docker Image**
Define a Dockerfile to specify the container configuration. For example:

```
# Use Ubuntu 22.04 as the base image
FROM ubuntu:22.04

# Install necessary packages
RUN apt-get update && apt-get install -y apache2 openssh-server && rm -rf /var/lib/apt/lists/*

# Create a new user
RUN useradd -m docker-user && echo "docker-user:password" | chpasswd

# Grant permissions to the user
RUN chown -R docker-user:docker-user /var/www/html && usermod -aG sudo docker-user && \
    echo "docker-user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Expose necessary ports
EXPOSE 22 80

# Start services
CMD service ssh start && /usr/sbin/apache2ctl -D FOREGROUND
```

### **Build and run the Docker container**

```
# Build the Docker image
docker build -t my_docker_image .

# Run the container
docker run -p 8022:22 -p 8080:80 -d my_docker_image
```

### **Docker Management Commands**

| **Command**                    | **Description**              |
|--------------------------------|------------------------------|
| **docker ps**                  |	List all running containers |
| **docker stop <container>**    |	Stop a running container    |  
| **docker start <container>**   |	Start a stopped container   |
| **docker restart <container>** |	Restart a running container |
| **docker rm <container>**      |	Remove a container          |
| **docker rmi <image>**         |	Remove a Docker image       |
| **docker logs <container>**    |	View logs of a container    |

---

## Linux Containers (LXC)
LXC is a lightweight virtualization technology for running multiple isolated Linux systems on a single host.

### **Installing LXC**
Install LXC on Ubuntu:
```
sudo apt-get install lxc lxc-utils -y
```

### **Creating and Managing LXC Containers**

1) Create a container:
   ```
   sudo lxc-create -n my_container -t ubuntu
   ```
   
2) Manage containers:
   | **Command**                    |	**Description**              |
   |--------------------------------|------------------------------|
   | **lxc-ls**	                    | List all existing containers |
   | **lxc-start -n <container>**	  | Start a stopped container    |
   | **lxc-stop -n <container>**	  | Stop a running container     |
   | **lxc-attach -n <container>**	| Connect to a container       |
   
### **Securing Containers**
- Restrict Access: Limit SSH or other unnecessary services.
- Limit Resources: Configure resource quotas with cgroups.
- Isolate Environments: Use namespaces for process, network, and file system isolation.
  
### **Example: Limiting Resources**

To restrict a container's CPU and memory, edit its configuration file:
```
sudo vim /usr/share/lxc/config/my_container.conf
```

Add the following lines:
```
lxc.cgroup.cpu.shares = 512
lxc.cgroup.memory.limit_in_bytes = 512M
```

Restart the LXC service:
```
sudo systemctl restart lxc.service
```

---

## Conclusion
Containerization, whether through Docker or LXC, offers a robust way to manage and deploy applications efficiently. By understanding their respective tools and security configurations, you can optimize application performance and security in any environment.
