### Task 4: Optimize Your Docker Image with Multi-Stage Builds
1. **Implement a Multi-Stage Docker Build:**  
   - Modify your existing `Dockerfile` to include multi-stage builds.
    ```bash
            # Build Stage

        FROM python:3.9-slim As builder

        # Defining work directoy

        WORKDIR /app

        # Copy dependency file first for efficient caching
        COPY requirement.txt .
        RUN pip install --no-cache-dir -r requirement.txt --target=/app/deps

        # Copy application source code
        COPY . .

        #Here one stage is completed

        #stage 2 starts here

        # Final Distroless Stage
        FROM gcr.io/distroless/python3-debian11
        WORKDIR /app

        # Copy dependencies from the builder stage
        COPY --from=builder /app/deps /app/deps
        COPY --from=builder /app .

        # Set environment variables
        ENV PYTHONUNBUFFERED=1
        ENV PYTHONPATH="/app/deps"

        # Expose the application port
        EXPOSE 8000

        # Run the application
        CMD ["run.py"]

    ```
    cmd => docker build -f  ./Dockerfile-multi -t  python-app-mini:latest  .
   
2. **Compare Image Sizes:**  
   - Build your image before and after the multi-stage build modification and compare their sizes using:
     ```bash
        docker build -f  ./Dockerfile-multi -t  python-app-mini:latest  .

     ```
     Previous image size is : 137MB
     After distroless image size is: 62.8MB
3. **Document the Differences:**  
   - #### The benefits of multi-stage builds and the impact on image size.
      - Multi-stage builds are a powerful feature in Docker that allow you to use multiple FROM statements in a single Dockerfile. Each FROM instruction starts a new stage, and you can selectively copy artifacts from one stage to another. This approach is especially useful for creating optimized production images without including unnecessary build-time dependencies.

      - #### Benefits of Multi-Stage Builds
         - Smaller Final Image Size
            - Only the necessary files and binaries are copied to the final image, omitting development tools, compilers, or    package managers used during the build process.
            - For example, a Node.js app built in an image with build tools like npm and node-gyp can be copied into a minimal runtime image like node:alpine without the build tools.

         - Improved Security
            - Smaller images with fewer packages mean fewer potential vulnerabilities.
            - Build-time secrets or tools are not present in the final runtime image.
            - Cleaner and More Maintainable Dockerfiles
            - Instead of managing temporary files or complex clean-up commands, you can isolate build logic in one stage and copy only the output.
            - Easier to read and reason about the image-building process.

         - Better Performance for CI/CD Pipelines
            - Layer caching is more efficient when each stage is logically separated.
            - Faster builds and rebuilds when only parts of the application change.
            - Reuse Across Different Environments
            - You can create multiple final stages for different environments (e.g., production vs. development) within a single Dockerfile.

      - #### Impact on Image Size
         - Without Multi-Stage Builds:
            - The final image often contains unnecessary build tools, intermediate files, and unused dependencies, leading to bloated image sizes.
            - Example: A Python app built with build-essential might be 1–2 GB if not cleaned up.

         - With Multi-Stage Builds:
            - Only the runtime essentials (e.g., binaries, libraries) are included, resulting in lean images.
            - Typical reductions: from 1–2 GB to ~100–200 MB, depending on the application and base image.

