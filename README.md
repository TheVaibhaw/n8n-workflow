# n8n Docker Setup Guide (Ubuntu & Windows)

## Overview

This project runs n8n using Docker and Docker Compose.

Default URL:

```text
http://localhost:5678
```

---

# Project Structure

```text
n8n/
├── docker-compose.yml
├── .gitignore
└── README.md
```

---

# Option 1: Ubuntu Setup

## Step 1: Install Docker

Update packages:

```bash
sudo apt update
```

Install Docker:

```bash
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Verify:

```bash
docker --version
```

Example output:

```text
Docker version 29.x.x
```

---

## Step 2: Install Docker Compose

```bash
sudo apt install docker-compose -y
```

Verify:

```bash
docker-compose --version
```

Example:

```text
docker-compose version 1.29.2
```

---

## Step 3: Clone Repository

```bash
git clone <YOUR_GITHUB_REPO>
cd n8n
```

---

## Step 4: Start n8n

```bash
docker-compose up -d
```

Check status:

```bash
docker ps
```

---

## Step 5: Open n8n

Open browser:

```text
http://localhost:5678
```

Create Owner Account.

---

## Useful Ubuntu Commands

### Stop n8n

```bash
docker-compose down
```

### Restart n8n

```bash
docker-compose restart
```

### View Logs

```bash
docker logs -f n8n
```

### Check Running Containers

```bash
docker ps
```

### Check All Containers

```bash
docker ps -a
```

### Update n8n

```bash
docker-compose down
docker pull docker.n8n.io/n8nio/n8n:latest
docker-compose up -d
```

---

# Option 2: Windows Setup

## Step 1: Install Docker Desktop

Download and install Docker Desktop.

Requirements:

- Windows 10/11
- WSL2 enabled

Verify installation:

Open PowerShell:

```powershell
docker --version
```

Example:

```text
Docker version 29.x.x
```

---

## Step 2: Clone Repository

Open PowerShell:

```powershell
git clone <YOUR_GITHUB_REPO>
cd n8n
```

---

## Step 3: Start n8n

```powershell
docker compose up -d
```

Check status:

```powershell
docker ps
```

---

## Step 4: Open n8n

Open browser:

```text
http://localhost:5678
```

Create Owner Account.

---

## Useful Windows Commands

### Stop n8n

```powershell
docker compose down
```

### Restart n8n

```powershell
docker compose restart
```

### View Logs

```powershell
docker logs -f n8n
```

### Check Running Containers

```powershell
docker ps
```

### Check All Containers

```powershell
docker ps -a
```

### Update n8n

```powershell
docker compose down
docker pull docker.n8n.io/n8nio/n8n:latest
docker compose up -d
```

---

# Docker Compose File

Create file:

```text
docker-compose.yml
```

Content:

```yaml
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    container_name: n8n

    restart: unless-stopped

    ports:
      - "5678:5678"

    environment:
      - TZ=Asia/Kolkata

    volumes:
      - n8n_data:/home/node/.n8n

volumes:
  n8n_data:
```

---

# Git Ignore

Create:

```text
.gitignore
```

Content:

```gitignore
# Environment
.env
.env.local

# Logs
*.log

# Docker Volume Data
n8n_data/

# IDE
.vscode/
.idea/

# OS Files
.DS_Store
Thumbs.db

# Backups
*.tar.gz

# Node
node_modules/
```

---

# GitHub Setup

Initialize repository:

```bash
git init
```

Add files:

```bash
git add .
```

Commit:

```bash
git commit -m "Initial n8n Docker setup"
```

Create main branch:

```bash
git branch -M main
```

Connect GitHub repository:

```bash
git remote add origin <REPOSITORY_URL>
```

Push:

```bash
git push -u origin main
```

---

# Files To Commit

```text
README.md
docker-compose.yml
.gitignore
```

---

# Files NOT To Commit

```text
n8n_data/
.env
*.tar.gz
Docker volumes
Local backups
```

---

# Backup Existing Workflows

List Docker volumes:

```bash
docker volume ls
```

Example:

```text
n8n_n8n_data
```

Backup:

```bash
docker run --rm \
-v n8n_n8n_data:/source \
-v $(pwd):/backup \
alpine \
tar czf /backup/n8n-backup.tar.gz -C /source .
```

---

# Restore Backup

```bash
docker run --rm \
-v n8n_n8n_data:/target \
-v $(pwd):/backup \
alpine \
sh -c "cd /target && tar xzf /backup/n8n-backup.tar.gz"
```

---

# Production Deployment

DNS Record:

```text
api.skylinescenes.com → AWS_PUBLIC_IP
```

Nginx Reverse Proxy:

```nginx
server {
    server_name api.skylinescenes.com;

    location / {
        proxy_pass http://localhost:5678;
    }
}
```

Enable SSL:

```bash
sudo certbot --nginx -d api.skylinescenes.com
```

Final URL:

```text
https://api.skylinescenes.com
```
