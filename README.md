# Jenkins CI Pipeline with Docker

This project demonstrates a simple CI pipeline using **Jenkins, GitHub, Docker, and Docker Hub**.

The application is a basic HTML and CSS website.

Whenever code is pushed to GitHub, a webhook automatically triggers Jenkins. Jenkins then checks the application files, builds a Docker image, and pushes it to Docker Hub.

## Pipeline Flow

```text
Developer
    ↓
Git Push
    ↓
GitHub
    ↓
Webhook
    ↓
Jenkins
    ↓
Test
    ↓
Build Docker Image
    ↓
Push to Docker Hub
    ↓
Success
```
test
