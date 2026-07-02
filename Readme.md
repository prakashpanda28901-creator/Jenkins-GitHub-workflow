# CI/CD Pipeline using Jenkins and Docker

A DevOps project demonstrating the implementation of a Continuous Integration and Continuous Deployment (CI/CD) pipeline using **Jenkins**, **Docker**, **Git**, and **GitHub**. The project automates the process of building and deploying a containerized Python Flask application using a Jenkins Pipeline.

---

# Project Overview

This project demonstrates how Jenkins can automate application deployment. A simple Python Flask application is containerized using Docker. Jenkins is configured with a Pipeline job that pulls the latest source code from GitHub, builds a Docker image, stops the existing running container, and deploys a new container automatically.

---

# Technologies Used

- Jenkins
- Docker
- Git
- GitHub
- Python
- Flask

---

# Project Structure

```
Jenkins-GitHub-workflow/
│
├── app.py
├── requirements.txt
├── Dockerfile
└── README.md
```

---

# Project Workflow

```
Developer
     │
     │ git push
     ▼
GitHub Repository
     │
     ▼
Jenkins Pipeline
     │
     ├── Checkout Source Code
     ├── Build Docker Image
     ├── Stop Existing Container
     ├── Remove Existing Container
     └── Deploy New Container
              │
              ▼
       Flask Application
```

---

# Features

- Automated CI/CD pipeline using Jenkins
- Source code checkout from GitHub
- Docker image creation using Jenkins
- Automatic Docker container deployment
- Automatic replacement of the old container
- Consistent and repeatable deployments

---

# Prerequisites

Install the following tools before starting the project:

- Git
- Docker
- Jenkins
- Python 3
- Flask

---

# Clone the Repository

```bash
git clone https://github.com/prakashpanda28901-creator/Jenkins-GitHub-workflow.git

cd Jenkins-GitHub-workflow
```

---

# Run the Application Locally

Build the Docker image:

```bash
docker build -t flask-app .
```

Run the Docker container:

```bash
docker run -d -p 5000:5000 --name flask-container flask-app
```

Verify the running container:

```bash
docker ps
```

Access the application:

```
http://localhost:5000
```

About page:

```
http://localhost:5000/about
```

---

# Push Project to GitHub

```bash
git init

git add .

git commit -m "Initial commit"

git branch -M main

git remote add origin https://github.com/prakashpanda28901-creator/Jenkins-GitHub-workflow.git

git push -u origin main
```

---

# Configure Jenkins

## Add Jenkins User to Docker Group

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Start Jenkins:

```bash
sudo systemctl start jenkins
```

Check Jenkins status:

```bash
sudo systemctl status jenkins
```

---

# Create Jenkins Pipeline Job

1. Open Jenkins Dashboard.
2. Click **New Item**.
3. Enter a job name (e.g., **job2**).
4. Select **Pipeline**.
5. Click **OK**.
6. Scroll down to the **Pipeline** section.
7. Choose **Pipeline script**.
8. Paste the following pipeline script.
9. Save the pipeline.
10. Click **Build Now**.

---

# Jenkins Pipeline Script

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {
                git branch: 'main',
                    url: 'https://github.com/prakashpanda28901-creator/Jenkins-GitHub-workflow.git'
            }

        }

        stage('Build Docker Image') {

            steps {
                sh 'docker build -t flask-app .'
            }

        }

        stage('Stop Old Container') {

            steps {
                sh '''
                docker stop flask-container || true
                docker rm flask-container || true
                '''
            }

        }

        stage('Deploy Container') {

            steps {
                sh '''
                docker run -d \
                --name flask-container \
                -p 5000:5000 \
                flask-app
                '''
            }

        }

    }

}
```

---

# Pipeline Execution Flow

```
GitHub Repository
        │
        ▼
Checkout Source Code
        │
        ▼
Build Docker Image
        │
        ▼
Stop Existing Container
        │
        ▼
Remove Existing Container
        │
        ▼
Deploy New Docker Container
        │
        ▼
Flask Application Running
```

---

# Verify Deployment

Check running containers:

```bash
docker ps
```

View logs:

```bash
docker logs flask-container
```

Open the application:

```
http://localhost:5000
```

Open the About page:

```
http://localhost:5000/about
```

---

# Useful Docker Commands

Build Docker image

```bash
docker build -t flask-app .
```

Run Docker container

```bash
docker run -d -p 5000:5000 --name flask-container flask-app
```

List running containers

```bash
docker ps
```

List Docker images

```bash
docker images
```

Stop container

```bash
docker stop flask-container
```

Remove container

```bash
docker rm flask-container
```

Remove image

```bash
docker rmi flask-app
```

---

# Learning Outcomes

Through this project, I learned:

- CI/CD pipeline fundamentals
- Jenkins Pipeline configuration
- GitHub integration with Jenkins
- Docker image creation
- Docker container deployment
- Build automation
- Deployment automation
- Container lifecycle management
- Basic DevOps workflow

---

# Author

**Prakash Panda**

DevOps & Cloud Enthusiast

GitHub: https://github.com/prakashpanda28901-creator

---

# License

This project is created for learning and educational purposes.