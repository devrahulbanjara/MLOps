# Docker

## 📦 What is Docker?

Think of Docker like instant noodles.

- Traditional cooking (like with cauliflower or chicken) varies because every chef adds a different amount of masala (spices like turmeric, coriander, salt). The result? Different taste.
- Docker is like instant noodles – it comes with the noodles and the exact amount of spice mix. So no matter who makes it, it tastes the same.

➡️ **Docker standardizes your application and its environment**, just like the spice pack does with noodles.

---

## 🤔 Why Do We Need Docker?

### 1. 🧪 Consistency Across Environments

**Problem:**  
Applications behave differently in dev, test, and prod due to variations in dependencies, OS, or config.

**Solution:**  
Docker bundles the application with its dependencies, configs, and OS libraries – ensuring consistent behavior across environments.

**What problem does this solve?**

- No more "It works on my machine"
- Stable deployments across all stages

---

### 2. 🧼 Isolation

**Problem:**  
Running multiple applications on the same system can lead to:

- Dependency clashes
- Resource contention

**Solution:**  
Each Docker container runs in its **own isolated environment**, with its own dependencies and runtime.

**What problem does this solve?**

- No interference between apps
- Enables running different versions of libraries side-by-side

---

### 3. 📈 Scalability

**Problem:**  
Scaling apps manually to handle load is hard.

**Solution:**  
Docker allows **horizontal scaling** by running multiple container instances of the same app.

**What problem does this solve?**

- Easily increase capacity
- Integrates well with orchestration tools like Kubernetes

---

## 🛠️ Docker Core Concepts

| Concept             | Definition                                                   |
| ------------------- | ------------------------------------------------------------ |
| **Dockerfile**      | Text file with instructions to build a Docker image          |
| **Image**           | A snapshot of the environment (read-only)                    |
| **Container**       | A running instance of an image                               |
| **Docker Daemon**   | The background service that builds, runs, and manages Docker |
| **Docker Client**   | CLI that talks to the daemon                                 |
| **Docker Registry** | A place to store and share images (e.g. Docker Hub)          |

---

## 🔰 First Steps: Hello World

```bash
docker pull hello-world
docker run hello-world
```

**What happens:**

- Docker client talks to Docker daemon.
- Daemon pulls the hello-world image from Docker Hub.
- A container is created from the image.
- It runs and prints output to the terminal.

---

### 🐧 Run Ubuntu Bash

```bash
docker run -it ubuntu bash
```

---

## 📁 Dockerfile Example

**Create a Dockerfile**

```Dockerfile
# Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

---

**Build Image**

```bash
docker build -t my-python-app .
```

**Run Container**

```bash
docker run -d --name mycontainer my-python-app
```

**Stop Container**

```bash
docker stop mycontainer
```

---

## ☁️ Push and Pull from Docker Hub

**Tag your image**

```bash
docker tag my-python-app username/my-python-app:latest
```

**Push to Docker Hub**

```bash
docker push username/my-python-app:latest
```

**Pull from Docker Hub**

```bash
docker pull username/my-python-app:latest
```

---

## 🧃 Docker Compose

**Why Docker Compose?**  
When you have multiple services (e.g., app + database + cache), Compose lets you define and run them with a single command.

**docker-compose.yml Example**

```yaml
version: "3"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

**Run Compose**

```bash
docker-compose up
```

**Stop Compose**

```bash
docker-compose down
```

---

## 🌐 Docker Networking

Docker supports three main types of networks:

| Type   | Use Case                         |
| ------ | -------------------------------- |
| bridge | Default, containers on same host |
| host   | Shares host network stack        |
| none   | No network access                |

**Example: Custom Bridge Network**

```bash
docker network create mynetwork
docker run -d --name app --network mynetwork my-python-app
docker run -d --name db --network mynetwork postgres
```

---

## 🔌 Docker Port Mapping

Expose container ports to the host:

```bash
docker run -p 8080:80 nginx
```

- Left side = Host port
- Right side = Container port
- Visit `http://localhost:8080` in your browser.

---

## 💾 Docker Volumes

Volumes persist data outside the container lifecycle.

**Create Volume**

```bash
docker volume create mydata
```

**Mount Volume**

```bash
docker run -v mydata:/data ubuntu
```

**Or bind to host directory:**

```bash
docker run -v $(pwd)/logs:/app/logs my-python-app
```

---

## 🖼️ Docker Image Commands

```bash
# List images
docker images

# Remove image
docker rmi image_id
```

---

## 📦 Container Commands

```bash
# List running containers
docker ps

# List all containers
docker ps -a

# Stop a container
docker stop container_id

# Remove a container
docker rm container_id
```

---

## 📚 Resources

- [Docker Official Docs](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Cheat Sheet](https://dockerlabs.collabnix.com/docker/cheatsheet/)

---
