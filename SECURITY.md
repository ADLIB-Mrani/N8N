# Security Considerations

## Overview

This document outlines the security measures implemented in the N8N E-Book Automation system and best practices for secure usage.

## Security Features Implemented

### 1. Input Sanitization

**Command Injection Prevention:**
- All user inputs that are passed to shell commands are sanitized
- Filenames are restricted to alphanumeric characters, hyphens, and underscores
- Special characters are removed or escaped before command execution

**Example (ebook-formatter.json):**
```javascript
// Before: Direct interpolation (vulnerable)
"{{ $json.baseFilename }}.pdf"

// After: Sanitized (secure)
"{{ $json.baseFilename.replace(/[^a-zA-Z0-9_-]/g, '_') }}.pdf"
```

### 2. XSS Protection

**HTML Content Escaping:**
- All user-provided content displayed in HTML emails is properly escaped
- Special HTML characters are converted to their entity equivalents
- Prevents malicious scripts from being injected

**Example (ebook-distributor.json):**
```javascript
function escapeHtml(text) {
  return String(text)
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#039;');
}
```

### 3. Input Validation

**Required Fields:**
- All workflows validate required inputs before processing
- Missing or invalid inputs result in clear error messages
- Type checking for numeric values (prices, word counts)

**Edge Case Handling:**
- Empty titles generate fallback values
- Null/undefined values are handled gracefully
- Maximum length limits prevent abuse

### 4. Environment Variables

**Sensitive Data Protection:**
- API keys and credentials stored in environment variables
- `.gitignore` excludes sensitive files from version control
- Example `.env` file provided (no actual credentials)

**Configuration:**
- Google Sheet IDs configurable via environment variables
- Webhook URLs externalized
- Database credentials in environment

## User Security Responsibilities

### API Key Management

**DO:**
- ✅ Store API keys in environment variables
- ✅ Use restricted API keys with minimal permissions
- ✅ Rotate keys regularly (every 90 days)
- ✅ Monitor API usage for anomalies

**DON'T:**
- ❌ Commit API keys to version control
- ❌ Share API keys in public forums
- ❌ Use root/admin API keys
- ❌ Reuse keys across projects

### N8N Instance Security

**Authentication:**
- Enable N8N basic authentication in production
- Use strong, unique passwords
- Consider additional authentication layers (OAuth, SSO)

**Network Security:**
- Run N8N behind reverse proxy (nginx, Caddy)
- Enable HTTPS with valid SSL certificates
- Restrict access by IP if possible
- Use firewall rules to limit exposure

**Example nginx configuration:**
```nginx
server {
    listen 443 ssl http2;
    server_name n8n.yourdomain.com;
    
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    
    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    
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

### Content Security

**AI-Generated Content:**
- Review all AI-generated content before publishing
- Verify facts and statistics
- Remove any potentially harmful or misleading information
- Ensure compliance with platform policies

**Copyright Considerations:**
- Don't train on copyrighted material without permission
- Add original insights and examples
- Disclose AI usage where required
- Respect intellectual property rights

## Data Privacy

### User Data

**What We Collect:**
- E-book metadata (titles, descriptions, keywords)
- Sales data from integrated platforms
- Email addresses (if using email distribution)

**What We Don't Collect:**
- Payment information (handled by platforms)
- Personal identification beyond what's necessary
- Browsing history or tracking data

**Data Storage:**
- N8N data stored locally or in your database
- Google Sheets data in your Google account
- Platform data (Gumroad, Amazon) on their servers

### GDPR Compliance

If serving EU customers:
- Provide clear privacy policy
- Allow users to request data deletion
- Document data processing activities
- Obtain consent for email marketing

## Vulnerability Reporting

### How to Report

If you discover a security vulnerability:

1. **DO NOT** open a public GitHub issue
2. Email security details to: [Your security email]
3. Include:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

### Response Timeline

- **24 hours**: Acknowledgment of report
- **7 days**: Initial assessment and response
- **30 days**: Fix developed and tested
- **Public disclosure**: After fix is deployed

## Security Checklist

### Initial Setup
- [ ] Change default N8N credentials
- [ ] Enable HTTPS
- [ ] Configure firewall rules
- [ ] Set up API key rotation
- [ ] Review and customize workflows
- [ ] Test input validation
- [ ] Enable logging

### Regular Maintenance
- [ ] Update N8N (monthly)
- [ ] Rotate API keys (quarterly)
- [ ] Review access logs (weekly)
- [ ] Audit workflows (monthly)
- [ ] Backup data (daily)
- [ ] Test disaster recovery (quarterly)

### Before Publishing E-Books
- [ ] Review AI-generated content
- [ ] Verify facts and statistics
- [ ] Check for plagiarism
- [ ] Test all download links
- [ ] Verify pricing and metadata
- [ ] Review platform terms of service

## Known Limitations

### Current Limitations

1. **Manual Amazon KDP Upload**: No public API available
2. **Email Rate Limits**: Depends on SMTP provider
3. **API Costs**: OpenAI charges per token
4. **No Built-in Encryption**: Use at database level if needed

### Mitigations

1. Provide clear manual instructions for Amazon
2. Implement rate limiting in workflows
3. Monitor and set API budget limits
4. Use encrypted databases (PostgreSQL with encryption)

## Best Practices

### For Developers

1. **Code Reviews**: All workflow changes should be reviewed
2. **Testing**: Test with malicious inputs
3. **Updates**: Keep dependencies updated
4. **Documentation**: Document security decisions

### For Users

1. **Principle of Least Privilege**: Grant minimal permissions
2. **Defense in Depth**: Multiple security layers
3. **Regular Audits**: Review workflows and credentials
4. **Incident Response**: Have a plan for breaches

## Compliance

### Platforms

**Gumroad:**
- Follow Gumroad's Terms of Service
- Comply with payment processing regulations
- Respect customer data privacy

**Amazon KDP:**
- Adhere to KDP content guidelines
- Follow royalty and pricing rules
- Maintain content quality standards

**OpenAI:**
- Follow OpenAI usage policies
- Don't use for harmful content
- Respect rate limits and fair use

### Legal Requirements

Depending on your jurisdiction:
- Business registration
- Tax compliance
- Consumer protection laws
- Data protection regulations
- Copyright and trademark law

## Resources

- [N8N Security Best Practices](https://docs.n8n.io/hosting/security/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OpenAI Safety Guidelines](https://openai.com/policies/usage-policies)
- [GDPR Compliance](https://gdpr.eu/)

## Updates

This security document is reviewed and updated quarterly. Last updated: 2024-12-06

---

**Security is a shared responsibility. Stay vigilant and follow best practices!**
