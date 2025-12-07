# Example N8N Workflows

This directory contains additional example workflows inspired by real-world automation use cases. These examples complement the e-book automation workflows and demonstrate N8N's versatility.

## Included Examples

### 1. Daily Hacker News Summary (`hackernews-ai-summary.json`)
**Purpose:** Receive a daily email with AI-filtered and summarized tech news

**What it does:**
- Fetches latest articles from Hacker News API
- Filters articles by score and relevance
- Uses OpenAI to summarize each article
- Sends formatted email digest every morning

**Use Case:** Stay informed about tech trends without spending hours reading

### 2. Local Email Classifier (`email-classifier-mistral.json`)
**Purpose:** Classify personal emails using privacy-focused local AI

**What it does:**
- Connects to your email (IMAP)
- Uses local Mistral LLM to classify emails
- Categories: Important, Spam, Newsletter, Personal, Work
- No data sent to external services (privacy-first)

**Use Case:** Automatic email organization without compromising privacy

### 3. AI Personal Assistant (`ai-assistant-calendar-email.json`)
**Purpose:** Interact with an AI assistant that manages your calendar and emails

**What it does:**
- Chat interface for natural language commands
- Reads and manages Google Calendar
- Reads and responds to emails
- Provides intelligent summaries and suggestions

**Use Case:** "Schedule a meeting with John next week" or "What's on my calendar today?"

## Privacy & Local AI

**Important Note:** Example 2 (Email Classifier) uses **local Mistral LLM** to keep your data private:
- No data sent to OpenAI or other cloud services
- Runs entirely on your server
- Free to use (open source model)
- Slower but fully private

This demonstrates that you can build powerful AI automations without compromising privacy.

## Setup Instructions

1. Import the desired workflow into N8N
2. Configure credentials (see each workflow's documentation)
3. For local Mistral: Install Ollama and pull Mistral model
4. Test the workflow with sample data
5. Activate for production use

## Customization

These workflows are templates - customize them for your needs:
- Change news sources (Reddit, Product Hunt, etc.)
- Add more email categories
- Extend AI assistant capabilities
- Integrate with other services (Slack, Notion, etc.)

## Learning Resources

These examples are based on comprehensive N8N training demonstrating:
- API integrations
- AI/LLM usage (cloud and local)
- Email automation
- Calendar management
- Privacy-focused solutions

## Contributing

Have a useful workflow example? Submit a PR with:
- The workflow JSON file
- Clear documentation
- Use case description
- Setup instructions
