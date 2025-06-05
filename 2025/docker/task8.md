# Task 8: Orchestrate with Docker Compose
---
1. **Create a docker-compose.yml File:**  
   - Write a `docker-compose.yml` file that defines at least two services (e.g., your sample app and a database).
   - Include definitions for services, networks, and volumes.

   '''bash
   version: "3.8"

services:
  mysql:
    user: "${UID}:${GID}"
    image: mysql:5.7
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: devops
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin
    volumes:
      - ./mysql-data:/var/lib/mysql
      - ./message.sql:/docker-entrypoint-initdb.d/message.sql
    networks:
      - twotier
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-uroot", "-proot"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 60s

  flask-app:
    image: trainwithshubham/two-tier-flask-app:latest
    container_name: flask-app
    ports:
      - "5000:5000"
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: root
      MYSQL_DB: devops
    depends_on:
      - mysql
    networks:
      - twotier
    restart: always
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:5000/health || exit 1"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 30s

networks:
  twotier:

   '''
   
2. **Deploy Your Application:**  
   - Bring up your application using:
     ```bash
     docker-compose up -d
     ```
   - Test the setup, then shut it down using:
     ```bash
     docker-compose down
     ```
3. **Document the Process:**  
   - Explain each service and configuration in your `solution.md`.
