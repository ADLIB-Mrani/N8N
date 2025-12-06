# N8N E-Book Automation - Complete Setup Guide

This guide will walk you through setting up the complete e-book automation system from scratch.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [N8N Installation](#n8n-installation)
3. [API Credentials Setup](#api-credentials-setup)
4. [Workflow Import](#workflow-import)
5. [Testing Workflows](#testing-workflows)
6. [Production Deployment](#production-deployment)

## Prerequisites

### System Requirements
- **Operating System:** Linux, macOS, or Windows with WSL
- **Node.js:** Version 16.x or higher
- **RAM:** Minimum 2GB (4GB recommended)
- **Storage:** 10GB free space

### Required Accounts
- OpenAI account with API access (for content generation)
- Gumroad account (for product distribution)
- Email service (SendGrid, SMTP server, or Gmail)
- Google account (for Google Sheets integration)
- Optional: Amazon KDP account

## N8N Installation

### Option 1: Docker (Recommended)

```bash
# Pull N8N Docker image
docker pull n8nio/n8n

# Run N8N with persistent storage
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

Access N8N at: http://localhost:5678

### Option 2: npm (Global Installation)

```bash
# Install N8N globally
npm install n8n -g

# Start N8N
n8n start
```

### Option 3: npx (Quick Test)

```bash
# Run N8N without installation
npx n8n
```

## API Credentials Setup

### 1. OpenAI API Setup

1. Visit https://platform.openai.com/api-keys
2. Create a new API key
3. Copy the key (starts with `sk-...`)

**In N8N:**
- Go to Settings → Credentials
- Click "Add Credential"
- Search for "OpenAI"
- Enter your API key
- Name it "OpenAI API"
- Save

**Pricing Note:** GPT-4 costs ~$0.03 per 1K tokens. Expect $2-5 per e-book generation.

### 2. Gumroad API Setup

1. Go to https://app.gumroad.com/settings/advanced
2. Scroll to "Application" section
3. Copy your Application ID and Secret

**In N8N:**
- Settings → Credentials → Add Credential
- Search for "Gumroad"
- Enter Application ID and Secret
- Name it "Gumroad API"
- Save

### 3. Email/SMTP Setup

**Option A: SendGrid**
1. Create account at https://sendgrid.com
2. Create API key in Settings → API Keys
3. In N8N: Add SendGrid credential with API key

**Option B: Gmail SMTP**
1. Enable 2-factor authentication on Gmail
2. Generate app password: https://myaccount.google.com/apppasswords
3. In N8N: Add SMTP credential
   - Host: smtp.gmail.com
   - Port: 587
   - User: your-email@gmail.com
   - Password: your-app-password
   - Secure: Yes

### 4. Google Sheets Setup

1. Go to https://console.cloud.google.com/
2. Create a new project
3. Enable Google Sheets API
4. Create OAuth 2.0 credentials
5. Download credentials JSON

**In N8N:**
- Settings → Credentials → Add Credential
- Search for "Google Sheets OAuth2"
- Follow OAuth flow to authorize
- Name it "Google Sheets OAuth2 API"

## Workflow Import

### Step 1: Clone Repository

```bash
git clone https://github.com/ADLIB-Mrani/N8N.git
cd N8N
```

### Step 2: Import Workflows

For each workflow file in the `workflows/` folder:

1. Open N8N web interface
2. Click "Workflows" in the left menu
3. Click "Import from File"
4. Select workflow JSON file:
   - `ebook-content-generator.json`
   - `ebook-formatter.json`
   - `ebook-distributor.json`
   - `sales-tracker.json`
5. Click "Import"

### Step 3: Configure Credentials

After importing, open each workflow and:

1. Click on nodes with warning icons
2. Select the appropriate credential from dropdown
3. Match credential names:
   - OpenAI nodes → "OpenAI API"
   - Gumroad nodes → "Gumroad API"
   - Email nodes → Your SMTP/SendGrid credential
   - Google Sheets → "Google Sheets OAuth2 API"
4. Save workflow

## Testing Workflows

### Test 1: Content Generator

1. Open "E-Book Content Generator" workflow
2. Click on "Webhook Trigger" node
3. Copy the webhook URL
4. Use curl or Postman to test:

```bash
curl -X POST https://your-n8n-instance/webhook/generate-ebook \
  -H "Content-Type: application/json" \
  -d '{
    "topic": "Introduction to Digital Marketing",
    "wordCount": 5000,
    "niche": "Business",
    "tone": "professional"
  }'
```

Expected result: JSON response with e-book content and marketing metadata

### Test 2: Formatter

```bash
curl -X POST https://your-n8n-instance/webhook/format-ebook \
  -H "Content-Type: application/json" \
  -d '{
    "markdownFile": "/path/to/generated-ebook.md",
    "author": "Your Name",
    "formats": ["pdf", "epub"]
  }'
```

### Test 3: Distributor

```bash
curl -X POST https://your-n8n-instance/webhook/distribute-ebook \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Introduction to Digital Marketing",
    "description": "A comprehensive guide...",
    "price": 9.99,
    "author": "Your Name",
    "files": {
      "pdf": "/path/to/ebook.pdf",
      "epub": "/path/to/ebook.epub"
    },
    "platforms": ["gumroad", "email"]
  }'
```

### Test 4: Sales Tracker

The sales tracker runs automatically at 9 AM daily. To test manually:

1. Open "E-Book Sales & Analytics Tracker" workflow
2. Click "Execute Workflow" button
3. Check execution log for results
4. Verify Google Sheets update
5. Check email inbox for report

## Production Deployment

### Environment Variables

Create `.env` file in N8N directory:

```env
# N8N Configuration
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=your-secure-password

# Webhook Base URL
WEBHOOK_URL=https://your-domain.com

# Execution Mode
EXECUTIONS_MODE=queue

# Database (for production)
DB_TYPE=postgresdb
DB_POSTGRESDB_HOST=localhost
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_DATABASE=n8n
DB_POSTGRESDB_USER=n8n_user
DB_POSTGRESDB_PASSWORD=your-db-password
```

### Docker Compose (Production)

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:14
    environment:
      POSTGRES_DB: n8n
      POSTGRES_USER: n8n_user
      POSTGRES_PASSWORD: your-db-password
    volumes:
      - postgres-data:/var/lib/postgresql/data
    restart: unless-stopped

  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - DB_TYPE=postgresdb
      - DB_POSTGRESDB_HOST=postgres
      - DB_POSTGRESDB_PORT=5432
      - DB_POSTGRESDB_DATABASE=n8n
      - DB_POSTGRESDB_USER=n8n_user
      - DB_POSTGRESDB_PASSWORD=your-db-password
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=your-secure-password
      - WEBHOOK_URL=https://your-domain.com
    volumes:
      - n8n-data:/home/node/.n8n
    depends_on:
      - postgres
    restart: unless-stopped

volumes:
  postgres-data:
  n8n-data:
```

Start with:
```bash
docker-compose up -d
```

### Reverse Proxy (nginx)

```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:5678;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### SSL Certificate (Let's Encrypt)

```bash
# Install certbot
sudo apt-get install certbot python3-certbot-nginx

# Get certificate
sudo certbot --nginx -d your-domain.com
```

## Maintenance

### Backup Workflows

```bash
# Export all workflows
docker exec -it n8n n8n export:workflow --all --output=/backup/

# Copy from container
docker cp n8n:/backup/ ./n8n-backup/
```

### Monitor Logs

```bash
# Docker logs
docker logs -f n8n

# Check executions
# Access N8N UI → Executions tab
```

### Update N8N

```bash
# Docker
docker pull n8nio/n8n
docker-compose down
docker-compose up -d

# npm
npm update -g n8n
```

## Troubleshooting

### Common Issues

**Issue:** OpenAI API errors
- **Solution:** Check API key validity and account balance

**Issue:** Webhook not accessible
- **Solution:** Check firewall rules, ensure WEBHOOK_URL is correct

**Issue:** Email sending fails
- **Solution:** Verify SMTP credentials, check email service limits

**Issue:** Google Sheets not updating
- **Solution:** Re-authorize OAuth, check sheet permissions

### Get Help

- N8N Community: https://community.n8n.io/
- Documentation: https://docs.n8n.io/
- GitHub Issues: https://github.com/ADLIB-Mrani/N8N/issues

## Next Steps

1. ✅ Complete setup following this guide
2. 🧪 Test all workflows individually
3. 🎨 Customize prompts and templates
4. 📈 Start generating e-books
5. 💰 Monitor sales and optimize
6. 🚀 Scale your e-book business

## Cost Estimation

### Monthly Operating Costs

| Service | Estimated Cost |
|---------|----------------|
| N8N (self-hosted) | $5-20 (VPS) |
| OpenAI API | $50-200 (depends on usage) |
| Gumroad | Free (8.5% + 30¢ per sale) |
| SendGrid | Free (100 emails/day) |
| Domain + SSL | $10-15 |
| **Total** | **$65-235/month** |

### Break-even Analysis

If selling e-books at $9.99 each:
- Need ~7-24 sales/month to break even
- Each additional sale is profit
- Potential: $500-5000+/month with consistent production

---

**Ready to make money with automation? Start generating your first e-book now!** 🚀
