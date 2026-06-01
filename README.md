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