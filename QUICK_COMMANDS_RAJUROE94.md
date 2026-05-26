# QUICK COMMAND REFERENCE FOR RAJUROE94

## ⚡ COPY-PASTE COMMANDS IN ORDER

### PART 1: LOCAL SETUP (Run these first)
```bash
# 1. Create project folder
mkdir raju-cicd-project
cd raju-cicd-project

# 2. Initialize git
git init
git config user.name "Your Name"
git config user.email "your.email@gmail.com"

# 3. Copy all files into this folder from the provided outputs

# 4. Create virtual environment and test
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python app.py
# Open browser: http://localhost:5000
# Press Ctrl+C to stop
```

---

### PART 2: PUSH TO GITHUB (Your Repo)
```bash
# 1. Commit all files
git add .
git commit -m "Initial commit: Flask app with CI/CD pipeline"
git branch -M main

# 2. Add your GitHub repo (Rajuroe94)
git remote add origin https://github.com/Rajuroe94/raju-cicd-project.git

# 3. Push to GitHub
git push -u origin main

# ✅ Check: https://github.com/Rajuroe94/raju-cicd-project
```

---

### PART 3: DOCKER HUB SETUP
```bash
# 1. Create Docker Hub account: https://hub.docker.com/signup
# 2. Create new repository: 
#    - Name: raju-app
#    - Keep Public
#    - Save

# 3. Get Access Token:
#    - Docker Hub Account Settings → Security
#    - Create New Access Token
#    - Copy the token (you'll need it next)

# 4. In GitHub - Add Secrets:
#    - Go: https://github.com/Rajuroe94/raju-cicd-project/settings/secrets/actions
#    - Create Secret 1:
#      Name: DOCKER_USERNAME
#      Value: rajuroe94
#    - Create Secret 2:
#      Name: DOCKER_PASSWORD
#      Value: <paste your Docker Hub access token>

# 5. Test CI/CD by pushing
git add .
git commit -m "Test CI/CD"
git push origin main

# Check GitHub Actions:
# https://github.com/Rajuroe94/raju-cicd-project/actions
# Watch the workflow run!
```

---

### PART 4: ENABLE KUBERNETES
```bash
# 1. Open Docker Desktop
# 2. Settings → Kubernetes → Check "Enable Kubernetes"
# 3. Wait 5-10 minutes for it to start

# 4. Verify
kubectl cluster-info
```

---

### PART 5: DEPLOY TO KUBERNETES
```bash
# 1. deployment.yaml already has: rajuroe94/raju-app:latest
#    (This is already updated for you!)

# 2. Deploy to Kubernetes
kubectl apply -f deployment.yaml

# 3. Check deployment status
kubectl get pods
kubectl get svc raju-app-service

# 4. Wait for LoadBalancer IP (may take 1-2 minutes)
kubectl get svc raju-app-service -w

# You should see something like:
# NAME                 TYPE           CLUSTER-IP    EXTERNAL-IP
# raju-app-service     LoadBalancer   10.x.x.x      localhost

# 5. Open browser: http://localhost
# ✅ You should see "Hi Raju! 👋"
```

---

## 🔄 AFTER DEPLOYMENT - CONTINUOUS WORKFLOW

### Making Changes to Your App:
```bash
# 1. Edit app.py in VS Code (make a change)

# 2. Test locally
python app.py
# Check: http://localhost:5000

# 3. Commit and push
git add app.py
git commit -m "Updated app message"
git push origin main

# 4. Watch GitHub Actions build:
# https://github.com/Rajuroe94/raju-cicd-project/actions

# 5. Once build is done, restart Kubernetes
kubectl rollout restart deployment/raju-app

# 6. Watch pods restart
kubectl get pods -w

# 7. Refresh browser to see new changes
# http://localhost
```

---

## 🆘 DEBUGGING COMMANDS

```bash
# View pod logs
kubectl logs <POD_NAME>

# Watch pods in real-time
kubectl get pods -w

# Describe pod (full info)
kubectl describe pod <POD_NAME>

# View all resources
kubectl get all

# If LoadBalancer not working, port forward:
kubectl port-forward svc/raju-app-service 8080:80
# Then visit: http://localhost:8080
```

---

## 📋 YOUR SPECIFIC LINKS

**GitHub Repo:**  
https://github.com/Rajuroe94/raju-cicd-project

**GitHub Actions (CI/CD):**  
https://github.com/Rajuroe94/raju-cicd-project/actions

**GitHub Secrets (Add DOCKER creds):**  
https://github.com/Rajuroe94/raju-cicd-project/settings/secrets/actions

**Docker Hub Image (after first build):**  
https://hub.docker.com/r/rajuroe94/raju-app

---

## ✅ VERIFICATION CHECKLIST

- [ ] Python app runs locally (`python app.py` → http://localhost:5000)
- [ ] Code pushed to GitHub: https://github.com/Rajuroe94/raju-cicd-project
- [ ] Docker Hub secrets added (DOCKER_USERNAME & DOCKER_PASSWORD)
- [ ] GitHub Actions workflow ran successfully (check Actions tab)
- [ ] Docker image built and pushed to: https://hub.docker.com/r/rajuroe94/raju-app
- [ ] Kubernetes enabled in Docker Desktop
- [ ] deployment.yaml applied: `kubectl apply -f deployment.yaml`
- [ ] Pods running: `kubectl get pods`
- [ ] Service created: `kubectl get svc`
- [ ] App accessible in browser: http://localhost

---

🎉 You're all set! Follow these commands in order and you'll have a complete CI/CD pipeline running locally!
