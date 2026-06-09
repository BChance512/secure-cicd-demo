# Secure CI/CD Demo

## Overview

This project demonstrates a secure Continuous Integration and Continuous Deployment (CI/CD) pipeline using GitHub Actions for a simple Flask web application.

The goal of this repository is to showcase automated testing, security scanning, dependency validation, and container deployment as part of a modern DevSecOps workflow.

---

## Application

The application is a lightweight Flask API that exposes a single health endpoint.

### Endpoint

```
GET /health
```

### Response

```json
{
  "status": "healthy"
}
```

---

## CI/CD Pipeline

Every push or pull request to the **main** branch automatically executes the following GitHub Actions workflow:

1. Checkout the repository
2. Set up Python
3. Install project dependencies
4. Run unit tests using **pytest**
5. Perform static code security analysis using **Bandit**
6. Scan dependencies for known vulnerabilities using **pip-audit**
7. Build a Docker image
8. Publish the Docker image to GitHub Container Registry (GHCR)

---

## Security Approach

This repository demonstrates several security best practices:

- Static Application Security Testing (SAST) with Bandit
- Software Composition Analysis (SCA) using pip-audit
- Pinned dependency versions
- Automated security validation before deployment
- Automated container image publishing through GitHub Actions

During development, Bandit identified the use of `debug=True` in the Flask application. The issue was remediated by removing debug mode before deployment.

Additionally, pip-audit identified outdated dependencies which were upgraded to secure versions before the final pipeline execution.

---

## Running Locally

Create and activate a virtual environment:

```
python -m venv .venv
```

Windows:

```
.venv\Scripts\activate
```

Install dependencies:

```
pip install -r requirements.txt
```

Run the application:

```
python app/main.py
```

---

## Docker

Build the image:

```
docker build -t secure-cicd-demo .
```

Run the container:

```
docker run -p 5000:5000 secure-cicd-demo
```

---

## Technologies Used

- Python
- Flask
- GitHub Actions
- Docker
- Pytest
- Bandit
- pip-audit
- GitHub Container Registry (GHCR)

---

## Design Decisions

The application intentionally remains simple so the focus is on demonstrating a secure CI/CD pipeline rather than application complexity.

The pipeline validates application functionality, performs automated security analysis, checks dependencies for known vulnerabilities, and builds and publishes a container image, providing a repeatable and security-focused deployment process.
