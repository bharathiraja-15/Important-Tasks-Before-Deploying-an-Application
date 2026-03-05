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

If you want, I can also give you **10 REAL-TIME TASKS DevOps engineers actually do daily before deployment** (this will help you speak like a **Senior DevOps Engineer in interviews**).
