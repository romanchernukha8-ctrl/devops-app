# DevOps App with Load Balancing & Auto Rollback

## Description

This project demonstrates a production-like deployment pipeline using Docker, Nginx, and GitHub Actions.

It includes automated deployment, health checks, and a rollback mechanism that restores the last stable version if something goes wrong.

---

## Live Demo

http://3.85.224.36

---

## Architecture

Client → Nginx → App1 / App2

* Nginx acts as a load balancer
* Two application instances handle traffic
* Requests are distributed between containers

---

## Features

* Multi-container setup with Docker Compose
* Load balancing via Nginx
* Health check endpoint (`/health`)
* CI/CD pipeline using GitHub Actions
* Automatic rollback on failed deployment
* Remote deployment to AWS via SSH

---

## Health Endpoint

GET /health → 200 OK

Used in CI/CD pipeline to verify application health after deployment.

---

## Project Structure

devops-app/
├── app.py
├── Dockerfile
├── docker-compose.yml
├── nginx.conf
├── requirements.txt
├── .dockerignore
├── .gitignore
├── .github/workflows/deploy.yml
└── README.md

---

## Run Locally

docker compose up -d --build

App will be available at:

http://localhost:8080

---

## Load Balancing Test

Refresh the page multiple times:

Expected result:

Hello from app1
Hello from app2

---

## CI/CD Pipeline

Pipeline flow:

1. Install dependencies
2. Run application test (localhost:5000/health)
3. Connect to AWS server via SSH
4. Pull latest code
5. Build Docker image
6. Backup current version
7. Deploy new version (docker-compose)
8. Run healthcheck inside container
9. If failed → rollback to previous version

---

## Rollback Mechanism

Before deployment:

docker tag devops-app:latest devops-app:backup

If healthcheck fails:

docker tag devops-app:backup devops-app:latest
docker compose up -d --force-recreate

---

## Failure Scenario (Test)

To test rollback:

1. Modify `/health` to return 500
2. Push changes
3. Open GitHub Actions

Expected:

* Deployment starts
* Healthcheck fails
* Rollback triggered
* Previous version restored

---

## Tech Stack

* Python (Flask)
* Docker / Docker Compose
* Nginx
* GitHub Actions
* AWS EC2

---

## Key Concept

This project implements a self-healing deployment system:

If a new release is broken → system automatically restores the last working version.

---

## Example Response

Hello from app1
Hello from app2
