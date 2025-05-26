### Task 3: Explore Docker Terminologies and Components
---
1. **Document Key Terminologies:**  
   - In your `solution.md`, list and briefly describe key Docker terms such as image, container, Dockerfile, volume, and network.

- #### Docker Image
    - Definition: A read-only template with instructions to create a container.
    - Analogy: Like a "blueprint" or "recipe" (e.g., python:3.9-slim).

    - Key Points:
        - Built from a Dockerfile.
        - Stored in registries (Docker Hub, ECR).
        - Immutable (changes create new layers).

- #### Container
    - Definition: A runnable instance of an image.
    - Analogy: A "living house" built from the blueprint (image).

    - Key Points:
        - Isolated process with its own filesystem.
        - Ephemeral (can be stopped/deleted).
        - Shares the host OS kernel (lightweight).

- #### Dockerfile
    - Definition: A text file with commands to build an image.
    - Example:

    ```bash
    dockerfile
    FROM python:3.9
    COPY . /app
    RUN pip install -r requirements.txt
    ```
    - Key Points:
        - Each instruction creates a layer.
        - Order affects build caching.

- #### Volume
    - Definition: Persistent storage for containers.
    - Purpose: Retain data after container stops.

    - Types:
        - Named volumes: Managed by Docker (docker volume create).
        - Bind mounts: Link to host directories (-v /host/path:/container/path).

- #### Network
    - Definition: Isolated communication layer for containers.
    - Types:
        - Bridge: Default network for containers on one host.
        - Host: Shares host’s network directly.
        - Overlay: Connects containers across multiple hosts.

    - Use Case:
    ```bash
    docker network create my_net
    docker run --network=my_net my_app
    ```
    ---
- **Explain the main Docker components (Docker Engine, Docker Hub, etc.) and how they interact.**

- #### Docker Engine
    - What it is: The core runtime that executes containers.
    - Components:
    - Docker Daemon (dockerd): Background service managing images, containers, networks, and volumes.
    - Docker CLI: Command-line tool to interact with the daemon (e.g., docker run).
    - Containerd: Underlying container runtime (handles low-level operations like starting/stopping containers).
    - Role:
        - Builds images from Dockerfile.
        - Runs containers from images.
        - Manages storage, networking, and lifecycle.

- #### Docker Hub
    - What it is: A cloud-based registry for Docker images (like GitHub for code).
    - Key Features:
        - Hosts public/private images (e.g., nginx, python).
        - Automated builds from GitHub/Bitbucket.
        - Vulnerability scanning for images.
    - Interaction:
        - The Docker Engine pulls (docker pull) and pushes (docker push) images to/from Docker Hub.
    - Example:

    ```bash
    docker pull nginx:latest  # Fetches from Docker Hub
    ```

- #### Docker Images
    - What they are: Immutable templates for containers (layered filesystem + metadata).
    - Interaction:
        - Built by Docker Engine from a Dockerfile (docker build).
        - Stored locally or in registries (Docker Hub, AWS ECR).

- #### Docker Containers
    - What they are: Runnable instances of images.
    - Interaction:
    - Created by Docker Engine (docker run).
    - Isolated using kernel namespaces/cgroups.
    - Ephemeral (data persists only if volumes are used).

- #### Docker Volumes
    - What they are: Persistent storage for containers.
    - Interaction:
    - Created/managed by Docker Engine (docker volume create).
    - Mounted to containers:
    ```bash
    docker run -v my_volume:/path/in/container
    ```

- #### Docker Networking
    - What it is: Virtual networks for container communication.
    - Types:
        - Bridge: Default private network for containers on one host.
        - Host: Bypasses isolation, using host’s network directly.
        - Overlay: Connects containers across multiple hosts (for Swarm/Kubernetes).
    - Interaction:
        - Created by Docker Engine (docker network create).
    - Used when running containers:

    ```bash
    docker run --network=my_bridge_network
    ```

- #### Docker Compose
    - What it is: Tool for defining/running multi-container apps.
    - Interaction:
        - Uses a docker-compose.yml file to define services, networks, volumes.
        - Docker Engine executes the setup:

    ```bash
    docker-compose up
    ```

- #### How Components Work Together
    - Developer writes a Dockerfile → Docker Engine builds an image.
    - Image is pushed to Docker Hub → Team pulls it (docker pull).
    - Docker Engine runs a container from the image (docker run).
    - Volumes attach persistent storage; Networks enable communication.
    - Docker Compose orchestrates multi-container apps.


