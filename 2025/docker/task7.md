### Task 7: Configure Docker Networking
1. **Create a Custom Docker Network:**  
   - #### Create a custom Docker network:
     ```bash
     docker network create my_network
     docker network ls
     docker network inspect my_network

     Output 

        [
        {
            "Name": "my_network",
            "Id": "abb3e2f580bd3fbcfdf353b2ed151a8d0de9fbb4ce77455bbf5b2cdf9787aab5",
            "Created": "2025-05-27T15:21:43.860364229Z",
            "Scope": "local",
            "Driver": "bridge",
            "EnableIPv6": false,
            "IPAM": {
                "Driver": "default",
                "Options": {},
                "Config": [
                    {
                        "Subnet": "172.19.0.0/16",
                        "Gateway": "172.19.0.1" 
                    }
                ]
            },
            "Internal": false,
            "Attachable": false,
            "Ingress": false,
            "ConfigFrom": {
                "Network": ""
            },
            "ConfigOnly": false,
            "Containers": {},
            "Options": {},
            "Labels": {}
        }
    ]

     ```
2. **Run Containers on the Same Network:**  
   - #### Run two containers (e.g., your sample app and a simple database like MySQL) on the same network to demonstrate inter-container communication:
     ```bash
     docker run -d --name sample-app --network my_network <your-username>/sample-app:v1.0
     docker run -d --name my-db --network my_network -e MYSQL_ROOT_PASSWORD=root mysql:latest
     ```
3. **Document the Process:**  
   - #### Describe how Docker networking enables container communication and its significance in multi-container applications.
    - Docker networking is fundamental for enabling communication between containers, both on the same host and across multiple hosts. It’s especially crucial in multi-container applications, where components like a web server, application server, and database need to interact seamlessly.

    - **Container Communication via Docker Networking**
        - Example in Multi-Container App
            Let’s say you have:
             - A web app container
             - A database container
        When both containers are on the same user-defined network:
        Docker assigns each container an internal IP.
        Docker sets up internal DNS so containers can refer to each other by name.

        - Docker provides an isolated network namespace for each container and lets you connect containers to virtual networks that Docker manages.
        - Each container gets:
        - Its own IP address within the Docker network
        - A hostname (typically its container name)
        - The ability to communicate with other containers on the same network using internal DNS


    ---