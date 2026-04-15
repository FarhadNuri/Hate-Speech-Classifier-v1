# 🚂 Deploy to Railway - Complete Step-by-Step Guide

Railway is the easiest way to deploy your Flask app. It's free to start and automatically detects your app.

---

## Prerequisites

1. ✅ GitHub account
2. ✅ Railway account (we'll create this)
3. ✅ Your code pushed to GitHub

---

## Part 1: Push Your Code to GitHub

### Step 1: Create a GitHub Repository

1. Go to https://github.com
2. Click the **"+"** icon in the top right
3. Click **"New repository"**
4. Fill in:
   - Repository name: `bengali-hate-speech-classifier`
   - Description: `Bengali hate speech classification using Flask and ML`
   - Choose **Public** or **Private**
   - **DO NOT** check "Add a README file"
5. Click **"Create repository"**

### Step 2: Push Your Code

Open your terminal in the project folder and run:

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit - Flask app ready for deployment"

# Add your GitHub repository as remote
git remote add origin https://github.com/YOUR_USERNAME/bengali-hate-speech-classifier.git

# Push to GitHub
git branch -M main
git push -u origin main
```

**Replace `YOUR_USERNAME`** with your actual GitHub username.

**If you get an error about secrets**, follow the instructions in `GIT_PUSH_FIX.md`.

---

## Part 2: Deploy to Railway

### Step 1: Create Railway Account

1. Go to https://railway.app
2. Click **"Login"** in the top right
3. Click **"Login with GitHub"**
4. Authorize Railway to access your GitHub account
5. You'll get **$5 free credit** per month (no credit card needed!)

### Step 2: Create New Project

1. Once logged in, click **"New Project"**
2. Click **"Deploy from GitHub repo"**
3. If this is your first time:
   - Click **"Configure GitHub App"**
   - Select which repositories Railway can access
   - Choose **"Only select repositories"**
   - Select your `bengali-hate-speech-classifier` repository
   - Click **"Install & Authorize"**
4. Back on Railway, you'll see your repository listed
5. Click on **`bengali-hate-speech-classifier`**

### Step 3: Railway Auto-Detects Your App

Railway will automatically:
- ✅ Detect it's a Python app
- ✅ Find your `requirements.txt`
- ✅ Find your `Procfile`
- ✅ Start building your app

You'll see a build log showing:
```
Building...
Installing dependencies...
Starting web server...
```

This takes about 2-3 minutes.

### Step 4: Wait for Deployment

Watch the deployment logs. You'll see:
- Installing Python packages
- Downloading your model from HuggingFace
- Starting the server

When you see:
```
✓ Build successful
✓ Deployment live
```

Your app is ready!

### Step 5: Get Your App URL

1. In the Railway dashboard, click on your project
2. Click on the **"Settings"** tab
3. Scroll down to **"Domains"**
4. Click **"Generate Domain"**
5. Railway will give you a URL like:
   ```
   https://bengali-hate-speech-classifier-production.up.railway.app
   ```
6. Click on the URL to open your app!

---

## Part 3: Test Your Deployed App

1. Open the Railway-generated URL
2. You should see your black and white UI
3. Enter some Bengali text
4. Click "Analyze Text"
5. Check if predictions work!

---

## Part 4: Monitor Your App

### View Logs

1. In Railway dashboard, click on your project
2. Click on the **"Deployments"** tab
3. Click on the latest deployment
4. You'll see real-time logs showing:
   - Model loading
   - Incoming requests
   - Predictions being made

### Check Usage

1. Click on **"Metrics"** tab
2. See:
   - Memory usage
   - CPU usage
   - Request count
   - Response times

---

## Part 5: Update Your App

When you make changes to your code:

```bash
# Make your changes to files
# Then commit and push

git add .
git commit -m "Update UI design"
git push origin main
```

Railway will **automatically**:
1. Detect the push
2. Rebuild your app
3. Deploy the new version
4. Zero downtime!

---

## Troubleshooting

### Build Failed

**Check the logs:**
1. Click on the failed deployment
2. Read the error message
3. Common issues:
   - Missing package in `requirements.txt`
   - Syntax error in code
   - Port configuration issue

**Fix:**
1. Fix the issue locally
2. Test locally: `python app.py`
3. Push the fix: `git push origin main`

### App Crashes on Start

**Check if model is loading:**
1. Look at logs for "Loading model artifacts..."
2. If it fails, the HuggingFace model might be private
3. Make sure your model is public on HuggingFace

### Out of Memory

Railway free tier has 512MB RAM. If your app uses more:

**Solution 1: Upgrade Plan**
- Click "Settings" → "Plan"
- Upgrade to Hobby plan ($5/month for 8GB RAM)

**Solution 2: Optimize**
- The model files are large (~1GB)
- Consider using a smaller model

### Slow First Request

The first request after deployment is slow because:
1. Model needs to download from HuggingFace
2. Model needs to load into memory

**This is normal!** Subsequent requests are fast.

---

## Cost & Limits

### Free Tier ($5 credit/month)
- ✅ 512MB RAM
- ✅ 1GB disk space
- ✅ Shared CPU
- ✅ Custom domain
- ✅ Automatic HTTPS
- ⚠️ Sleeps after 30 minutes of inactivity

### Hobby Tier ($5/month)
- ✅ 8GB RAM
- ✅ 100GB disk space
- ✅ Dedicated CPU
- ✅ No sleep
- ✅ Priority support

---

## Custom Domain (Optional)

### Add Your Own Domain

1. Buy a domain (e.g., from Namecheap, GoDaddy)
2. In Railway, go to Settings → Domains
3. Click "Custom Domain"
4. Enter your domain: `classifier.yourdomain.com`
5. Railway will show you DNS records to add
6. Add these records in your domain registrar:
   ```
   Type: CNAME
   Name: classifier
   Value: [Railway provides this]
   ```
7. Wait 5-60 minutes for DNS to propagate
8. Your app will be live at your custom domain!

---

## Environment Variables (If Needed)

If you need to add secrets (like API keys):

1. Go to your project in Railway
2. Click **"Variables"** tab
3. Click **"New Variable"**
4. Add:
   - Key: `HF_TOKEN`
   - Value: `your_huggingface_token`
5. Click **"Add"**
6. Railway will automatically restart your app

Then in your code:
```python
import os
token = os.environ.get('HF_TOKEN')
```

---

## Success Checklist

- ✅ Code pushed to GitHub
- ✅ Railway project created
- ✅ App deployed successfully
- ✅ URL generated
- ✅ App loads in browser
- ✅ Predictions work
- ✅ Logs show no errors

---

## Next Steps

1. Share your app URL with others!
2. Monitor usage in Railway dashboard
3. Set up custom domain (optional)
4. Upgrade to Hobby tier if needed
5. Add analytics (optional)

---

## Support

- Railway Docs: https://docs.railway.app
- Railway Discord: https://discord.gg/railway
- Railway Status: https://status.railway.app

---

## Your App is Live! 🎉

Your Bengali Hate Speech Classifier is now accessible worldwide at your Railway URL!
