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
        # Base image (OS)

    FROM python:3.9-slim

    # Working directory

    WORKDIR /app

    # Copy src code to container

    COPY . .

    # Run the build commands

    RUN pip install -r requirement.txt

    # expose port 80

    EXPOSE 8000

    # serve the app / run the app (keep it running)

    CMD ["python","run.py"]

    ```
    - Created app.py file where code is present

    ```bash
    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def main():
        return "Hello Docker!"

    ```
    - Creted run.py file to hosting

    ```bash

    from app import app
    app.run(debug=True, host='0.0.0.0', port=8000)

    ```
    - Create requirement.txt to install dependencies

    ```bash
    
    flask==2.2.2
W   erkzeug==2.2.2

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
