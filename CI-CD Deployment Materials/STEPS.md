

---

## **Interactive Guide: Jenkins & Docker Setup for MLOps Project**

---

### **Step 1: Install Docker Desktop**
- **Action**: Download and install Docker Desktop from [Docker's official website](https://www.docker.com/products/docker-desktop).
- **Run Docker**: Start Docker Desktop and ensure it runs in the background.

---

### **Step 2: Setup Jenkins Container**

1. **Create a Custom Jenkins Folder:**
   - **Action**: In your working directory, create a folder named `custom_jenkins`.

2. **Create a Dockerfile inside `custom_jenkins` Folder:**
   - **Action**: Open VS Code or your preferred text editor.
   - **Create a file named `Dockerfile` inside `custom_jenkins` and paste the following code:**

    ```dockerfile
    # Use the Jenkins image as the base image
    FROM jenkins/jenkins:lts

    # Switch to root user to install dependencies
    USER root

    # Install prerequisites and Docker
    RUN apt-get update -y && \
        apt-get install -y apt-transport-https ca-certificates curl gnupg software-properties-common && \
        curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
        echo "deb [arch=amd64] https://download.docker.com/linux/debian bullseye stable" > /etc/apt/sources.list.d/docker.list && \
        apt-get update -y && \
        apt-get install -y docker-ce docker-ce-cli containerd.io && \
        apt-get clean

    # Add Jenkins user to the Docker group (create if it doesn't exist)
    RUN groupadd -f docker && \
        usermod -aG docker jenkins

    # Create the Docker directory and volume for DinD
    RUN mkdir -p /var/lib/docker
    VOLUME /var/lib/docker

    # Switch back to the Jenkins user
    USER jenkins
    ```

3. **Build Jenkins Docker Image:**
   - Open a terminal (CMD or VS Code Terminal) and run the following commands:
   
    ```bash
    cd custom_jenkins
    docker build -t jenkins-dind .
    ```

   - **Check Images**:
    ```bash
    docker images
    ```

4. **Run Jenkins Docker Container:**
   - **Action**: Run the following command to start Jenkins in a Docker container.

    ```bash
    docker run -d --name jenkins-dind \
    --privileged \
    -p 8080:8080 -p 50000:50000 \
    -v //var/run/docker.sock:/var/run/docker.sock \
    -v jenkins_home:/var/jenkins_home \
    jenkins-dind
    ```

5. **Verify Container is Running:**
   - **Check Running Containers**:
    ```bash
    docker ps
    ```

   - **Get Jenkins Logs**:
    ```bash
    docker logs jenkins-dind
    ```

   - **Action**: Copy the alphanumeric password provided in the logs for Jenkins installation.

---

### **Step 3: Access Jenkins and Complete Setup**

1. **Open Jenkins in Browser:**
   - **Action**: Go to [localhost:8080](http://localhost:8080).
   - **Paste the Password**: Use the alphanumeric password you copied earlier.

2. **Install Suggested Plugins:**
   - Follow the prompts to install the suggested plugins.

3. **Create Jenkins User:**
   - Set up your user credentials and complete the setup.

---

### **Step 4: Install Python and Required Packages in Jenkins Container**

1. **Access the Jenkins Container Terminal:**
   - **Action**: Run the following command to access the Jenkins container's terminal as root.

    ```bash
    docker exec -u root -it jenkins-dind bash
    ```

2. **Install Python and Pip:**
   - **Action**: Run these commands to install Python 3 and pip.

    ```bash
    apt update -y
    apt install -y python3
    python3 --version
    ln -s /usr/bin/python3 /usr/bin/python
    python --version
    apt install -y python3-pip
    apt install -y python3-venv
    exit
    ```

3. **Restart Jenkins Container:**
   - **Action**: Restart Jenkins container to apply changes.

    ```bash
    docker restart jenkins-dind
    ```

4. **Sign in Again to Jenkins Dashboard:**
   - **Action**: Go back to the Jenkins dashboard and sign in with your user credentials.

---

### **Step 5: Project Dockerfile Setup**

1. **Create Dockerfile for the Project:**
   - **Action**: Create a Dockerfile in your project directory with the following content:

    ```dockerfile
    # Use a lightweight Python image
    FROM python:slim

    # Set environment variables to prevent Python from writing .pyc files & Ensure Python output is not buffered
    ENV PYTHONDONTWRITEBYTECODE=1 \
        PYTHONUNBUFFERED=1

    # Set the working directory
    WORKDIR /app

    # Install system dependencies required by LightGBM
    RUN apt-get update && apt-get install -y --no-install-recommends \
        libgomp1 \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

    # Copy the application code
    COPY . .

    # Install the package in editable mode
    RUN pip install --no-cache-dir -e .

    # Train the model before running the application
    RUN python pipeline/training_pipeline.py

    # Expose the port that Flask will run on
    EXPOSE 5000

    # Command to run the app
    CMD ["python", "application.py"]
    ```

2. **Build Docker Image for the Project:**
   - **Action**: Run the following command to build the image:

    ```bash
    docker build -t your_project_image .
    ```

3. **Run the Project Docker Container:**
   - **Action**: Run the following command to start the project container:

    ```bash
    docker run -d -p 5000:5000 your_project_image
    ```

---

### **Step 6: Install Google Cloud CLI in Jenkins Container**

1. **Install Google Cloud SDK:**
   - **Action**: Follow these commands to install the Google Cloud SDK inside the Jenkins container:

    ```bash
    docker exec -u root -it jenkins-dind bash
    apt-get update
    apt-get install -y curl apt-transport-https ca-certificates gnupg
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
    echo "deb https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
    apt-get update && apt-get install -y google-cloud-sdk
    gcloud --version
    exit
    ```

---

### **Step 7: Grant Docker Permissions to Jenkins User**

1. **Grant Docker Permissions:**
   - **Action**: Run the following commands to give Docker permissions to the Jenkins user:

    ```bash
    docker exec -u root -it jenkins-dind bash
    groupadd docker
    usermod -aG docker jenkins
    usermod -aG root jenkins
    exit
    ```

2. **Restart Jenkins Container:**
   - **Action**: Restart the Jenkins container to apply changes.

    ```bash
    docker restart jenkins-dind
    ```

---
