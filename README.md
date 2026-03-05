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

Great mindset 👍. If you practice the **right small tasks repeatedly**, you will not struggle during deployment. I’ll design a **real DevOps practice roadmap** that simulates **a 5–6 years experienced DevOps engineer workflow**. Each task is small but very important in real projects.

We will practice using:

* Git
* Docker
* Kubernetes
* Jenkins
* SonarQube
* Terraform

---

# DevOps Deployment Mastery Practice Tasks

## Phase 1 — Source Code Management (Day 1–2)

### Task 1 — Create Git Repository

Create a repository in **GitHub**

Practice commands:

```bash
git init
git add .
git commit -m "initial commit"
git push
```

Practice these scenarios:

1. Create branch
2. Merge branch
3. Resolve merge conflict

Commands to practice:

```bash
git branch dev
git checkout dev
git merge main
```

A **senior DevOps engineer must be strong in Git workflows**.

---

# Phase 2 — Build Application (Day 3)

### Task 2 — Build a Simple Application

Create simple app.

Example:

Python / Node / Java (any).

Run application locally.

Example:

```bash
python app.py
```

Check:

```
localhost:5000
```

Goal:
Always **verify application before containerizing**.

---

# Phase 3 — Containerization (Day 4)

### Task 3 — Create Docker Image

Practice with **Docker**

Create Dockerfile.

Run:

```bash
docker build -t bankapp:v1 .
```

Check images:

```bash
docker images
```

Run container:

```bash
docker run -p 5000:5000 bankapp:v1
```

Test application.

---

# Phase 4 — Docker Registry (Day 5)

### Task 4 — Push Image to Registry

Login to registry.

Example:

```bash
docker login
```

Push image to **Docker Hub**

```bash
docker push yourname/bankapp:v1
```

Practice:

1. tagging image
2. pushing image
3. pulling image

Commands:

```bash
docker tag bankapp:v1 username/bankapp:v1
docker pull username/bankapp:v1
```

---

# Phase 5 — Kubernetes Basics (Day 6)

### Task 5 — Deploy Container to Kubernetes

Use **Kubernetes**

Create deployment file.

Example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: bankapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: bankapp
  template:
    metadata:
      labels:
        app: bankapp
    spec:
      containers:
      - name: bankapp
        image: username/bankapp:v1
        ports:
        - containerPort: 5000
```

Apply:

```bash
kubectl apply -f deployment.yaml
```

Check pods:

```bash
kubectl get pods
```

---

# Phase 6 — Kubernetes Service (Day 7)

### Task 6 — Expose Application

Create service.

```bash
kubectl expose deployment bankapp --type=NodePort --port=80 --target-port=5000
```

Check service:

```bash
kubectl get svc
```

Open application.

---

# Phase 7 — CI/CD Pipeline (Day 8)

### Task 7 — Create Pipeline

Use **Jenkins**

Pipeline stages:

```
1 Clone Code
2 Build Application
3 SonarQube Scan
4 Docker Build
5 Docker Push
6 Deploy Kubernetes
```

Example Jenkins pipeline stages:

```
Stage 1: Git Clone
Stage 2: Build
Stage 3: Code Scan
Stage 4: Docker Build
Stage 5: Docker Push
Stage 6: Kubernetes Deploy
```

---

# Phase 8 — Code Quality (Day 9)

### Task 8 — Setup Code Scan

Install **SonarQube**

Run:

```
sonar-scanner
```

Check:

* vulnerabilities
* bugs
* code smells

---

# Phase 9 — Dev / Stage / Prod Deployment (Day 10)

### Task 9 — Environment Based Deployment

Create 3 Kubernetes namespaces.

```bash
kubectl create namespace dev
kubectl create namespace stage
kubectl create namespace prod
```

Deploy applications separately.

DEV

```bash
kubectl apply -f deployment-dev.yaml -n dev
```

STAGE

```bash
kubectl apply -f deployment-stage.yaml -n stage
```

PROD

```bash
kubectl apply -f deployment-prod.yaml -n prod
```

---

# Phase 10 — Rollback Practice (Day 11)

### Task 10 — Rollback Deployment

Very important real-time skill.

Update image.

```bash
kubectl set image deployment/bankapp bankapp=bankapp:v2
```

Rollback.

```bash
kubectl rollout undo deployment bankapp
```

---

# Phase 11 — Troubleshooting (Day 12)

### Task 11 — Debug Failed Deployment

Check pods.

```bash
kubectl get pods
```

Check logs.

```bash
kubectl logs pod-name
```

Describe pod.

```bash
kubectl describe pod pod-name
```

---

# Final Skill You Will Gain

After these tasks you will confidently handle:

✔ Application deployment
✔ CI/CD pipeline
✔ Docker containerization
✔ Kubernetes deployment
✔ Dev / Stage / Prod environments
✔ Rollbacks
✔ Debugging failures

This is exactly what **5–6 years DevOps engineers do daily**.

---

💡 Since you also mentioned you want to **master Kubernetes deeply**, the next step I can give you is:

**“20 REAL Production Problems DevOps Engineers Face While Deploying Applications (and how to fix them)”**

This will **massively increase your interview confidence and troubleshooting skills.**
Great question. Practicing **production problems + how to explain them** will really help you speak like a **5–6 years DevOps engineer in interviews**. I’ll organize the **40 real production issues** into categories and show:

* Problem
* How to detect it
* Step-by-step fix
* How to explain it in an interview

Tools commonly involved: Docker, Kubernetes, Jenkins, Git, SonarQube, Terraform.

---

# 40 Real Production Problems DevOps Engineers Face

# 1–8 Docker Problems

## 1. Docker Build Fails

**Problem**
Docker image fails during build.

**Check**

```bash
docker build .
```

**Common reason**

* wrong dependency
* syntax error in Dockerfile

**Fix**

```dockerfile
RUN apt update && apt install -y curl
```

**Interview explanation**

> During Docker image build the pipeline failed due to dependency issues in the Dockerfile. I reviewed the build logs, corrected the dependency installation command, rebuilt the image and validated the container locally before pushing to the registry.

---

## 2. Container Exits Immediately

Check logs:

```bash
docker logs containerID
```

Common reasons:

* application crash
* wrong command in Dockerfile

Fix:

```dockerfile
CMD ["python","app.py"]
```

**Interview explanation**

> The container was exiting immediately because the entrypoint command was incorrect. After checking logs I corrected the CMD instruction and rebuilt the image.

---

## 3. Port Not Accessible

Check container port mapping.

```bash
docker ps
```

Fix:

```bash
docker run -p 8080:80 image
```

Explanation:

> The issue occurred due to incorrect port mapping between host and container.

---

## 4. Docker Image Too Large

Check image size:

```bash
docker images
```

Fix:

Use **multi-stage builds**.

Explanation:

> I optimized the Docker image by implementing multi-stage builds which reduced image size and improved deployment speed.

---

## 5. Wrong Image Tag

Problem:
Pipeline deployed incorrect version.

Fix:

```bash
docker tag bankapp:v1 bankapp:latest
```

Explanation:

> The deployment was referencing an incorrect image tag, so I updated the tag and redeployed.

---

## 6. Docker Registry Authentication Failure

Check login:

```bash
docker login
```

Fix credentials.

Explanation:

> The pipeline failed while pushing image due to registry authentication failure.

---

## 7. Docker Image Vulnerabilities

Scan image with:

```bash
trivy image bankapp:v1
```

Fix by updating base image.

Explanation:

> Security scanning identified vulnerabilities, so I updated the base image and rebuilt the container.

---

## 8. Container Memory Issue

Check usage:

```bash
docker stats
```

Fix memory limits.

---

# 9–20 Kubernetes Problems

## 9. Pod CrashLoopBackOff

Check:

```bash
kubectl get pods
```

Check logs:

```bash
kubectl logs podname
```

Fix application error.

Explanation:

> Pod entered CrashLoopBackOff due to application startup failure.

---

## 10. ImagePullBackOff

Reason:
image not found.

Fix:

```bash
kubectl describe pod
```

Update image name.

---

## 11. Service Not Accessible

Check service:

```bash
kubectl get svc
```

Fix:

Check selector labels.

---

## 12. ConfigMap Not Loaded

Check:

```bash
kubectl describe pod
```

Fix ConfigMap reference.

---

## 13. Secret Not Mounted

Fix secret configuration.

```bash
kubectl create secret
```

---

## 14. Deployment Not Updating

Check rollout.

```bash
kubectl rollout status deployment app
```

Fix by updating image.

---

## 15. High CPU Usage

Check metrics.

```bash
kubectl top pods
```

Fix resource limits.

---

## 16. Node Not Ready

Check:

```bash
kubectl get nodes
```

Fix node issue.

---

## 17. Pods Not Scheduling

Check:

```bash
kubectl describe pod
```

Reason:
insufficient resources.

---

## 18. Wrong Namespace Deployment

Check:

```bash
kubectl get pods -n dev
```

---

## 19. Rolling Update Failure

Fix rollback.

```bash
kubectl rollout undo deployment app
```

---

## 20. Liveness Probe Failure

Fix probe configuration.

---

# 21–30 CI/CD Problems

## 21. Jenkins Pipeline Fails

Check build logs.

Explanation:

> I reviewed Jenkins console logs and identified the failed stage.

---

## 22. Git Clone Failure

Check SSH keys.

---

## 23. Pipeline Permission Issue

Fix Jenkins credentials.

---

## 24. SonarQube Quality Gate Failed

Fix code quality issues.

---

## 25. Pipeline Timeout

Increase timeout.

---

## 26. Build Artifact Missing

Check artifact path.

---

## 27. Wrong Branch Trigger

Fix webhook configuration.

---

## 28. Pipeline Stuck

Restart Jenkins agent.

---

## 29. Deployment Script Failure

Fix script syntax.

---

## 30. Environment Variable Missing

Add env variables.

---

# 31–40 Infrastructure Problems

## 31. Terraform Apply Fails

Check plan.

```bash
terraform plan
```

---

## 32. AWS Permission Error

Fix IAM role.

---

## 33. Load Balancer Not Routing

Check target group.

---

## 34. DNS Not Resolving

Fix DNS record.

---

## 35. SSL Certificate Expired

Renew certificate.

---

## 36. Storage Not Mounted

Check volume configuration.

---

## 37. Database Connection Failed

Check secrets.

---

## 38. Network Policy Blocking Traffic

Update policy.

---

## 39. Monitoring Not Working

Check **Prometheus**.

---

## 40. Logs Not Showing

Check **ELK Stack** configuration.

---

# How to Explain Production Issues in Interviews

Use this structure:

### 1. Problem

What happened.

### 2. Investigation

How you debugged.

### 3. Solution

How you fixed it.

### 4. Prevention

How you avoided it next time.

Example:

> During deployment the application pod entered CrashLoopBackOff state. I investigated using kubectl logs and found the application configuration was incorrect. After updating the environment variable configuration and redeploying the pod the application started successfully. Later we added validation checks in the CI pipeline to prevent similar issues.

---

If you want, I can also show you:

**“25 Most Dangerous Kubernetes Production Failures (with exact kubectl commands DevOps engineers use to fix them)”**

This will make your **Kubernetes troubleshooting skills extremely strong for interviews.**
These are **25 dangerous Kubernetes production failures** that DevOps engineers often face. I’ll show you for each:

* What the problem is
* How to detect it
* Exact **`kubectl` commands** to troubleshoot
* How to fix it
* How to explain it clearly in interviews

Tool involved: Kubernetes.

---

# 25 Dangerous Kubernetes Production Failures

---

# 1. Pod in CrashLoopBackOff

**Problem**
Application container keeps crashing and restarting.

**Detect**

```bash
kubectl get pods
```

Output:

```
CrashLoopBackOff
```

**Debug**

```bash
kubectl logs pod-name
kubectl describe pod pod-name
```

**Fix**

* Fix application configuration
* Fix environment variables
* Rebuild image

**Interview explanation**

> The pod entered CrashLoopBackOff due to an application startup error. I checked pod logs and identified the configuration issue, corrected the environment variable, and redeployed the application.

---

# 2. ImagePullBackOff

**Problem**
Kubernetes cannot pull image.

**Check**

```bash
kubectl describe pod pod-name
```

Possible causes

* wrong image name
* registry authentication issue

**Fix**

```bash
kubectl edit deployment app
```

Update correct image.

---

# 3. Pods Not Scheduling

**Problem**
Pods stuck in `Pending`.

**Check**

```bash
kubectl describe pod pod-name
```

Common reason:

```
Insufficient CPU
```

**Fix**

```bash
kubectl scale deployment app --replicas=2
```

Or increase node capacity.

---

# 4. Node Not Ready

**Check**

```bash
kubectl get nodes
```

If node shows:

```
NotReady
```

**Debug**

```bash
kubectl describe node node-name
```

**Fix**
Restart kubelet or node.

---

# 5. Service Not Accessible

**Check services**

```bash
kubectl get svc
```

**Check endpoints**

```bash
kubectl get endpoints
```

If empty → label mismatch.

**Fix**

```bash
kubectl edit service service-name
```

Correct selector labels.

---

# 6. Deployment Failed

**Check**

```bash
kubectl rollout status deployment app
```

**Fix**

```bash
kubectl rollout restart deployment app
```

---

# 7. Rolling Update Failure

Check rollout history.

```bash
kubectl rollout history deployment app
```

Rollback.

```bash
kubectl rollout undo deployment app
```

---

# 8. High CPU Usage

Check usage.

```bash
kubectl top pods
```

Fix by adding resource limits.

Example:

```yaml
resources:
  limits:
    cpu: "500m"
```

---

# 9. High Memory Usage

Check memory.

```bash
kubectl top pods
```

Fix:

increase memory limits.

---

# 10. Pod OOMKilled

Check pod status.

```bash
kubectl describe pod pod-name
```

If reason:

```
OOMKilled
```

Fix by increasing memory.

---

# 11. ConfigMap Not Applied

Check configmap.

```bash
kubectl get configmap
```

Fix:

```bash
kubectl apply -f configmap.yaml
```

Restart deployment.

---

# 12. Secret Missing

Check secrets.

```bash
kubectl get secrets
```

Create secret.

```bash
kubectl create secret generic db-secret --from-literal=password=123
```

---

# 13. Container Not Starting

Check logs.

```bash
kubectl logs pod-name
```

Fix container command.

---

# 14. Wrong Namespace Deployment

Check namespaces.

```bash
kubectl get ns
```

Deploy correctly.

```bash
kubectl apply -f deployment.yaml -n dev
```

---

# 15. DNS Resolution Failure

Test inside pod.

```bash
kubectl exec -it pod-name -- nslookup service-name
```

Fix DNS configuration.

---

# 16. Persistent Volume Not Mounting

Check PVC.

```bash
kubectl get pvc
```

Describe.

```bash
kubectl describe pvc pvc-name
```

Fix storage class.

---

# 17. Pod Network Issue

Test connectivity.

```bash
kubectl exec -it pod-name -- ping service
```

Fix network policy.

---

# 18. Load Balancer Not Working

Check service type.

```bash
kubectl get svc
```

If external IP pending → cloud issue.

---

# 19. Job Not Completing

Check jobs.

```bash
kubectl get jobs
```

Logs:

```bash
kubectl logs job/job-name
```

---

# 20. CronJob Not Running

Check cronjobs.

```bash
kubectl get cronjobs
```

Check schedule.

---

# 21. Deployment Stuck Updating

Check rollout.

```bash
kubectl rollout status deployment app
```

Rollback if necessary.

---

# 22. Pods Restarting Frequently

Check restart count.

```bash
kubectl get pods
```

Investigate logs.

---

# 23. Node Disk Full

Check node events.

```bash
kubectl describe node node-name
```

Clean unused images.

---

# 24. API Server Not Responding

Check cluster status.

```bash
kubectl cluster-info
```

Restart control plane if needed.

---

# 25. Too Many Pods on Node

Check distribution.

```bash
kubectl get pods -o wide
```

Fix with autoscaling.

---

# Golden Troubleshooting Commands (Memorize)

These are used daily by DevOps engineers.

```bash
kubectl get pods
kubectl describe pod pod-name
kubectl logs pod-name
kubectl get svc
kubectl get nodes
kubectl get events
kubectl rollout status deployment
kubectl rollout undo deployment
kubectl exec -it pod-name -- bash
kubectl top pods
```

---

# Best Interview Explanation Template

When interviewer asks about a failure:

Explain like this:

> During a production deployment the application pod entered CrashLoopBackOff state. I first checked the pod status using `kubectl get pods`, then analyzed the logs using `kubectl logs`. The logs indicated a configuration issue with environment variables. After correcting the configuration and redeploying the application the pod started successfully.

Structure:

1️⃣ Identify issue
2️⃣ Debug using kubectl
3️⃣ Fix configuration
4️⃣ Redeploy

---

If you want, I can also teach you **“The 15-step Kubernetes troubleshooting workflow used by senior DevOps engineers when production deployment fails.”**
This is the **exact mental process experts follow in real incidents.**

