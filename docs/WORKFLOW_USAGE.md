# Workflow Usage Guide

Complete guide on how to use each workflow in the N8N E-Book Automation system.

## Workflow 1: E-Book Content Generator

### Purpose
Automatically generate complete e-book content using AI (ChatGPT).

### Input Parameters

```json
{
  "topic": "Your e-book topic",
  "wordCount": 10000,
  "niche": "Your niche (Business, Health, Tech, etc.)",
  "tone": "professional|casual|academic|friendly"
}
```

### Usage Example

```bash
curl -X POST http://localhost:5678/webhook/generate-ebook \
  -H "Content-Type: application/json" \
  -d '{
    "topic": "Social Media Marketing for Small Businesses",
    "wordCount": 15000,
    "niche": "Digital Marketing",
    "tone": "professional"
  }'
```

### Output

The workflow generates:
- Complete e-book content in Markdown format
- Chapter-by-chapter structure
- Table of contents
- Marketing copy (description, keywords, categories)

### Expected Time
- Short e-book (5,000 words): 5-10 minutes
- Medium e-book (10,000 words): 10-15 minutes
- Long e-book (20,000+ words): 15-25 minutes

## Workflow 2: E-Book Formatter & Converter

### Purpose
Convert generated content into multiple e-book formats (PDF, EPUB, HTML).

### Input Parameters

```json
{
  "markdownFile": "/path/to/ebook.md",
  "author": "Your Name",
  "formats": ["pdf", "epub"],
  "price": 9.99
}
```

### System Requirements
- `wkhtmltopdf` for PDF generation
- `calibre` for EPUB generation

## Workflow 3: Multi-Platform Distributor

### Purpose
Automatically distribute e-books to multiple platforms.

### Supported Platforms
- Gumroad (automated)
- Amazon KDP (instructions provided)
- Email subscribers (automated)
- Social media (content generated)

## Workflow 4: Sales & Analytics Tracker

### Purpose
Track sales across all platforms and generate daily reports.

### Schedule
Runs automatically every day at 9:00 AM.

### Output
- Google Sheets update
- Email report with analytics
- Revenue tracking

For detailed usage instructions, see the main README.md file.
