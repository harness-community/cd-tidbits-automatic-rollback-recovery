# CI/CD Tidbit — Automatic Rollback with Harness

Learn how to configure Harness Continuous Delivery to automatically roll back a failed Kubernetes deployment. This tidbit demonstrates deploying a healthy application, intentionally introducing a deployment failure, and allowing Harness to automatically restore the previous successful release using the **Stage Rollback** failure strategy.

## What this skill accomplishes

Automatic Rollback is one of the most important deployment safety features in Harness.

Instead of manually reverting failed releases, Harness continuously monitors deployment health and, when a deployment fails to reach a healthy state, automatically executes rollback steps to restore the last successful release.

In this tidbit you will:

- Build a Docker image using Harness CI.
- Deploy the application to Kubernetes using a Rolling Deployment.
- Simulate a deployment failure.
- Observe Harness detecting the failure.
- Automatically roll back to the previous healthy release.

---

## What you will build

A complete CI/CD pipeline consisting of two stages.

### Build Stage

- Clone source code from GitHub.
- Build a Docker image.
- Push the image to Docker Hub.

### Deploy Stage

Deploy the application using a **Rolling Deployment**.

The deployment includes:

- Kubernetes Deployment
- Kubernetes Service
- Docker Hub Artifact
- Stage Rollback Failure Strategy
- Kubernetes Rolling Rollback Step

---

## Architecture

```text
Developer
    |
    v
GitHub Repository
    |
    v
Harness CI (Build & Push)
    |
    v
Docker Hub
    |
    v
Harness CD
    |
    v
Kubernetes Cluster
    |
    v
Healthy Deployment
    |
Deploy Broken Version
    |
Harness Detects Failure
    |
Automatic Rollback
    |
Previous Version Restored
```

---

## Prerequisites

- Harness Account
- Harness Project
- GitHub Connector
- Docker Hub Connector
- Kubernetes Connector
- Kubernetes Delegate
- Kubernetes Cluster (Kind, Minikube, Rancher Desktop, etc.)
- Docker Hub Account
- GitHub Repository

---

## Repository Structure

```text
harness-rollback/
├── app/
├── k8s/
├── .harness/
└── README.md
```

---

## Steps

1. Fork or clone the repository.
2. Configure GitHub, Docker Hub, and Kubernetes connectors.
3. Create the Harness Service.
4. Create the Environment and Infrastructure Definition.
5. Configure the Build and Deploy stages.
6. Deploy a healthy version.
7. Introduce a deployment failure.
8. Observe automatic rollback.
9. Verify the deployment using kubectl.

---

## Verification

```bash
kubectl get pods -n rollback-demo
kubectl get rs -n rollback-demo
kubectl rollout history deployment rollback-demo -n rollback-demo
```

---

## Expected Result

```text
Build Stage              ✅
Deploy Stage             ✅
Rolling Deployment       ❌
Execution (Rollback)     ✅
Application Restored     ✅
```

---

## Try It

- Invalid container command
- Invalid Docker image tag
- Startup failure
- Readiness probe failure
- Liveness probe failure

---

## Troubleshooting

- Check pod events and logs.
- Verify the Stage Rollback failure strategy.
- Confirm a previous successful deployment exists.
- Validate Docker Hub credentials and image tags.

---

## References

- Harness Continuous Delivery Documentation
- Harness Kubernetes Deployments
- Harness Failure Strategies
- Kubernetes Rolling Updates
- Kubernetes Rollback
