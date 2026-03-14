# WAF Detector — Deploy to Railway

## Files
```
waf-app/
├── app.py              # Flask backend + WAF detection logic
├── requirements.txt    # Python dependencies
├── Procfile            # Railway/gunicorn start command
├── README.md           # This file
└── static/
    └── index.html      # Frontend (served by Flask)
```

## Deploy to Railway (5 minutes)

### Step 1 — Create GitHub repo
1. Go to github.com → New repository
2. Name it `waf-detector` (public or private, both work)
3. Don't initialize with README

### Step 2 — Push these files
```bash
cd waf-app
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/waf-detector.git
git push -u origin main
```

### Step 3 — Deploy on Railway
1. Go to railway.app → New Project
2. Click **"Deploy from GitHub repo"**
3. Select your `waf-detector` repo
4. Railway auto-detects Python and deploys
5. Click **"Generate Domain"** under Settings → Networking
6. Your public URL is ready in ~2 minutes

### Step 4 — Share the URL
Your app will be live at:
`https://waf-detector-xxxx.up.railway.app`

Share this URL with your interviewer.

## Local testing (optional)
```bash
pip install -r requirements.txt
python app.py
# Open http://localhost:5000
```

## Lead capture
Leads are currently logged to the Railway console.
To save them: edit the `/api/lead` route in `app.py` to write to a file or send an email.
