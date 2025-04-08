# MEAN CRUD App

This is a full-stack CRUD application built using the **MEAN stack** (MongoDB, Express.js, Angular, Node.js). It is fully containerized using Docker and deployed via a CI/CD pipeline using GitHub Actions.

---

## 🧱 Tech Stack

- **Docker** – Containerization
- **Docker Compose** – Multi-container orchestration
- **Nginx** – Reverse Proxy for Angular frontend
- **GitHub Actions** – CI/CD automation

---

## 🚀 Features

- CRUD operations for tutorials
- Angular frontend with form validation
- RESTful API backend
- MongoDB integration with Mongoose
- CI/CD Pipeline with automatic build and deployment

---

## 🐳 Dockerized Setup

### 1. Build & Run Locally with Docker Compose

```bash
    git clone https://github.com/Lakshman386/mean-crud-app.git
    cd mean-crud-app
    docker-compose up --build

The app will be available at: http://15.206.229.63/tutorials

🤖 CI/CD Pipeline (GitHub Actions)
  Trigger:
      Automatically runs on every push to the main branch.

  Actions:
    Checkout code

      Log in to Docker Hub

      Build and push backend and frontend Docker images

      SSH into remote Ubuntu VM

      Pull the latest code and Docker images

      Restart containers using Docker Compose

[image](https://github.com/user-attachments/assets/88d7f347-7467-4602-a011-715ff6a09605)


🔐 Secrets Required (GitHub Repository Settings → Secrets and Variables)
    Key	                Description
  DOCKER_USERNAME	    Docker Hub username
  DOCKER_PASSWORD	    Docker Hub password or access token
  VM_HOST	            Public IP of the target VM
  VM_USER	            SSH username (e.g., ubuntu)
  SSH_PRIVATE_KEY	    Your private SSH key for the VM

📁 Project Structure
  mean-crud-app/
    ├── backend/
    │   ├── app/
    │   ├── config/
    │   └── Dockerfile
    ├── frontend/
    │   ├── src/
    │   └── Dockerfile
    ├── nginx/
    │   └── default.conf
    ├── docker-compose.yml
    ├── .github/workflows/
    │   └── main.yml (CI/CD Pipeline)

📦 Docker Hub Images
    Backend: lakshman386/backend-app
    Frontend: lakshman386/frontend-app

🌐 Deployment URL
  http://15.206.229.63/tutorials
![image](https://github.com/user-attachments/assets/b61b410e-e44a-4e6d-a62b-c74ba0ac53aa)

