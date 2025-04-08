# 🚀 MEAN CRUD App Deployment (CI/CD + Docker + Nginx)

This repository contains a full-stack CRUD application built using the **MEAN Stack**:
- **MongoDB**
- **Express.js**
- **Angular 15**
- **Node.js**

It is containerized with **Docker**, uses **Nginx** as a reverse proxy, and is deployed using a GitHub Actions **CI/CD pipeline** to an Ubuntu VM.

---

## 📦 Deliverables

- ✅ Step-by-step setup and deployment instructions
- ✅ CI/CD configuration and execution
- ✅ Docker image build and push process
- ✅ Application deployment and working UI
- ✅ Nginx setup and infrastructure details
- ✅ Screenshots and visual references

---

## 🛠️ Step-by-Step Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Lakshman386/mean-crud-app.git
cd mean-crud-app
```

---

### 2. Project Structure

```
mean-crud-app/
├── backend/                 # Node.js + Express + MongoDB
│   └── Dockerfile
├── frontend/                # Angular frontend
│   └── Dockerfile
├── nginx/                   # Nginx config for reverse proxy
│   └── default.conf
├── docker-compose.yml       # Multi-container orchestration
└── .github/workflows/
    └── deploy.yml             # CI/CD pipeline
```

---

### 3. Run Locally with Docker Compose

Ensure Docker is installed. Then run:

```bash
docker-compose up --build
```

Visit: `http://15.206.229.63:80` to view the app.

---

## ⚙️ CI/CD Pipeline (GitHub Actions)

### Trigger

The pipeline runs on every `push` to the `main` branch.

### GitHub Actions Workflow

```yaml
on:
  push:
    branches:
      - main
```

### Actions Performed

- Checkout code
- Authenticate with Docker Hub
- Build and push Docker images
- SSH into remote server
- Pull updated images & restart containers

### Secrets Required

| Secret Key          | Description                    |
|---------------------|--------------------------------|
| `DOCKER_USERNAME`   | Docker Hub username            |
| `DOCKER_PASSWORD`   | Docker Hub password/token      |
| `VM_HOST`           | Public IP of the target VM     |
| `VM_USER`           | SSH username (e.g., `ubuntu`)  |
| `SSH_PRIVATE_KEY`   | SSH private key for the VM     |

---

## 🐳 Docker Images

| Service   | Image Name                    |
|-----------|-------------------------------|
| Backend   | `lakshman386/backend-app`     |
| Frontend  | `lakshman386/frontend-app`    |

---

## 🌐 Nginx Reverse Proxy Setup

Located in `nginx/default.conf`:

```nginx
server {
  listen 80;
  location / {
    root /usr/share/nginx/html;
    index index.html index.htm;
    try_files $uri $uri/ /index.html;
  }
  location /api {
    proxy_pass http://backend:8080;
  }
}
```

This setup:
- Serves Angular frontend
- Proxies `/api` requests to backend

---

## 📸 Screenshots

### ✅ CI/CD Configuration

![CI/CD Workflow](c:\Users\sanag\OneDrive\Pictures\Screenshots\Screenshot 2025-04-08 160400.png)

### 🐳 Docker Build & Push

![Docker Build](c:\Users\sanag\OneDrive\Pictures\Screenshots\Screenshot 2025-04-08 160143.png)

### 🚀 Deployment in Action

![Deployment Output](c:\Users\sanag\OneDrive\Pictures\Screenshots\Screenshot 2025-04-08 153324.png)

### 🖥️ Live UI

![Frontend UI](c:\Users\sanag\OneDrive\Pictures\Screenshots\Screenshot 2025-04-08 153509.png)

### 🌐 Nginx Infrastructure

![Nginx Config](c:\Users\sanag\OneDrive\Pictures\Screenshots\Screenshot 2025-04-08 160731.png)

---

## 📍 Deployment Steps on Ubuntu VM

1. SSH into your VM:
   ```bash
   ssh -i key.pem ubuntu@<VM_PUBLIC_IP>
   ```

2. Install Docker & Docker Compose:
   ```bash
   sudo apt update
   sudo apt install docker.io docker-compose -y
   ```

3. Let the GitHub Action take care of deploying from here!

---

## ✅ Final Output

- App URL: `http://15.206.229.63:80`
- Backend served via Docker
- Frontend served via Nginx
- CI/CD automates deployments on every push to `main`

---

## 🧹 Troubleshooting Tips

- **MongoDB Connection Refused**: Ensure `mongo` is the correct hostname inside Docker Compose.
- **Disk Full Error**: SSH into your VM and run:
  ```bash
  docker system prune -af
  ```
