# 🚀 Quick Start Guide - Pride Share

## Get Your App Running in 30 Minutes

This guide will get your Pride Share signup page live and ready for your presentation.

---

## ⚡ Prerequisites

Before starting, make sure you have:
- [ ] GitHub account
- [ ] Supabase account (free tier)
- [ ] Google Cloud account (for Gemini API - $300 free credit)
- [ ] Railway OR Render account (backend hosting - free tier)
- [ ] Vercel account (frontend hosting - free tier)

---

## 📝 Step-by-Step Setup

### STEP 1: Supabase Database (5 minutes)

1. Go to [supabase.com](https://supabase.com) and sign up
2. Create new project:
   - Name: `prideshare-pnw`
   - Database password: **Save this!**
   - Region: `East US`
3. Wait 2 minutes for provisioning
4. Go to Project Settings → API
5. Copy these values:
   ```
   SUPABASE_URL=https://xxxxx.supabase.co
   SUPABASE_ANON_KEY=eyJhbGc...
   SUPABASE_SERVICE_KEY=eyJhbGc... (keep this secret!)
   ```
6. Go to SQL Editor → New Query
7. Copy & paste contents of `database_schema.sql`
8. Click **Run**
9. ✅ You should see "Success" - your database is ready!

---

### STEP 2: Google Gemini API (3 minutes)

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with Google account
3. Click **Get API Key** → **Create API key**
4. Copy the key:
   ```
   GEMINI_API_KEY=AIza...
   ```
5. ✅ Done! You have free quota for testing

---

### STEP 3: Deploy Backend (10 minutes)

#### Option A: Railway (Recommended)

1. Go to [railway.app](https://railway.app)
2. Sign up with GitHub
3. Click **New Project** → **Deploy from GitHub repo**
4. Connect your GitHub account
5. Select your forked `prideshare-backend` repo
6. Railway auto-detects Python
7. Go to **Variables** tab and add:
   ```
   SUPABASE_URL=your_url_from_step1
   SUPABASE_SERVICE_KEY=your_service_key_from_step1
   GEMINI_API_KEY=your_key_from_step2
   FRONTEND_URL=https://prideshare.vercel.app (we'll update this)
   ENVIRONMENT=production
   ```
8. Railway deploys automatically (~2 min)
9. Copy your deployment URL:
   ```
   https://prideshare-backend-production.up.railway.app
   ```
10. Test it: Visit `https://your-url.railway.app/health`
11. ✅ If you see `{"status":"healthy"}`, you're good!

---

### STEP 4: Deploy Frontend (10 minutes)

1. Go to [vercel.com](https://vercel.com)
2. Sign up with GitHub
3. Click **Add New** → **Project**
4. Import your `prideshare-frontend` repo
5. Configure:
   - **Root Directory**: Leave as `./` (or set to `frontend` if monorepo)
   - **Framework Preset**: Next.js
6. Add Environment Variables:
   ```
   NEXT_PUBLIC_API_URL=https://your-railway-url.railway.app
   NEXT_PUBLIC_SUPABASE_URL=your_url_from_step1
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key_from_step1
   ```
7. Click **Deploy**
8. Wait 2 minutes
9. Copy your deployment URL:
   ```
   https://prideshare.vercel.app
   ```
10. ✅ Visit the URL - you should see your landing page!

---

### STEP 5: Update Backend CORS (2 minutes)

1. Go back to Railway
2. Update the `FRONTEND_URL` variable:
   ```
   FRONTEND_URL=https://prideshare.vercel.app
   ```
3. Railway redeploys automatically
4. ✅ Your backend now accepts requests from your frontend!

---

### STEP 6: Test the Complete Flow (5 minutes)

1. Visit `https://prideshare.vercel.app`
2. Click **Join Now**
3. Fill out the signup form with:
   ```
   Email: test@pnw.edu
   Name: Test Student
   ZIP: 46323
   Role: Both
   ```
4. Click **Continue to Schedule**
5. Choose **Enter Manually**
6. Add a test class:
   ```
   Course: CS 240
   Building: NILS
   Days: Monday, Wednesday
   Time: 10:30 - 11:20
   ```
7. Click **Add This Class**
8. Click **Complete Signup**
9. ✅ If you see success message, everything works!

---

### STEP 7: Verify in Database (2 minutes)

1. Go to Supabase → Table Editor
2. Check `users` table → you should see 1 row
3. Check `schedules` table → you should see 1 row
4. ✅ Data is being saved correctly!

---

## 🎯 For Your Presentation

### Generate QR Code

1. Go to [qr-code-generator.com](https://www.qr-code-generator.com/)
2. Enter your signup URL:
   ```
   https://prideshare.vercel.app/signup
   ```
3. Customize:
   - Add PNW logo (center)
   - Colors: Gold (#CFB87C) and Black
   - Size: 500x500 px
4. Download as PNG
5. ✅ Print this on your flyers/posters!

### Create Demo Account

1. Create a test account with your actual @pnw.edu email
2. Add your real class schedule
3. This will be your demo account during presentation
4. ✅ You can show live matching!

---

## 📊 Monitor Your App

### Check Backend Health
```bash
curl https://your-backend-url.railway.app/health
```

### Check Frontend
```bash
curl https://prideshare.vercel.app
```

### View Logs

**Railway:**
- Go to your project → Deployments → View Logs

**Vercel:**
- Go to your project → Deployments → Click deployment → View Logs

---

## 🐛 Troubleshooting

### "Failed to connect to database"
- Check Supabase is running
- Verify `SUPABASE_URL` and `SUPABASE_SERVICE_KEY` are correct
- Ensure no extra spaces in environment variables

### "CORS error" in browser console
- Verify `FRONTEND_URL` in Railway matches your Vercel URL exactly
- Check for `http://` vs `https://`
- Redeploy backend after changing CORS settings

### "Building failed" on Vercel
- Check `package.json` exists in root
- Verify all dependencies are listed
- Check build logs for specific error

### OCR not working
- Verify `GEMINI_API_KEY` is correct
- Check you haven't exceeded free quota
- Test with a clear, high-quality schedule image

### No buildings in dropdown
- Run `database_schema.sql` again in Supabase
- Check backend logs - buildings should load on startup
- Verify `buildings` table has data

---

## 🎬 Demo Script (For Presentation)

**1. Show the Problem (30 seconds)**
"PNW students drive alone, wasting $30-50/month on gas and parking."

**2. Show the Solution (30 seconds)**
"Pride Share matches students with same classes and routes using AI."

**3. Live Demo (2 minutes)**
- Show QR code: "Students scan this"
- Open signup page
- Fill form with test account
- Upload a schedule screenshot
- Show AI extracting classes
- View matches
- Show cost savings dashboard

**4. Technical Overview (1 minute)**
- Next.js frontend
- FastAPI backend
- Google Gemini for OCR
- Deployed on Railway + Vercel
- All code on GitHub

**5. Impact & Future (30 seconds)**
- Currently X students signed up
- $X saved collectively
- X lbs CO₂ reduced
- Can scale to other universities

---

## 📱 URLs to Memorize

```
Landing Page:  https://prideshare.vercel.app
Signup Page:   https://prideshare.vercel.app/signup
API Docs:      https://your-backend.railway.app/docs
GitHub Repo:   https://github.com/yourusername/prideshare
```

---

## ✅ Pre-Presentation Checklist

Day before presentation:
- [ ] Both sites are live and accessible
- [ ] QR code printed and tested
- [ ] Demo account created with real schedule
- [ ] Screenshots of key features saved
- [ ] Backup video recorded (in case of internet issues)
- [ ] Slide deck includes live demo link
- [ ] Tested on both desktop and mobile
- [ ] Prepared answers for technical questions
- [ ] Have Postman/curl commands ready to show API

Morning of presentation:
- [ ] Check both sites are still live
- [ ] Test QR code with phone
- [ ] Clear browser cache
- [ ] Close unnecessary tabs
- [ ] Check battery/charger
- [ ] Have backup internet (phone hotspot)

---

## 🆘 Emergency Contacts

If something breaks right before presentation:

1. **Frontend down**: Show GitHub code + screenshots
2. **Backend down**: Show API docs + architecture diagram
3. **OCR fails**: Use manual entry demo instead
4. **Database issues**: Show SQL schema + explain design
5. **Total failure**: Use pre-recorded video

---

## 🎉 You're Ready!

Your app is live, tested, and ready for presentation. 

**Good luck! 🚀**

Questions? Check the main README or API docs at `/docs`.
