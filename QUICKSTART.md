# Quick Start Guide - Get Your First E-Book in 30 Minutes

This is the fastest way to get started with the N8N E-Book Automation system and generate your first e-book.

## ⚡ Speed Setup (10 minutes)

### Step 1: Install N8N (2 minutes)

**Option A - Docker (Recommended):**
```bash
docker run -it --rm --name n8n -p 5678:5678 n8nio/n8n
```

**Option B - npx (No installation):**
```bash
npx n8n
```

Access: http://localhost:5678

### Step 2: Get OpenAI API Key (3 minutes)

1. Go to https://platform.openai.com/api-keys
2. Create account (if needed)
3. Click "Create new secret key"
4. Copy key (starts with `sk-...`)
5. Add $5-10 credit to your account

### Step 3: Import First Workflow (5 minutes)

1. Download or clone this repo
2. In N8N, click "Workflows" → "Import from File"
3. Select `workflows/ebook-content-generator.json`
4. Click on "Generate Outline (ChatGPT)" node
5. Add Credential → OpenAI
6. Paste your API key
7. Click "Save"
8. Click on "Generate Chapter Content" node
9. Select the same OpenAI credential
10. Save workflow

## 🚀 Generate Your First E-Book (20 minutes)

### Step 1: Choose Your Topic (2 minutes)

Pick something you know about or that's profitable:
- **Digital Marketing for Beginners**
- **Passive Income Strategies**
- **Healthy Meal Prep**
- **Time Management Hacks**
- **Python Programming Basics**

### Step 2: Run the Workflow (15 minutes)

1. In N8N, open "E-Book Content Generator" workflow
2. Click "Execute Workflow" button
3. In the "Webhook Trigger" node, click "Listen for Test Event"
4. Copy the webhook URL

5. Open a new terminal and run:

```bash
curl -X POST YOUR_WEBHOOK_URL_HERE \
  -H "Content-Type: application/json" \
  -d '{
    "topic": "Digital Marketing for Small Businesses",
    "wordCount": 8000,
    "niche": "Business",
    "tone": "professional"
  }'
```

**Replace `YOUR_WEBHOOK_URL_HERE` with the actual URL from step 4**

6. Wait 10-15 minutes while N8N generates your e-book
7. Watch the execution progress in N8N interface
8. Download the generated markdown file

### Step 3: Review Your E-Book (3 minutes)

Your e-book includes:
- ✅ Complete title and structure
- ✅ 8-12 chapters with full content
- ✅ Table of contents
- ✅ Professional formatting
- ✅ Marketing copy (description, keywords)

## 🎨 Quick Formatting (Optional - 5 minutes)

Want PDF/EPUB? Install these tools:

**macOS:**
```bash
brew install wkhtmltopdf calibre
```

**Ubuntu/Debian:**
```bash
sudo apt-get install wkhtmltopdf calibre
```

Then use the formatter workflow the same way!

## 💰 Your First Sale (Same Day)

### 1. Create Free Gumroad Account (5 minutes)
- Go to https://gumroad.com
- Sign up
- Verify email

### 2. Upload Your E-Book (5 minutes)
- Click "Create Product"
- Upload your PDF
- Set price: $9.99
- Add description (use the generated marketing copy!)
- Publish

### 3. Share Your Link (5 minutes)
- Copy product URL
- Share on:
  - Twitter/X
  - Facebook groups
  - Reddit (relevant subreddits)
  - Your email signature
  - LinkedIn

### 4. Wait for Sales! 💰

First sale typically within 24-48 hours if shared properly.

## 📈 Scale to 10 E-Books (This Week)

**Day 1:** Generate 2 e-books (topics in same niche)
**Day 2:** Format and publish on Gumroad
**Day 3:** Generate 2 more e-books
**Day 4:** Format and publish
**Day 5:** Generate 2 more e-books
**Day 6:** Format and publish
**Day 7:** Create bundle offer (6 e-books for $39.99)

**Expected Results:** 10-30 sales in first week = $99-300

## 🎯 Common First-Time Mistakes to Avoid

❌ **Don't:** Generate 50,000 word e-books on first try
✅ **Do:** Start with 5,000-10,000 words

❌ **Don't:** Pick oversaturated topics like "weight loss"
✅ **Do:** Pick specific niches like "weight loss for new moms"

❌ **Don't:** Publish without reviewing AI content
✅ **Do:** Read and edit for accuracy

❌ **Don't:** Set price too low ($0.99)
✅ **Do:** Start at $7.99-9.99, test pricing

❌ **Don't:** Wait for perfection
✅ **Do:** Publish and iterate

## 🔥 Hot Topics to Start With (Tested & Proven)

1. **"ChatGPT Prompts for [Your Profession]"** - Very trendy
2. **"Passive Income with [Platform]"** - High demand
3. **"Beginner's Guide to [Skill]"** - Evergreen
4. **"30-Day [Habit] Challenge"** - Action-oriented
5. **"Complete [Tool/Software] Guide"** - Practical

## 💡 Pro Tips

1. **Title is Everything:** Spend time on a compelling title
2. **Cover Matters:** Use Canva free templates
3. **Share Everywhere:** Reddit, Twitter, Facebook groups
4. **Get Reviews Fast:** Give free copies to 5-10 friends
5. **Track Everything:** Use the sales tracker workflow

## 🆘 Troubleshooting

**Problem:** Workflow times out
- **Fix:** Reduce wordCount to 5000

**Problem:** OpenAI API error
- **Fix:** Check API key and account balance

**Problem:** Poor content quality
- **Fix:** Be more specific in topic, add more context

**Problem:** No sales
- **Fix:** Improve title, lower price temporarily, share more

## 📚 What's Next?

After your first e-book:
1. ✅ Set up the formatter workflow
2. ✅ Import the distributor workflow
3. ✅ Set up sales tracking
4. ✅ Read full SETUP_GUIDE.md
5. ✅ Check MONETIZATION_GUIDE.md for strategies
6. ✅ Join e-book creator communities

## 🎥 Video Tutorial

Watch the complete tutorial: https://youtu.be/5CudnzjAf2I

## 🤑 Your 30-Day Goal

- **Week 1:** 1 e-book, first sale
- **Week 2:** 5 e-books, $100 revenue
- **Week 3:** 10 e-books, $300 revenue  
- **Week 4:** 15 e-books, $500+ revenue

**This is achievable with 1-2 hours per day!**

## ⚡ Ready? Start Now!

1. Install N8N
2. Get OpenAI key
3. Import workflow
4. Generate e-book
5. Publish on Gumroad
6. Make money!

---

**Questions?** Open an issue on GitHub or check the full documentation.

**Success story?** Share it! Tag @ADLIB-Mrani

🚀 **Time to turn automation into income!** 🚀
