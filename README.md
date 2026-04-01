# 🚀 DevOps App with Load Balancing & Rollback

## 📌 Description

This project demonstrates a production-like deployment setup using Docker, Nginx, and GitHub Actions with an automatic rollback mechanism based on health checks.

---

## 🧱 Architecture

Client → Nginx → App1 / App2

---

## ⚙️ Features

- Multi-container application (Docker Compose)
- Load balancing via Nginx
- Health check endpoint (`/health`)
- CI/CD pipeline with GitHub Actions
- Automatic rollback if deployment fails

---

## 📁 Project Structure

devops-app/
├── app.py
├── Dockerfile
├── docker-compose.yml
├── nginx.conf
├── requirements.txt
├── .dockerignore
├── .gitignore
├── .github/
│   └── workflows/
│       └── deploy.yml
└── README.md

---

## 🐳 Run locally

docker compose up -d --build

App available at:

http://localhost:8080

---

## 🔁 Load balancing test

Refresh the page multiple times:

You should see responses from different instances (app1 / app2).

---

## 🧪 Rollback test

1. Break the `/health` endpoint (return 500)
2. Push changes to GitHub
3. Open GitHub Actions

Expected result:

- Healthcheck fails
- Rollback is triggered
- Previous version is restored automatically

---

## 🔄 CI/CD Pipeline

Pipeline steps:

1. Build Docker image
2. Backup previous version
3. Deploy new version (docker-compose)
4. Run healthcheck (`/health`)
5. If failed → rollback to previous version

---

## 📦 Tech Stack

- Python (Flask)
- Docker / Docker Compose
- Nginx
- GitHub Actions

---

## 💡 Key Concept

This project implements a self-healing deployment system:

If a new deployment fails → system automatically rolls back to a stable version.

---

## 👨‍💻 Author


