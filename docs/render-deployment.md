# Deployment Guide: GitHub & Render

This guide provides step-by-step instructions for uploading **College Event Hub** to GitHub (`ayushverma1903`) and deploying it live on **Render**.

---

## Part 1: Push Code to GitHub (`ayushverma1903`)

### Step 1: Create a GitHub Repository
1. Open your browser and go to: [https://github.com/new](https://github.com/new)
2. **Repository name**: `college-event-hub`
3. Set visibility to **Public** or **Private** as desired.
4. Click **Create repository**.

### Step 2: Push Local Code to GitHub
Open PowerShell / Terminal in your project directory (`d:\project\collegeeventhub\collegeeventhub`) and run:

```bash
# 1. Ensure remote URL is configured to your repository
git remote set-url origin https://github.com/ayushverma1903/college-event-hub.git

# 2. Push to main branch
git push -u origin main
```

> **Note**: If prompted for credentials by GitHub:
> - User: `ayushverm1903`
> - Password: Use a **Personal Access Token (PAT)** generated from [GitHub Settings > Developer Settings > Personal Access Tokens](https://github.com/settings/tokens) or use GitHub Desktop / VS Code Git integration.

---

## Part 2: Deploy on Render

Render will automatically host your Node.js application and connect to your MongoDB Atlas database.

### Option A: Deploy using Render Blueprint (Recommended - 1 Click)

1. Go to [Render Dashboard](https://dashboard.render.com/) and log in (or Sign Up using GitHub).
2. Click **New +** in the top right and select **Blueprint**.
3. Connect your GitHub repository (`ayushverm1903/college-event-hub`).
4. Render will automatically detect `render.yaml` and configure:
   - **Service Name**: `college-event-hub`
   - **Environment**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
   - **Environment Variables**: Pre-configured MongoDB connection & production flags.
5. Click **Apply**. Render will build and launch your application!

---

### Option B: Deploy Manually as a Web Service

If you prefer creating the Web Service manually on Render:

1. Click **New +** > **Web Service**.
2. Select **Build and deploy from a Git repository**.
3. Choose `ayushverm1903/college-event-hub`.
4. Configure settings:
   - **Name**: `college-event-hub`
   - **Region**: Oregon (US West) or nearest region
   - **Branch**: `main`
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
   - **Instance Type**: `Free`
5. Under **Environment Variables**, add:

| Key | Value |
| --- | --- |
| `NODE_ENV` | `production` |
| `SESSION_SECRET` | `your_secret_key_here` |
| `MONGODB_URI` | `mongodb+srv://tanushreekumbhare11_db_user:LAUOMNrXqnGuwTaJ@cluster0.bvf4swb.mongodb.net/college_event_hub?retryWrites=true&w=majority` |

6. Click **Create Web Service**.

---

## Part 3: Verification & Post-Deployment

Once deployed, Render will provide a live URL such as `https://college-event-hub.onrender.com`.

1. Open your live app URL in the browser.
2. Verify endpoints:
   - Homepage: `https://<your-app>.onrender.com/`
   - Health Check: `https://<your-app>.onrender.com/api/health`
3. Optional: Seed admin user on production:
   - Run `npm run seed:admin` using Render's Shell feature if you wish to pre-populate admin credentials.
