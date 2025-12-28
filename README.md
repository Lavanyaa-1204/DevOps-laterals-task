# DevOps Lateral Task: Production-Ready Deployment

This project transforms a basic full-stack application into a containerized, automated system. It demonstrates a robust CI/CD lifecycle using industry-standard tools for high availability and security.



## 🏗 System Architecture
* **Frontend**: React.js SPA served via **Nginx**.
* **Backend**: High-performance Rust server using **Diesel ORM**.
* **Reverse Proxy**: Nginx acts as the entry point (Port 80) for routing and security.
* **CI/CD**: Automated via **Jenkins** for continuous build and registry delivery.

---

## 🛠 Level 1: Containerization & Reverse Proxy

### Best Practices Implemented:
* **Multi-Stage Builds**: Implemented in both `Backend` and `Frontend` Dockerfiles to reduce image size and keep source code out of production.
* **Base Images**: Used `node:18-alpine` and `rust:slim` for a lightweight, secure footprint.
* **Nginx Hardening**: Optimized for performance with Gzip compression and security headers.

---

## 🏗 Level 2: CI/CD Automation (Jenkins)

The pipeline is defined as **Pipeline-as-Code** via a `Jenkinsfile`.

### Pipeline Flow:
1. **Checkout**: Pulls source code from GitHub.
2. **Build**: Executes multi-stage builds for both Frontend and Backend images.
3. **Registry Push**: Authenticates with **Docker Hub** using Jenkins' **Global Credentials** to push versioned images.
4. **Security**: Secrets (Docker Hub tokens) are securely injected as masked environment variables.

---

## 🚀 Execution Instructions

### Prerequisites
* **Docker Desktop** (Windows/macOS) or **Docker Engine** (Linux).
* **Docker Compose** (V2 recommended).

### 🪟 For Windows Users (PowerShell/CMD)
1. **Clone the repository**:
   ``` powershell 
   git clone <your-repo-url>
   cd DevOps-laterals-task ```
2. Run the stack
``` docker-compose up --build ```
3. Access the app: Open http://localhost in your browser.

🐧 For Linux Users (Terminal)
1. Clone the repository:
    ``` git clone <your-repo-url>
        cd DevOps-laterals-task ```
2.  Set permissions (if necessary):
    ``` # Ensure your user is in the docker group
        sudo usermod -aG docker $USER ```
3.  Run the stack:
    ``` docker-compose up --build ```
4.  Access the app: Navigate to http://localhost.

📋 Best Practices Followed

Build Isolation: Use of .dockerignore to prevent local OS junk (like node_modules or target) from entering the build context.

Immutability: Every build produces a fresh, versioned container image.

Security: Zero hardcoding of sensitive data; all secrets managed via Jenkins Credentials.

📸 Proof of Completion
