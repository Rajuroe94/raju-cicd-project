# Raju's CI/CD Pipeline Project - Setup for Rajuroe94

Complete end-to-end CI/CD pipeline using GitHub, Docker, and Kubernetes - Customized for **Rajuroe94**.

## 📋 Prerequisites

Before starting, ensure you have installed:
- Git
- Docker Desktop
- VS Code  
- Python 3.11+
- kubectl (comes with Docker Desktop)

---

## 🚀 Quick Start for Rajuroe94

### YOUR SPECIFIC LINKS:
- 📍 **GitHub Repo:** https://github.com/Rajuroe94/raju-cicd-project
- 🔧 **GitHub Actions:** https://github.com/Rajuroe94/raju-cicd-project/actions
- 🐳 **Docker Hub Image:** https://hub.docker.com/r/rajuroe94/raju-app
- 🔐 **Add Secrets Here:** https://github.com/Rajuroe94/raju-cicd-project/settings/secrets/actions

---

## 📝 Step-by-Step Setup

### 1️⃣ LOCAL SETUP (Your Laptop - 5 minutes)

#### Create Project & Initialize Git
```bash
# Create folder
mkdir raju-cicd-project
cd raju-cicd-project

# Initialize git
git init
git config user.name "Your Name"
git config user.email "your.email@gmail.com"

# Copy all provided files into this folder:
# - app.py
# - requirements.txt
# - Dockerfile
# - deployment.yaml
# - .github/workflows/docker-build.yml
# - .gitignore
```

#### Test Python App Locally
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run the app
python app.py
```

✅ Open your browser → **http://localhost:5000**

You should see: **"Hi Raju! 👋 Welcome to your CI/CD Pipeline!"**

```bash
# Stop the app
Ctrl+C
```

---

### 2️⃣ GITHUB SETUP (2 minutes)

#### Create Repository on GitHub
1. Go to: https://github.com/new
2. Repository name: `raju-cicd-project`
3. Description: `CI/CD pipeline with Flask, Docker, and Kubernetes`
4. Choose: **Public**
5. Click: **Create repository**

#### Push Your Code to GitHub
```bash
# Add all files
git add .

# Commit
git commit -m "Initial commit: Flask app with Docker & Kubernetes setup"

# Set main branch
git branch -M main

# Add remote (Rajuroe94's repo)
git remote add origin https://github.com/Rajuroe94/raju-cicd-project.git

# Push to GitHub
git push -u origin main
```

✅ Check: https://github.com/Rajuroe94/raju-cicd-project

---

### 3️⃣ DOCKER HUB SETUP (5 minutes)

#### Create Docker Hub Account & Repository
1. Go to: https://hub.docker.com/signup (or login if you have account)
2. Create new repository:
   - Click **Create Repository**
   - Name: `raju-app`
   - Visibility: **Public**
   - Create

#### Create Access Token
1. Click on your profile icon → Account Settings
2. Click **Security** in the left menu
3. Click **New Access Token**
4. Name: `github-ci`
5. Copy the token (you'll need it next!)

#### Add GitHub Secrets
These secrets allow GitHub to push images to your Docker Hub account.

1. Go to: https://github.com/Rajuroe94/raju-cicd-project/settings/secrets/actions
2. Click: **New repository secret**

**Secret 1: DOCKER_USERNAME**
- Name: `DOCKER_USERNAME`
- Value: `rajuroe94` (your Docker Hub username)
- Click **Add secret**

**Secret 2: DOCKER_PASSWORD**
- Name: `DOCKER_PASSWORD`
- Value: `paste your access token here` (from step above)
- Click **Add secret**

✅ Both secrets added!

---

### 4️⃣ TEST CI/CD PIPELINE (2 minutes)

The CI/CD pipeline will run automatically whenever you push to GitHub.

#### Trigger a Build
```bash
# Make a small change to app.py (just add a space, save)
# Or just commit an empty commit:
git commit --allow-empty -m "Trigger CI/CD workflow"
git push origin main
```

#### Watch the Build
1. Go to: https://github.com/Rajuroe94/raju-cicd-project/actions
2. You should see a workflow running
3. Click on it to see the build progress
4. Wait for ✅ green checkmark (takes ~2-3 minutes)

✅ Your Docker image has been built and pushed to:  
**https://hub.docker.com/r/rajuroe94/raju-app**

---

### 5️⃣ KUBERNETES SETUP (10 minutes)

#### Enable Kubernetes in Docker Desktop
1. Open **Docker Desktop**
2. Click the gear icon (Settings)
3. Go to **Kubernetes** tab
4. Check the box: **Enable Kubernetes**
5. Click **Apply & Restart**
6. Wait 5-10 minutes for Kubernetes to start

#### Verify Kubernetes is Running
```bash
kubectl cluster-info
```

You should see:
```
Kubernetes control plane is running at https://...
CoreDNS is running at https://...
```

✅ Kubernetes is ready!

---

### 6️⃣ DEPLOY YOUR APP TO KUBERNETES (2 minutes)

#### The deployment.yaml is already customized for you!
It uses: `rajuroe94/raju-app:latest` ✅

#### Deploy
```bash
# Apply the deployment
kubectl apply -f deployment.yaml

# Check deployment
kubectl get deployments
```

You should see:
```
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
raju-app   2/2     2            2           10s
```

#### Check Pods
```bash
kubectl get pods
```

You should see 2 pods running:
```
NAME                        READY   STATUS    RESTARTS   AGE
raju-app-xxxxxxxxxx-xxxxx   1/1     Running   0          30s
raju-app-xxxxxxxxxx-yyyyy   1/1     Running   0          30s
```

#### Check Service
```bash
kubectl get svc raju-app-service
```

You should see:
```
NAME               TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)
raju-app-service   LoadBalancer   10.x.x.x      localhost     80:xxxxx/TCP
```

✅ Service is ready!

---

### 7️⃣ ACCESS YOUR APP IN BROWSER (1 minute)

#### Open in Browser
Open your web browser and go to:
```
http://localhost
```

✅ **You should see: "Hi Raju! 👋 Welcome to your CI/CD Pipeline!"**

Congratulations! Your app is now running in Kubernetes! 🎉

---

## 🔄 CONTINUOUS WORKFLOW - Making Changes

Once everything is set up, here's how to make changes:

### Step 1: Edit Your Code
```bash
# Edit app.py in VS Code
# For example, change the welcome message
```

### Step 2: Test Locally
```bash
# Activate virtual environment
source venv/bin/activate

# Run app locally
python app.py

# Check: http://localhost:5000
```

### Step 3: Commit and Push
```bash
# Commit your changes
git add .
git commit -m "Updated welcome message"
git push origin main
```

### Step 4: GitHub Actions Builds Automatically
- Go to: https://github.com/Rajuroe94/raju-cicd-project/actions
- Watch the workflow build and push image to Docker Hub
- Wait for ✅ green checkmark

### Step 5: Restart Kubernetes Pods
```bash
# Tell Kubernetes to restart the pods with new image
kubectl rollout restart deployment/raju-app

# Watch pods restart
kubectl get pods -w
```

### Step 6: Refresh Browser
```
http://localhost
```

✅ Your changes are now live!

---

## 📊 Useful Commands Reference

### Kubernetes Commands
```bash
# View all resources
kubectl get all

# View pods
kubectl get pods

# View deployment
kubectl get deployment raju-app

# View service
kubectl get svc raju-app-service

# View pod logs
kubectl logs <POD_NAME>

# Stream logs in real-time
kubectl logs -f <POD_NAME>

# Describe pod for troubleshooting
kubectl describe pod <POD_NAME>

# Restart deployment
kubectl rollout restart deployment/raju-app

# Delete everything
kubectl delete deployment raju-app
kubectl delete service raju-app-service
```

### Docker Commands (Local Testing)
```bash
# Build image locally
docker build -t rajuroe94/raju-app:test .

# Run image locally
docker run -d -p 5000:5000 rajuroe94/raju-app:test

# List containers
docker ps

# Stop container
docker stop <CONTAINER_ID>

# View logs
docker logs <CONTAINER_ID>
```

### Git Commands
```bash
# View commit history
git log --oneline

# Check status
git status

# Undo last commit (before push)
git reset --soft HEAD~1
```

---

## 🔄 Your Pipeline Flow

```
1. You edit app.py in VS Code
   ↓
2. git push origin main
   ↓
3. GitHub Actions automatically triggers
   ↓
4. Builds Docker image
   ↓
5. Pushes to Docker Hub: rajuroe94/raju-app
   ↓
6. You restart Kubernetes: kubectl rollout restart deployment/raju-app
   ↓
7. Kubernetes pulls new image and restarts pods
   ↓
8. Your changes are live! http://localhost
```

---

## ✅ Verification Checklist

- [ ] Local app runs: `python app.py` → http://localhost:5000
- [ ] Code on GitHub: https://github.com/Rajuroe94/raju-cicd-project
- [ ] Docker Hub account & repo created: https://hub.docker.com/r/rajuroe94/raju-app
- [ ] GitHub Secrets added: DOCKER_USERNAME + DOCKER_PASSWORD
- [ ] GitHub Actions ran successfully (check Actions tab)
- [ ] Docker image exists in Docker Hub
- [ ] Kubernetes enabled in Docker Desktop
- [ ] Deployment applied: `kubectl apply -f deployment.yaml`
- [ ] Pods running: `kubectl get pods` (shows 2 pods)
- [ ] Service created: `kubectl get svc` (shows LoadBalancer)
- [ ] App accessible: http://localhost (shows "Hi Raju!")

---

## 🆘 Troubleshooting

**Problem: Pods not starting?**
```bash
kubectl describe pod <POD_NAME>
kubectl logs <POD_NAME>
```

**Problem: Image not pulling from Docker Hub?**
- Check username is correct in `deployment.yaml`: `rajuroe94`
- Check image exists: https://hub.docker.com/r/rajuroe94/raju-app
- Check GitHub Actions completed successfully

**Problem: LoadBalancer shows "pending"?**
This is normal in local Kubernetes. Use port-forward:
```bash
kubectl port-forward svc/raju-app-service 8080:80
# Then visit: http://localhost:8080
```

**Problem: GitHub Actions failed?**
- Check GitHub Secrets are correct
- View workflow logs in Actions tab
- Common issue: wrong Docker Hub credentials

**Problem: Can't connect to http://localhost?**
```bash
# Check service details
kubectl get svc raju-app-service

# Port forward manually
kubectl port-forward svc/raju-app-service 80:5000

# Then try: http://localhost
```

---

## 📚 Resources

- Docker Docs: https://docs.docker.com/
- Kubernetes Docs: https://kubernetes.io/docs/
- GitHub Actions: https://docs.github.com/en/actions
- Flask: https://flask.palletsprojects.com/

---

## 🎯 Your GitHub & Docker Hub

**GitHub Username:** Rajuroe94  
**GitHub Repo:** https://github.com/Rajuroe94/raju-cicd-project  
**Docker Hub Username:** rajuroe94  
**Docker Hub Image:** https://hub.docker.com/r/rajuroe94/raju-app  

---

Made with ❤️ for Rajuroe94's DevOps Journey! 🚀

Ready to deploy? Start from **Step 1: LOCAL SETUP** above! 👆
