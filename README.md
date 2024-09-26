# Shared Actions Repository

## Overview

This repository contains reusable GitHub Actions workflows to streamline processes across multiple repositories (such as API and Frontend microservices). These workflows are used to build and push Docker images to Amazon ECR and deploy Kubernetes configurations to Amazon EKS.

## Workflows

### 1. **Build and Push Docker Image**
This workflow builds a Docker image and pushes it to an Amazon ECR repository.

- **Path**: `.github/workflows/build-and-push.yml`

#### Inputs:
- `ecr-repo-uri`: Amazon ECR repository URI.
- `dockerfile-path`: Path to the Dockerfile.
- `context-path`: Docker build context.

#### Usage Example:
```yaml
jobs:
  build:
    uses: shared-actions-repo/.github/workflows/build-and-push.yml@main
    with:
      ecr-repo-uri: ${{ secrets.ECR_REPO_URI }}
      dockerfile-path: ./Dockerfile
      context-path: .
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

```
### 2. Deploy to Kubernetes

This workflow deploys Kubernetes manifests (such as Deployment and Service files) to an Amazon EKS cluster.

Path:
```
.github/workflows/deploy-to-k8s.yml
```

Inputs:

- <mark>**deployment-file:**</mark> Path to the Kubernetes Deployment YAML file.
- <mark>**service-file:**</mark> Path to the Kubernetes Service YAML file.

Secrets:

- <mark>**AWS_ACCESS_KEY_ID:**</mark> AWS access key for authentication.
- <mark>**AWS_SECRET_ACCESS_KEY:**</mark> AWS secret access key for authentication.

Usage:

To use this workflow in other repositories, reference it like this in your workflow file:

```yaml
jobs:
  deploy:
    uses: shared-actions-repo/.github/workflows/deploy-to-k8s.yml@main
    with:
      deployment-file: ./k8s/deployment.yml
      service-file: ./k8s/service.yml
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```
### Pre-requisites
To use the workflows in this repository, you must have the following:

1. `Amazon ECR Repositories:` Make sure you have Amazon ECR repositories set up for each of your microservices.
   
2. `Amazon EKS Cluster:` Ensure you have a running EKS cluster to which the Kubernetes resources will be deployed.
   
3. `Secrets Configuration:` Configure the following secrets in each of your microservice repositories:
   
    - `AWS_ACCESS_KEY_ID:` The AWS Access Key ID for authentication.
    - `AWS_SECRET_ACCESS_KEY:` The AWS Secret Access Key for authentication.
    - `ECR_REPO_URI:` The Amazon ECR URI for the respective microservice.
      
## Contributions

Contributions are welcome! Please read our contributing guidelines to learn how you can propose bug fixes, improvements, or new features.

## License

This repository is licensed under the MIT License. See the LICENSE file for more details.

## Contact

For support or partnership inquiries, please contact <aarushi2.mehta@gmail.com>.
