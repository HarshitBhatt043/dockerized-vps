# Dockerized VPS GitOps Deployment

This branch is designed to manage Docker-based applications deployed on a VPS using GitOps workflows. It leverages version control, automation, and GitOps tooling (like [Komodo](https://komo.do/docs/intro)) to ensure a seamless and auditable deployment pipeline for your VPS-hosted services.

## Features

- Docker-based service configuration for a VPS environment.
- GitOps integration for automation and reproducibility.
- Easy branching and deployment for different service stacks.
- Orphan-branch model for clean, focused service configurations.

## Requirements

- Git
- Docker & Docker Compose installed on your VPS
- GitOps tool such as [Komodo](https://komo.do/docs/intro)
- Webhook or polling method to auto-deploy on commits

## Branch Purpose

This branch — `dockerized-vps` — contains configurations specifically meant for VPS-based services and deployments. It is isolated from other services via Git's orphan branch structure.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://{{git-source}}/homelab10400/dockerized-vps.git
cd dockerized-vps
```

### 2. Create a New Branch

To create a new branch for your HomeLab containerized application, use the following naming convention:  
**Branch Naming Convention:**

```yaml
ServiceName
```

**Example:**  
`Nginx`

Create the orphan branch:

```bash
git checkout --orphan Nginx
```

### 3. Modify and Commit

Make your desired changes to the Docker Compose files, `.env` configs, or additional setup scripts.

```bash
git add .
git commit -m "Configure VPS with web server and database"
```

### 4. Push the Branch

```bash
git push origin Nginx
```

### 5. Connect to GitOps Tool

Set up your GitOps tool (e.g., Komodo) to monitor this branch and trigger deployments on changes.

#### Steps to Set Up:

- Add a webhook in [Komodo](https://komo.do/docs/webhooks)
- Set it to track the `Nginx` branch
- Enable auto-sync or manual approval as preferred

### 6. Test the Flow

Make a small update and push it to test your end-to-end automation.

---

## Bash Helpers

Helpful aliases and functions to make working with Git branches easier:

```bash
# Pull all branches locally
alias pullall="for branch in \$(git branch | sed 's/^\* //'); do git checkout \$branch && git pull; done"

# Git auto-completion
source /usr/share/bash-completion/completions/git

# Create a new orphan branch quickly
orphan() {
  if [ -z "$1" ]; then
    echo "Usage: orphan <branch-name>"
    return 1
  fi
  git checkout --orphan "$1"
}
```

---

## Deployment Flow (Diagram)

```
Git Branch (e.g., Nginx)
        ↓
  Git Commit/Push
        ↓
  Komodo GitOps Sync
        ↓
  Dockerized Deployment to VPS
```

---
**THIS REPOSITORY IS ENCRYPTED. IF YOU'RE HERE, YOU'RE EITHER VERY BRAVE OR VERY LOST. EITHER WAY, GOOD LUCK!**
