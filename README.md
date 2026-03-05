# Important-Tasks-Before-Deploying-an-Application
Important Tasks Before Deploying an Application
Before **deploying an application in a real DevOps environment**, there are several **important tasks you must complete**. If you do these properly, deployment becomes smooth and production issues will be very low.

I will give you a **real-time DevOps checklist** that companies usually follow.

---

# Important Tasks Before Deploying an Application

## 1. Code Review (Very Important)

Before deployment, the **source code must be reviewed**.

**What to check**

* Code quality
* Security issues
* Coding standards
* Unused code
* Bugs

**Tools used**

* GitHub Pull Request review
* GitLab Merge Request
* Bitbucket Code review

**Real-time workflow**

Developer → Create Pull Request → Team review → Approve → Merge to main branch

---

# 2. Static Code Analysis

Scan the code for **bugs, vulnerabilities, and code smells**.

**Most used tool**

* SonarQube

**What it checks**

* Security vulnerabilities
* Duplicate code
* Maintainability
* Reliability issues

If **Quality Gate fails → deployment should stop**.

---

# 3. Unit Testing

Developers write **unit test cases**.

Example tools:

* JUnit (Java)
* PyTest (Python)
* Jest (NodeJS)

**Important metrics**

* Code coverage should be **> 70–80%**

---

# 4. Build the Application

Convert source code into a **build artifact**.

Examples

* `.jar`
* `.war`
* `.zip`
* `.binary`

**Tools used**

* Maven
* Gradle
* npm

---

# 5. Containerization

Create a **Docker image** of the application.

Tool used:

* Docker

Example steps

```
Dockerfile
↓
docker build
↓
docker image created
```

---

# 6. Image Security Scan

Before pushing image to registry, scan it.

Tools used

* Trivy
* Clair
* Anchore

Checks

* Vulnerabilities
* CVE issues
* Outdated libraries

---

# 7. Push Image to Registry

Store Docker images in registry.

Examples

* Docker Hub
* Amazon Elastic Container Registry
* JFrog Artifactory

---

# 8. Infrastructure Readiness Check

Before deployment ensure infrastructure is ready.

Check

* Kubernetes cluster running
* Nodes healthy
* Storage available
* Network working

Platforms

* Kubernetes
* OpenShift
* Amazon EKS

---

# 9. Secrets & Config Management

Application may need:

* Database password
* API keys
* Environment variables

Store securely using:

* Kubernetes Secrets
* HashiCorp Vault

---

# 10. Deployment Strategy

Choose safe deployment method.

Common strategies

1. **Rolling Deployment**
2. **Blue-Green Deployment**
3. **Canary Deployment**

Mostly used in

* Kubernetes

---

# 11. Health Checks

Configure health checks.

Types

* **Liveness Probe** → container alive?
* **Readiness Probe** → ready to serve traffic?

---

# 12. Monitoring Setup

Monitor application performance.

Tools

* Prometheus
* Grafana
* Datadog

---

# 13. Logging Setup

Centralized logging.

Tools

* ELK Stack
* Splunk

---

# 14. Backup & Rollback Plan

If deployment fails you must rollback.

Example

```
kubectl rollout undo deployment
```

---

# Real Time CI/CD Pipeline Flow

```
Developer push code → GitHub
        ↓
CI Pipeline triggered
        ↓
Code Review
        ↓
SonarQube Scan
        ↓
Build Application
        ↓
Docker Build
        ↓
Security Scan
        ↓
Push Image to Registry
        ↓
Deploy to Kubernetes
        ↓
Monitoring & Logging
```

---

# Very Important Interview Answer (How You Should Explain)

If interviewer asks:

**"What steps do you follow before deploying an application?"**

You can answer like this:

> Before deployment we ensure code quality through pull request review and static code analysis using SonarQube.
> Then we run unit tests and build the artifact using Maven or Gradle.
> After that we containerize the application using Docker and scan the image for vulnerabilities using Trivy.
> The image is pushed to a container registry like ECR or DockerHub.
> Before deployment we verify infrastructure readiness in Kubernetes, configure secrets and environment variables, and ensure monitoring and logging are configured.
> Finally we deploy using strategies like rolling or blue-green deployment.

---
Good. I will give you **one real-time DevOps task** that many companies actually do before deployment.
You can practice it on your laptop and later explain it confidently in interviews.

We will simulate a **real DevOps pipeline task**.

---

# Real-Time DevOps Practice Task (Step by Step)

## Task Goal

You will:

1. Clone application code
2. Build application
3. Create Docker image
4. Scan image for vulnerabilities
5. Push image to registry
6. Deploy to Kubernetes

Tools you will use:

* Git
* Docker
* Trivy
* Kubernetes
* Docker Hub

---

# Step 1 — Clone Application Code

First get application code from Git repository.

Example:

```bash
git clone https://github.com/dockersamples/node-bulletin-board
cd node-bulletin-board
```

Check files:

```bash
ls
```

You should see

```
Dockerfile
package.json
server.js
```

---

# Step 2 — Build Application (Optional for Node)

Install dependencies.

```bash
npm install
```

Run locally to verify:

```bash
node server.js
```

Open browser

```
http://localhost:8080
```

If it works → application ready.

Stop it

```
CTRL + C
```

---

# Step 3 — Build Docker Image

Now create container image using **Dockerfile**.

```bash
docker build -t yourdockerhubname/nodeapp:v1 .
```

Example

```bash
docker build -t bharathiraja3234/nodeapp:v1 .
```

Check image:

```bash
docker images
```

Expected output

```
bharathiraja3234/nodeapp   v1
```

---

# Step 4 — Scan Image for Vulnerabilities

Before deployment companies scan image for security issues.

Install scanner:

```bash
sudo apt install trivy
```

Run scan:

```bash
trivy image bharathiraja3234/nodeapp:v1
```

This shows:

* HIGH vulnerabilities
* CRITICAL vulnerabilities

Fix if necessary.

---

# Step 5 — Push Image to Docker Registry

Login first.

```bash
docker login
```

Push image.

```bash
docker push bharathiraja3234/nodeapp:v1
```

Now image stored in:

* Docker Hub

---

# Step 6 — Create Kubernetes Deployment File

Create file

```
deployment.yaml
```

Example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: node-app
  template:
    metadata:
      labels:
        app: node-app
    spec:
      containers:
      - name: node-container
        image: bharathiraja3234/nodeapp:v1
        ports:
        - containerPort: 8080
```

---

# Step 7 — Deploy Application to Kubernetes

Apply deployment.

```bash
kubectl apply -f deployment.yaml
```

Check pods.

```bash
kubectl get pods
```

Check deployment.

```bash
kubectl get deployment
```

---

# Step 8 — Expose Application

Create service.

```bash
kubectl expose deployment node-app --type=NodePort --port=80 --target-port=8080
```

Check service.

```bash
kubectl get svc
```

Open application.

```
http://node-ip:nodeport
```

---

# Step 9 — Verify Deployment

Check logs.

```bash
kubectl logs pod-name
```

Check rollout.

```bash
kubectl rollout status deployment node-app
```

---

# Real DevOps Workflow You Just Practiced

```
Developer Push Code
        ↓
Clone Repository
        ↓
Build Application
        ↓
Docker Build
        ↓
Security Scan (Trivy)
        ↓
Push Image (DockerHub)
        ↓
Kubernetes Deployment
        ↓
Expose Service
        ↓
Application Running
```

---

# Real Interview Explanation (Very Important)

If interviewer asks:

**"Explain your deployment process."**

Answer like this:

> First I clone the application code from Git repository.
> Then I build the application and verify it locally.
> After that I containerize the application using Docker.
> Before pushing the image I scan it using Trivy to check for vulnerabilities.
> Once the image is secure, I push it to DockerHub.
> Then I create Kubernetes deployment manifests and deploy the application to the cluster using kubectl.
> Finally I expose the service and verify pods, logs, and rollout status.

---

# Your Task Now (Practice)

Do these **5 commands now**:

```
1. git clone node application
2. docker build image
3. trivy scan
4. docker push
5. kubectl deployment
```

---

If you want, I can also give you **one COMPLETE REAL COMPANY TASK (CI/CD pipeline project)** using:

* Jenkins
* SonarQube
* Docker
* Kubernetes

This is the **exact project many DevOps engineers show in interviews**.

If you want, I can also give you **10 REAL-TIME TASKS DevOps engineers actually do daily before deployment** (this will help you speak like a **Senior DevOps Engineer in interviews**).
Good question. I will give you a **REAL COMPANY STYLE TASK** where you practice **Dev → Stage → Prod deployment like a real DevOps engineer**.

This task will help you understand how **CI/CD pipelines work in companies** using:

* GitHub
* Jenkins
* SonarQube
* Docker
* Kubernetes

I will explain **exact tasks you must do step-by-step**.

---

# Real DevOps Practice Project

## Dev → Stage → Production Pipeline

You will build a **complete CI/CD pipeline**.

Pipeline flow:

```
Developer → GitHub
        ↓
Jenkins Pipeline
        ↓
SonarQube Code Scan
        ↓
Docker Build
        ↓
Push Docker Image
        ↓
Deploy to DEV
        ↓
Testing
        ↓
Deploy to STAGE
        ↓
Approval
        ↓
Deploy to PROD
```

---

# Step 1 — Create a Git Repository

Create repository in **GitHub**

Example repo name

```
bankapp-devops-project
```

Add these files:

```
Dockerfile
app.py
requirements.txt
Jenkinsfile
deployment-dev.yaml
deployment-stage.yaml
deployment-prod.yaml
```

---

# Step 2 — Sample Application (Simple Python App)

Create `app.py`

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Bank Application Running"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

---

# Step 3 — Requirements File

Create `requirements.txt`

```
flask
```

---

# Step 4 — Create Dockerfile

```
FROM python:3.9

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python","app.py"]
```

---

# Step 5 — Create Kubernetes DEV Deployment

`deployment-dev.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: bankapp-dev
spec:
  replicas: 1
  selector:
    matchLabels:
      app: bankapp-dev
  template:
    metadata:
      labels:
        app: bankapp-dev
    spec:
      containers:
      - name: bankapp
        image: yourdockerhub/bankapp:dev
        ports:
        - containerPort: 5000
```

---

# Step 6 — Create STAGE Deployment

`deployment-stage.yaml`

```
replicas: 2
image: yourdockerhub/bankapp:stage
```

---

# Step 7 — Create PROD Deployment

`deployment-prod.yaml`

```
replicas: 3
image: yourdockerhub/bankapp:prod
```

Production always has **more replicas**.

---

# Step 8 — Setup SonarQube

Install **SonarQube**

Run container:

```bash
docker run -d -p 9000:9000 sonarqube
```

Open

```
http://localhost:9000
```

Create project and get **token**.

---

# Step 9 — Setup Jenkins

Install **Jenkins**

Install plugins:

* Docker pipeline
* SonarQube scanner
* Kubernetes CLI
* Git

---

# Step 10 — Create Jenkins Pipeline

Create `Jenkinsfile`

Example pipeline:

```groovy
pipeline {
 agent any

 stages {

 stage('Clone Code') {
 steps {
 git 'https://github.com/yourrepo/bankapp-devops-project'
 }
 }

 stage('SonarQube Scan') {
 steps {
 sh 'sonar-scanner'
 }
 }

 stage('Build Docker Image') {
 steps {
 sh 'docker build -t yourdockerhub/bankapp:dev .'
 }
 }

 stage('Push Image') {
 steps {
 sh 'docker push yourdockerhub/bankapp:dev'
 }
 }

 stage('Deploy to Dev') {
 steps {
 sh 'kubectl apply -f deployment-dev.yaml'
 }
 }

 stage('Deploy to Stage') {
 steps {
 input 'Approve for Stage?'
 sh 'kubectl apply -f deployment-stage.yaml'
 }
 }

 stage('Deploy to Production') {
 steps {
 input 'Approve for Production?'
 sh 'kubectl apply -f deployment-prod.yaml'
 }
 }

 }
}
```

---

# Step 11 — Run Pipeline

When developer pushes code to **GitHub**:

Pipeline will:

1. Clone code
2. Scan code
3. Build Docker image
4. Push image
5. Deploy to DEV
6. Deploy to STAGE
7. Deploy to PROD

---

# Real DevOps Environment Structure

Cluster layout:

```
Kubernetes Cluster

Namespace: dev
Namespace: stage
Namespace: prod
```

Example:

```
kubectl create namespace dev
kubectl create namespace stage
kubectl create namespace prod
```

---

# Real Company Deployment Flow

```
Developer Push Code
        ↓
CI Pipeline Trigger
        ↓
Code Scan (SonarQube)
        ↓
Docker Build
        ↓
Push Docker Image
        ↓
Deploy DEV
        ↓
QA Testing
        ↓
Deploy STAGE
        ↓
Manager Approval
        ↓
Deploy PROD
```

---

# Your Practice Tasks (Do These)

Task 1
Create **GitHub repository**

Task 2
Create **Python application**

Task 3
Create **Dockerfile**

Task 4
Push code to GitHub

Task 5
Install **Jenkins**

Task 6
Install **SonarQube**

Task 7
Create **Jenkins pipeline**

Task 8
Create **Kubernetes deployments**

Task 9
Run pipeline

---

# When you finish this project you can confidently say in interview

> I implemented a CI/CD pipeline using GitHub, Jenkins, SonarQube, Docker and Kubernetes where the pipeline automatically builds the application, scans code, builds Docker images, pushes them to registry and deploys them to Dev, Stage and Production environments.

---

✅ If you want, I can also give you a **SUPER REALISTIC DevOps project used in interviews in 2025–2026**:

**Terraform + EKS + Jenkins + ArgoCD + Kubernetes + Monitoring**

This is the **exact project that makes interviewers think you are a Senior DevOps engineer.**
