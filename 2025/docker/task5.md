### Task 5: Manage Your Image with Docker Hub
---
1. **Tag Your Image:**  
   - Tag your image appropriately:
     ```bash
     docker tag <your-username>/sample-app:latest <your-username>/sample-app:v1.0
     docker tag python-app-mini:latest python-app-mini:v1.0
---    ```
2. **Push Your Image to Docker Hub:**  
   - Log in to Docker Hub if necessary:
     ```bash
     docker login
     ```
   - Push the image:
     ```bash
     docker tag python-app-mini:latest rutuja696/python-app-mini:v1.0
     docker push rutuja696/python-app-mini:v1.0
---   ```
3. **(Optional) Pull the Image:**  
   - Verify by pulling your image:
     ```bash
     docker pull rutuja696/python-app-mini:v1.0