# Mockingbot — Standalone App

A real, deployable Next.js app. No dependency on claude.ai once it's live.

- `pages/index.js` — the chat UI
- `pages/api/chat.js` — server-side route holding the system prompt; talks to
  Anthropic's API using a key that's never exposed to the browser

## Before you start

You'll need:
1. **A GitHub account** (free) — github.com
2. **A Vercel account** (free) — vercel.com (sign up with GitHub, one click)
3. **An Anthropic API key** — console.anthropic.com → sign up → add billing → API Keys → Create Key

## Step 1: Get your Anthropic API key

1. Go to **console.anthropic.com**, sign in or create an account
2. **Settings → Billing**, add a payment method (this app costs a few cents per conversation to run)
3. **API Keys** in the left sidebar → **Create Key** → name it anything → copy it
   - Starts with `sk-ant-...` — save it, you'll paste it into Vercel in Step 3

## Step 2: Get this code onto GitHub

**Recommended — using git from a terminal** (avoids upload glitches):
```bash
cd path/to/unzipped/mockingbot-app
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```
(Create the empty repo on github.com first, then run the commands above.)

**Alternative — GitHub's web uploader:**
1. github.com → **+** → **New repository** → name it → **Create repository**
2. Click **uploading an existing file**
3. Drag in every file from inside the `mockingbot-app` folder, keeping the `pages/` and `pages/api/` structure intact
4. **Commit changes**

If you go this route and something looks broken later, compare each file's content against this README or ask for the exact content again — GitHub's web uploader can occasionally mix up file contents during multi-file drags.

## Step 3: Deploy on Vercel

1. **vercel.com** → sign in with GitHub
2. **Add New... → Project** → import your repo
3. Before deploying, open **Environment Variables** and add:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** your `sk-ant-...` key
4. **Deploy**
5. ~60 seconds later: a live URL like `mockingbot-yourname.vercel.app`

## Step 4 (optional): Real domain name

Buy one (Namecheap, etc.), then in Vercel: **Settings → Domains** → add it → follow the DNS instructions shown.

## How it works

- Browser sends the message to **your own server** at `/api/chat`
- That route adds the system prompt, attaches your secret key server-side, and calls Anthropic
- The response comes back through your server to the browser
- **The API key never reaches the browser** — nobody can view-source it

## Making changes later

- Edit `pages/index.js` for UI changes (colors, logo, layout, prompts)
- Edit `pages/api/chat.js` for system prompt or model changes
- Push to GitHub — Vercel auto-redeploys in about a minute

## Cost

Billed per API call by token usage. Typical conversation (with web search) costs a few cents.
Set a budget alert in console.anthropic.com → Billing if you want a safety net.
