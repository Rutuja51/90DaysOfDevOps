# Task 6: Persist Data with Docker Volumes
---
**Delete particular volumes**
```bash
docker volume ls
docker volume rm <volume_name>

```

**Create a Docker Volume:**  
   - Create a Docker volume:
     ```bash
     docker volume create my_volume
     ```
**Run a Container with the Volume:**  
   - Run a container using the volume to persist data:
     ```bash
     docker run -d -v my_volume:/app/data <your-username>/sample-app:v1.0
     run -d  -p 8000:8000 -v demo:/app/data rutuja696/python-app-mini:v1.0

 **Inspect docker volumes**
   ```bash
   docker volume inspect demo
   Output --
      [
      {
         "CreatedAt": "2025-05-27T13:58:18Z",
         "Driver": "local",
         "Labels": null,
         "Mountpoint": "/var/lib/docker/volumes/demo/_data",
         "Name": "demo",
         "Options": null,
         "Scope": "local"
      }
   ]

   ```
   **Create text file inside docker nnd how to see that in volumes**
   ```sh
   echo "Hello demo... Good Morining " > demofile.txt
   sudo su
   cd /var/lib/docker/volumes/demo/_data
   ls
   ``` 
**Document the Process:**  
   - Explain how Docker volumes help with data persistence and why they are useful.
    - Volumes are directories stored outside the container's writable layer, managed by Docker. They reside on the host filesystem, usually under /var/lib/docker/volumes/, and can be shared across containers.
    
    - How Volumes Help with Data Persistence
        - Survive Container Lifecycle
            - When a container is deleted, its internal filesystem is lost.
            - Volumes persist beyond the container's lifetime.
            - Useful for things like database storage (/var/lib/mysql) or uploaded files in web apps.

    - Isolate Data from Containers
        - Data is stored outside the container image.
        - You can update or replace containers without losing data.

    - Share Data Between Containers
        - Multiple containers can access the same volume.
        - Enables patterns like separating an app container from a data-processing container.

---