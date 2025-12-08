***
_Powered by Gemini and Perplexity_
***

## Video Notes

1. [Docker crash course](https://www.youtube.com/watch?v=pg19Z8LL06w)
2. [Docker v Kubernetes](https://www.youtube.com/watch?v=oGPjzCBZGzg)

Containers packages code, Docker creates the package, and Kubernetes manages the fleet of packages.

## What are Containers?

A container is a standardized unit of software that packages up code and all its dependencies (libraries, settings, system tools) so the application runs quickly and reliably from one computing environment to another.

Think of it like a shipping container in the real world.

Key Characteristics:

- Lightweight: Unlike Virtual Machines (VMs) which require a full Operating System (OS) for every app, containers share the host machine’s OS kernel. They only contain what they need to run the app.
- Portable: A container runs exactly the same on a developer's laptop, a test server, or a cloud production server. "It works on my machine" is no longer a valid excuse.
- Isolated: Containers are isolated from one another. If one crashes, it doesn't take down the host or other containers.

## What is Docker?

Docker is the commercial platform and toolkit that made containers easy to use. While the technology for containers (like Linux LXC) existed before, Docker democratized it. -- Dockers package containers

Core Docker Concepts:
- Docker File: A text document that contains all the commands to assemble an image (e.g., "Start with Linux, install Python, copy my code here").
- Docker Image: The read-only template created from the Dockerfile. This is the actual "package" (the blueprint).
- Docker Container: The runnable instance of an image. When you "run" an image, it becomes a container (the actual building).
- Docker Hub: A giant library (registry) where people share container images (like GitHub for binaries).

**Why use it**? It creates a consistent environment. A developer uses Docker to wrap their app in a container, and they can hand that container to the Operations team knowing 100% it will run.

## What is Kubernetes?

Kubernetes (often abbreviated as K8s) is an open-source container orchestration system.

Once you start using Docker, you might end up with hundreds or thousands of containers. Managing them manually is impossible. You need a way to automate deployment, scaling, and management.

Think of Kubernetes as the Traffic Controller or the Manager of the Fleet.

What Kubernetes does:
- Auto-scaling: If your website traffic spikes, Kubernetes automatically creates more containers to handle the load. When traffic drops, it kills them to save money.
- Self-healing: If a container crashes, Kubernetes notices immediately and restarts a new one to replace it.
- Load Balancing: It distributes network traffic intelligently across your containers so no single container is overwhelmed.
- Rolling Updates: It allows you to update your application code incrementally. If the new version breaks, K8s can automatically rollback to the previous version

## How they work together

Step 1 (The Code): You write your application code.

Step 2 (The Container): You use Docker to package that code into a portable container image.

Step 3 (The Orchestration): You tell Kubernetes to run that image. You say, "I want 5 copies of this container running at all times."

Step 4 (The Runtime): Kubernetes takes over, scheduling those containers across your servers and monitoring their health.

***
## Example of dockerfile

```docker
# 1) Base image with runtime
FROM python:3.13-slim

# 2) Workdir inside the container
WORKDIR /usr/src/app

# 3) Install Python deps first for better caching
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 4) Copy the rest of the repo
COPY . .

# 5) Expose the port your app listens on
EXPOSE 8080

# 6) Default command to run the app
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8080"]
```

Key points:
- FROM picks the runtime image (Python, Node, Java, etc.).​
- WORKDIR sets the working directory for subsequent commands.​
- COPY requirements.txt then RUN pip install lets Docker cache dependency installation until requirements change.​
- COPY . . brings in your repo (source, configs, etc.).​
- EXPOSE 8080 documents the container’s port, which Kubernetes or docker run -p will map.​
- CMD [...] defines the default process run when the container starts.​

**How to build and tag the image**
From the repo root (where the Dockerfile is):
```plaintext
docker build -t my-registry/my-app:v1 .
docker push my-registry/my-app:v1
```

### Kubernetes YAML

⬇️run 3 replicas of app image
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    app: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: my-registry/my-app:v1   # image built from your Dockerfile
          ports:
            - containerPort: 8080
```

A minimal Kubernetes example is usually a Deployment (to run your pods) plus a Service (to expose them). These YAMLs would live in your repo, typically under a k8s/ or deploy/ directory. 

Apply:
```bash
kubectl apply -f deployment.yaml
kubectl get pods
```

**Service example**
This exposes the Deployment on a stable cluster IP and port.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app
spec:
  type: ClusterIP
  selector:
    app: my-app
  ports:
    - port: 80        # clients use this port
      targetPort: 8080  # containerPort from the Deployment
```
Apply it:
```bash
kubectl apply -f service.yaml
kubectl get svc
```
