**Docker**   is a platform that lets you package an application and everything it needs to run (code, libraries, dependencies, and configuration) into a container. This makes it easy to run the application consistently across different environments, such as your laptop, a test server, or the cloud.

**Think of it like this**   
Application = a recipe.
Docker container = a lunchbox containing the meal and all the utensils needed to eat it.
Wherever you take the lunchbox, you can enjoy the same meal without worrying about what's available there.

**Why use Docker?**  
Docker solves the classic "it works on my machine" problem by ensuring the application runs the same way everywhere.

Some key benefits:

**Consistency**: The app behaves the same in development, testing, and production.
**Portability**: Containers can run on any system with Docker installed.
Isolation: Each application runs in its own environment without interfering with others.
**Fast startup**: Containers start in seconds because they share the host operating system's kernel.
Efficient resource usage: Containers use fewer resources than traditional virtual machines.

**How Docker works**  

***Docker has a few main components***:

1.**Dockerfile**
A text file with instructions for building an image.

Example:

FROM python:3.12
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD ["python", "app.py"]

2.**Docker Image**

-A read-only template created from a Dockerfile.
-Think of it as a blueprint for creating containers.

3.**Docker Container**

A running instance of an image.
Multiple containers can be created from the same image.

Docker uses two Linux features: **cgroups** and **namespaces**.  
**Docker vs. Virtual Machines**  
Docker Containers	         Virtual Machines
Share the host OS kernel	 Each VM includes its own operating system
Lightweight	                 Heavier
Start in seconds             May take minutes to boot
Lower memory usage           Higher memory usage

infra > os > container engine(docker , podman , ranc) > app > image  

**AWS** (Amazon Web Services) is a cloud platform provided by Amazon.

It gives you infrastructure and services over the internet instead of requiring you to buy and maintain physical servers.

**Bitnami** provides pre-packaged applications and application stacks that are easier to deploy.

**ArvanCloud** (ابر آروان) is a cloud service provider. It offers infrastructure and cloud services similar in concept to AWS, but it is primarily focused on the Iranian market and infrastructure.

These three cloud infrastructure providers provide us with the operating system we need in the form of an image.

docker image (readonly)> container (network ,vloume statefull) > registery (dockerhub)
**Nexus**, **Harbor**, and **Sonatype** are examples of **registry** tools.

If the data is not **persisted** outside the container, it will be lost when the container is removed. This data should be **persisted** on the host OS outside the container.

os > docker > dockerd (demon) >api >dockercli >costumer client  

**api** :An API converts the client’s request into a language that the server can understand.

**client** > docker build (image export) -> registery
           > docker pull -> like download
           >docker run 

**rest api**
request : get - put - post - delet - patch 

**status code** > info 1**
                > success 2**
                > redirection 3**
                > error 4**
                > server 5**

If Docker needs to be run by a regular user, the user must be granted access to the Docker group.

usermod -aG [docker] [username]
docker ps
docker run  (pull+creat+start)
docker run -it ubuntu (down after up)
docker run -dit ubuntu (stay up)
docker rm [id]
docker rm -f $(docker ps -aq) 
docker ps -aq [id]
docker exec -it [containername] /bin/bash
docker run -dit --name [containername] -p 80:80 [imagename]
ss -ntlp
docker run -dit --name [containername] -p 80:82 -p 443:443 [imagename] >Assign these two types of ports to a single container.

**If we want it to listen on a specific IP address**.>
docker run -dit --name [containername] -p ip 8000:8000 udp/tcp [imagename]
**With this command, you can extract the desired data from the container**>
docker inspect [containername] or docker inspect -- format '{{.networksetting,ipaddress}}' [imagename]
**You can also pass a command**>
docker exec [containername] ls /
**You can also pass a variable**>
docker run -dit --name [containername] -e var=ls [imagename]
**It copies files from inside the container to the host server**
docker cp file [containername] : /opt/file1
docker run -dit --name --dns 8.8.8.8 -hostname [containername] --restart=allways [imagename]
docker logs [containername]
docker pull gitlab-ce
docker -dit run --name gitlab-ce -p 80:80 gitlab/gitlab-ce
**docker commit is used to create a new Docker image from the current state of an existing container**
docker commit [idcontainer] new-name

**The order is important, so do it in this order**
1.docker run -dit --name [name] [image] >container create
2.docker exec -it [name] /bin/bash > You enter the container.
3.docker commit [idcontainer] [newname]>You create an image from the container above
4.docker images 
5.docker ps >show container

**docker file**

FROM (It specifies what the base image is)> FROM ubuntu:24.04  
WORKDIR (It specifies the working directory inside the container)> WORKDIR /app
COPY (It copies files from the host system into the image)> COPY . .
ADD (It is similar to COPY, but it provides more capabilities)> ADD app.tar.gz /app/
RUN (It executes the command while building the image)> RUN apt update && apt install -y nginx
ENV (It defines an environment variable)> ENV APP_ENV=production
EXPOSE (It documents/exposes the port used by the application)> EXPOSE 80
CMD (It is the default command that is executed when the container starts)> CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT (It specifies the main application of the container)> ENTRYPOINT ["dotnet", "MyApp.dll"]
ARG (It is a variable that is mainly used during the build process)> ARG VERSION=1.0
USER (It specifies which user the application should run as)> USER appuser
VOLUME (It is used to specify the paths intended for persistent data)> VOLUME ["/var/lib/myapp"]
HEALTHCHECK > HEALTHCHECK CMD curl --fail http://localhost:80 || exit 1
# ==========================================
# 1. Base Image
# ==========================================
FROM nginx:alpine

# ==========================================
# 2. Build-time variable
# ==========================================
ARG APP_VERSION=1.0

# ==========================================
# 3. Environment variables
# ==========================================
ENV APP_ENV=production
ENV APP_VERSION=${APP_VERSION}

# ==========================================
# 4. Working directory
# ==========================================
WORKDIR /usr/share/nginx/html

# ==========================================
# 5. Copy application files
# ==========================================
COPY ./html/ .

# ==========================================
# 6. Run commands during image build
# ==========================================
RUN echo "Building application version ${APP_VERSION}" \
    && echo "Environment: ${APP_ENV}"

# ==========================================
# 7. Expose application port
# ==========================================
EXPOSE 80

# ==========================================
# 8. Volume
# ==========================================
VOLUME ["/usr/share/nginx/html"]

# ==========================================
# 9. Health check
# ==========================================
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD wget --spider -q http://localhost/ || exit 1

# ==========================================
# 10. Default command
# ==========================================
CMD ["nginx", "-g", "daemon off;"]

The difference between ENTRYPOINT and CMD is that with the former, we pass the command, while with the latter, we pass the default command.

docker history app
docker save -o app.tar app:v1 > Create a tar file from the app image and save it here
docker export and inport
docker file mulistage > It means you write the Dockerfile in a way that your desired code is built inside it at the same time, so you don't need to build it externally

**Docker Hub** is a cloud-based registry for Docker images. You can think of it as a GitHub for Docker images.  

**docker login** is used to authenticate your Docker client with a container registry, such as Docker Hub

**docker tag** is used to give an existing Docker image another name/tag. It does not create a new image or copy the image >docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

A **Docker Volume** is a Docker-managed storage location used to persist data outside the container's writable layer
Container deleted
      ↓
Container's own data → usually deleted
      ↓
Docker Volume → data remains

example :
-docker volume create mydata
-docker run -d \
  --name myapp \
  **-v** mydata:/app/data \
  nginx

docker prune > docker prune is used to remove unused Docker resources and free disk space
It's important because Docker can accumulate stopped containers, unused images, networks, and build cache.
-docker container prune
-docker image prune
-docker volume prune
-docker network prune
-docker system prune > Stopped containers
                       Unused networks
                       Dangling images
                       Unused build cache

**docker network**

docker network is used to create and manage networks for communication between Docker containers.
        Docker Network
       /       |       \
   Container  Container  Container
      A          B          C

-docker network ls  
NETWORK ID     NAME      DRIVER
abc123         bridge    bridge
def456         host      host
ghi789         none      null


```bash
-docker network create mynetwork
-docker network ls
-docker run -d \
     --name web \
      --network mynetwork \
       nginx

docker run -d \
  --name app \
  --network mynetwork \
  ubuntu
```
Now app and web are on the same Docker network.

-docker network connect mynetwork mycontainer
-docker network inspect mynetwork
-docker network rm mynetwork

**bridge**  
The default network for containers.
-docker network create mynetwork
**host**  
The container shares the host's network namespace.
-docker run --network host nginx




















