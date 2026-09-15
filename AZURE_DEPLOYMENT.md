# Azure Deployment Guide for Sakshi Portfolio

This project is built with **React** + **Vite** + **Tailwind CSS**. It is ready for seamless deployment to Microsoft Azure.

---

## Option 1: Azure Static Web Apps (Recommended ⭐)

Azure Static Web Apps is the best, fastest, and free-tier-friendly service for React & Vite websites.

### Step-by-Step Deployment:
1. Go to the [Azure Portal](https://portal.azure.com).
2. Click **Create a resource** and search for **Static Web App**.
3. Fill in the basics:
   - **Subscription**: Select your Azure subscription
   - **Resource Group**: Select or create a new resource group
   - **Name**: `sakshi-portfolio` (or your preferred name)
   - **Plan type**: **Free**
   - **Deployment source**: Select **GitHub**
4. Sign in with GitHub and select:
   - **Organization**: `Sakshi-1142`
   - **Repository**: `Portfolio`
   - **Branch**: `main`
5. In the **Build Details** section:
   - **Build Presets**: Select `Custom` (or `Vite`)
   - **App location**: `/`
   - **Api location**: *(leave empty)*
   - **Output location**: `dist`
6. Click **Review + Create**, then **Create**.
7. Azure will automatically configure a GitHub Actions workflow in your repository. Within 2-3 minutes, your site will be live with a free SSL certificate and custom domain support!

---

## Option 2: Azure App Service

If you prefer using **Azure App Service**:

### For Azure App Service (Windows):
- The `web.config` file has already been added to `/public/web.config` and is copied to `dist/` on build. It handles client-side SPA routing and prevents 404 errors on page reload.

### For Azure App Service (Linux / Node):
- Set the Startup Command in Azure App Service Configuration to:
  ```bash
  npm run build && npm run start
  ```
  or serve using PM2:
  ```bash
  pm2 serve /home/site/wwwroot/dist --no-daemon --spa
  ```

---

## Configuration Files Added

- `staticwebapp.config.json` (Root & `public/`): Azure Static Web Apps routing rules, fallback for SPA routing, security headers, and MIME types.
- `public/web.config`: IIS URL rewrite rules for Azure App Service (Windows).
- `package.json`: Added `start` script for Azure Node runtime preview.
