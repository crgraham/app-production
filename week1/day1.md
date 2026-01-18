# INSTANT GRATIFICATION!

## Production Deployment in minutes

This guide will walk you through deploying a simple FastAPI application to Vercel in under 10 minutes.

## Step 1: Sign Up for Vercel

1. Open your web browser and navigate to [https://vercel.com](https://vercel.com)
2. Click the **Sign Up** button in the top right corner
3. Select **Hobby** (for personal projects)
4. Enter your name
5. Choose one of the following sign-up methods:
   - **GitHub** (recommended) - Click "Continue with GitHub" and authorize Vercel
   - **GitLab** - Click "Continue with GitLab" and authorize Vercel
   - **Bitbucket** - Click "Continue with Bitbucket" and authorize Vercel
   - **Email** - Enter your email address and follow the verification steps
6. Complete the onboarding (you can skip team creation)

## Step 2: Install Cursor IDE

> Note: You can use a different IDE if you prefer (VS Code, PyCharm, etc.), but these instructions assume you're using Cursor.

**Windows:**
1. Visit [https://cursor.com](https://cursor.com)
2. Click "Download for Windows"
3. Run the downloaded `.exe` installer
4. Follow the installation wizard
5. Launch Cursor from your Start Menu or Desktop

**Mac:**
1. Visit [https://cursor.com](https://cursor.com)
2. Click "Download for Mac"
3. Open the downloaded `.dmg` file
4. Drag Cursor to your Applications folder
5. Launch Cursor from Applications or Spotlight (Cmd+Space, type "Cursor")

**Linux:**
1. Visit [https://cursor.com](https://cursor.com)
2. Click "Download for Linux"
3. Extract the `.tar.gz` file:
   ```bash
   tar -xzf cursor-*.tar.gz
   ```
4. Move to `/opt` and create a symlink:
   ```bash
   sudo mv cursor /opt/
   sudo ln -s /opt/cursor/cursor /usr/local/bin/cursor
   ```
5. Launch by typing `cursor` in terminal

### Create Your Project Folder

1. Open Cursor
2. **Windows/Linux:** Click File → Open Folder → Create a new folder called "instant"
3. **Mac:** Click File → Open → Create a new folder called "instant"
4. Select and open the "instant" folder

## Step 3: Create Your FastAPI Application

In Cursor, create a new file called `instant.py` with the following content:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def instant():
    return "Live from production!"
```

Save the file (Ctrl+S on Windows/Linux, Cmd+S on Mac).

## Step 4: Create Requirements File

Create a new file called `requirements.txt` with the following content:

```
fastapi
uvicorn
```

Save the file.

## Step 5: Create Vercel Configuration

Create a new file called `vercel.json` with the following content:

```json
{
    "builds": [
        {
            "src": "instant.py",
            "use": "@vercel/python"
        }
    ],
    "routes": [
        {
            "src": "/(.*)",
            "dest": "instant.py"
        }
    ]
}
```

Save the file.

## Step 6: Install Node.js

Node.js is required for the Vercel CLI.

1. Visit the official Node.js download page: [https://nodejs.org/en/download](https://nodejs.org/en/download)

2. Choose your preferred installation method:
   - **Direct Download:** Download the installer for your operating system
   - **Package Manager:** Use the package manager for your platform (Homebrew for Mac, Chocolatey for Windows, etc.)
   - **Version Manager (recommended):** Use nvm, fnm, or volta for easy version management

3. After installation, open a **new** terminal window

4. Verify installation:
   ```bash
   node --version
   npm --version
   ```

Both commands should return version numbers if installed correctly.

## Step 7: Deploy to Vercel

### Open Terminal in Cursor

- Click Terminal → New Terminal (or press Ctrl+\` on Windows/Linux, Cmd+\` on Mac)

**Make sure you're in your "instant" project folder** - you should see your three files (instant.py, requirements.txt, vercel.json) when you list files.

### Install Vercel CLI and Deploy

1. Install Vercel CLI globally:
   ```bash
   npm install -g vercel
   ```

2. Login to Vercel:
   ```bash
   vercel login
   ```
   - Enter the email address you used to sign up for Vercel
   - Check your email for a verification link and click it
   - Return to the terminal - it should confirm you're logged in

3. Deploy to Vercel (development):
   ```bash
   vercel .
   ```
   - When prompted "Set up and deploy?"  → Press Enter (Yes)
   - "Which scope?"  → Select your personal account
   - "Link to existing project?"  → Type `n` and press Enter (No)
   - "What's your project's name?"  → Type `instant` and press Enter
   - "In which directory is your code located?"  → Press Enter (current directory)
   - Wait for deployment to complete (usually 30-60 seconds)
   - You'll see a URL like `https://instant-xxxxxx.vercel.app`

4. Test your development deployment:
   - Click the URL provided (or copy and paste into browser)
   - You should see: **"Live from production!"**


## Congratulations! 🎉

You've successfully deployed your first API to production! Your API is now:
- ✅ Live on the internet
- ✅ Automatically scaled
- ✅ Secured with HTTPS
- ✅ Accessible from anywhere in the world

### What You've Learned:
- How to create a simple FastAPI application
- How to configure a project for Vercel deployment
- How to use the Vercel CLI for deployment

### Next Steps:
- Try modifying the message in `instant.py` and redeploying
- Add more API endpoints
- Explore Vercel's dashboard at [https://vercel.com/dashboard](https://vercel.com/dashboard)

## Troubleshooting

### "vercel: command not found"
- Make sure you opened a **new** terminal after installing Node.js
- Try running `npm install -g vercel` again

### "Python version not supported"
- Vercel supports Python 3.9, 3.10, 3.11, and 3.12
- The default should work, but if you have issues, add a `runtime.txt` file with: `python-3.12`

### Deployment fails
- Check that all three files (instant.py, requirements.txt, vercel.json) are in your project folder
- Make sure you're in the correct directory when running `vercel`
- Ensure your vercel.json has the exact JSON structure shown above

### Need Help?
- Check Vercel's documentation: [https://vercel.com/docs](https://vercel.com/docs)
- Ask in class or post in the course forum
  
### Summary
Step 1: Sign up for Vercel. This matters because Vercel is the hosting platform you’re deploying onto; without an account you can’t create a project, get a deployment URL, or manage deployments/keys/logs. Picking “Hobby” is just the free-tier choice; GitHub signup is recommended mainly because it makes future “deploy from repo” workflows smoother, even though this tutorial uses the CLI.

Step 2: Install Cursor + create the “instant” folder. Cursor is just the editor; the important part is creating a clean project directory where your three deployment-critical files live together. This avoids the #1 beginner failure: running vercel from the wrong folder and deploying something else by accident.

Step 3: Create instant.py (FastAPI app). This is your actual web service. app = FastAPI() creates the ASGI app object, and @app.get("/") declares a route so you can hit / and get a response. It’s a deliberately tiny “health check” endpoint to prove the whole request → server → response path works end-to-end.

Step 4: Create requirements.txt. This is how Vercel knows what Python dependencies to install when it builds your serverless function. If fastapi isn’t listed, the build will fail. uvicorn is included because it’s the common dev server for running FastAPI locally; Vercel won’t necessarily run uvicorn directly, but keeping it here is fine for local testing and avoids confusion later.

Step 5: Create vercel.json. This is the glue that tells Vercel (a) “treat instant.py as a Python serverless entrypoint” (@vercel/python) and (b) “send all incoming routes to that file” (/(.*) → instant.py). Without this, Vercel won’t know which file to deploy or how to route requests, and you’ll typically get 404s or a build that doesn’t expose your API.

Step 6: Install Node.js (and npm). This matters because the Vercel CLI is a Node tool; you need Node/npm to install and run it. Using a version manager (nvm) matters because it prevents “my system node is old/broken” problems and makes upgrades/reverts painless. Verifying node --version and npm --version is a quick sanity check that your terminal can actually see the installs (PATH correctness).

Step 7: Deploy with the Vercel CLI. Opening a terminal inside Cursor is convenience; the important part is you’re in the project folder when running commands. npm install -g vercel installs the CLI globally so vercel is available as a command. vercel login links your local CLI to your Vercel account (auth). vercel . deploys the current directory: the prompts create a new project, choose which account/team (“scope”) owns it, set the project name, and confirm the code directory. The final URL test is crucial because it confirms the deployed function is reachable publicly, routing works, dependencies installed, and FastAPI is responding.
Troubleshooting section: it’s basically a checklist of the common failure points in each stage: CLI not on PATH (vercel: command not found), runtime mismatch (Python versions), missing files or wrong working directory (deployment fails). The reason this section is important is that these are environmental/deployment issues, not “your code is wrong” issues, and they’re what usually block people on day one.
