This repository contains Docker as Containerization platform to deploy the code & CI/CD tool as Jenkins to automate the application

---

## 🛠 Tech Stack
- Jenkins (CI/CD Tool)
- Docker (Containerization Platform Tool)
- AWS (or your cloud provider)
- Git & GitHub

---

## 🚀 How to Use
### 1️⃣ Clone from GitHub Repo
```
💡  git 'https://github.com/sindhumgithub/nodejs-project.git'
```

This stage is to clone from github Repo

---
### 2️⃣ Build Docker Image
```
💡 docker build -t $ECR_REPO:$IMAGE_TAG .
```
This stage creates the docker Image

### 3️⃣ Login to AWS ECR
```
💡 aws ecr get-login-password --region $AWS_REGION | \
   docker login --username AWS --password-stdin $ECR_REGISTRY
```
This stage is used to login to AWS ECR

### 4️⃣ Tag Docker Image
```
💡docker tag $ECR_REPO:$IMAGE_TAG $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG
```
This stage creates the docker Image for my application.

### 5️⃣ Push Image to ECR
```
💡 docker push $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG
```

