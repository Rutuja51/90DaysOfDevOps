# Task 2: Create a Dockerfile for a Sample Project
---
## 1. Select or Create a Sample Application:
- Choose a simple application (for example, a basic Node.js, Python, or Java app that prints “Hello, Docker!” or serves a simple web page).
    - Create app.py (python file in docker folder)
## 2. Write a Dockerfile:
- Create a Dockerfile that defines how to build an image for your application.
- Include comments in your Dockerfile explaining each instruction.

    - created docker file name as "Dockerflie".
    ```bash
    # Import base image OS you can get this from google python official
    FROM python:3.9-slim
    # Working directory where your code will get store in container
    WORKDIR /app
    #Copy source code to conatiner's working directoy
    COPY app.py .
    # here . means /app directory from container which current directory u can also do src/* app/
    # Now given command for insatlling libraries and compling commands
    RUN pip install
    #Expose ports . Deafult pythong is runnign on port 8000
    EXPOSE 80
    # here
    #Command to serve application
    CMD ["python","app.py"]
    ```

- Build your image using
```bash
    docker build -t app-python:latest .
```

## 3. Verify your Build :
- Run your container locally to ensure it works as expected:
```bash
    docker run -d -p 8080:80 -name <your-username>/sample-app:latest
    # -d => run in detached mode or in background preocess
    # -p => specifying ports
    #  8080:80 => <host-port>:<container-port>
    # -name => provides conatiner name
```
- Verify the container is running with:
```bash
    docker ps
```
- Check logs using
```bash
    docker logs <container_id>
```
