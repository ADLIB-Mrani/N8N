# Contributing to N8N E-Book Automation

Thank you for your interest in contributing! This document provides guidelines for contributing to this project.

## How to Contribute

### Reporting Issues

**Bug Reports:**
- Check if the issue already exists
- Use a clear, descriptive title
- Include steps to reproduce
- Describe expected vs actual behavior
- Include N8N version and environment details
- Add screenshots if applicable

**Feature Requests:**
- Describe the feature and its benefits
- Explain use cases
- Consider alternative solutions
- Be open to feedback

### Pull Requests

**Before Submitting:**
1. Fork the repository
2. Create a new branch: `git checkout -b feature/your-feature-name`
3. Make your changes
4. Test thoroughly
5. Update documentation
6. Commit with clear messages

**PR Guidelines:**
- One feature/fix per PR
- Include tests if applicable
- Update relevant documentation
- Follow existing code style
- Reference related issues

**Commit Messages:**
```
feat: Add new workflow for social media posting
fix: Resolve command injection vulnerability in formatter
docs: Update setup guide with Docker instructions
refactor: Simplify email template generation
```

## Development Setup

### Prerequisites
- Node.js 16+
- N8N installed
- Git
- Text editor (VS Code recommended)

### Local Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/N8N.git
cd N8N

# Add upstream remote
git remote add upstream https://github.com/ADLIB-Mrani/N8N.git

# Create branch for your changes
git checkout -b feature/your-feature

# Make changes and test
# ...

# Commit and push
git add .
git commit -m "feat: Your feature description"
git push origin feature/your-feature
```

## Workflow Development

### Adding New Workflows

1. **Create Workflow in N8N:**
   - Design and test in N8N interface
   - Use clear node names
   - Add helpful notes to nodes
   - Test with various inputs

2. **Export Workflow:**
   - File → Export
   - Save to `workflows/` directory
   - Use descriptive filename: `workflow-name.json`

3. **Document Workflow:**
   - Add usage instructions to `docs/WORKFLOW_USAGE.md`
   - Include example API calls
   - List prerequisites
   - Explain configuration

4. **Test Workflow:**
   - Test with valid inputs
   - Test with invalid inputs
   - Test edge cases
   - Verify error handling

### Workflow Best Practices

**Security:**
- Sanitize all user inputs
- Use environment variables for credentials
- Escape HTML content
- Validate data types

**Performance:**
- Minimize API calls
- Use batching where possible
- Implement caching if appropriate
- Consider rate limits

**Usability:**
- Clear error messages
- Helpful node descriptions
- Sensible default values
- Progressive disclosure

## Documentation

### Documentation Standards

**README Updates:**
- Keep features list current
- Update prerequisites if needed
- Add new workflows to list
- Include version compatibility

**Guide Updates:**
- Update relevant guides when changing workflows
- Include new examples
- Explain breaking changes
- Keep screenshots current

**Code Comments:**
- Explain complex logic
- Document assumptions
- Note security considerations
- Reference issues/PRs

## Testing

### Manual Testing

**Workflow Testing:**
1. Import workflow into clean N8N instance
2. Configure with test credentials
3. Execute with sample data
4. Verify output
5. Test error conditions

**Integration Testing:**
1. Test workflow chains
2. Verify data passing between workflows
3. Check platform integrations
4. Validate formatting/output

### Test Scenarios

**Content Generator:**
- Short e-book (5,000 words)
- Long e-book (20,000 words)
- Various niches
- Different tones
- Edge case topics

**Formatter:**
- Markdown with special characters
- Very long titles
- Missing metadata
- Various formats
- Large files

**Distributor:**
- Single platform
- Multiple platforms
- Invalid credentials
- Network errors
- Rate limiting

**Sales Tracker:**
- No sales data
- Large datasets
- Missing API keys
- Invalid dates
- Export failures

## Code Style

### JSON Workflows

```json
{
  "name": "Descriptive Workflow Name",
  "nodes": [
    {
      "parameters": {
        "field": "value"
      },
      "id": "descriptive-id",
      "name": "Clear Node Name",
      "type": "n8n-nodes-base.nodeName",
      "position": [x, y]
    }
  ]
}
```

### JavaScript in Code Nodes

```javascript
// Use clear variable names
const userInput = $input.first().json;

// Add error handling
try {
  // Process data
  const result = processData(userInput);
  return { json: result };
} catch (error) {
  throw new Error(`Processing failed: ${error.message}`);
}

// Sanitize inputs
function sanitize(text) {
  return String(text).replace(/[^a-zA-Z0-9_-]/g, '_');
}
```

### Markdown Documentation

```markdown
# Main Heading

## Section Heading

### Subsection

**Bold** for emphasis
*Italic* for terms
`code` for commands/values

- List item
- List item

1. Numbered item
2. Numbered item
```

## Areas for Contribution

### High Priority

- [ ] Add support for more e-book formats (AZW3, etc.)
- [ ] Implement Amazon KDP API integration
- [ ] Add automated cover generation
- [ ] Create batch processing workflow
- [ ] Add A/B testing for pricing
- [ ] Implement affiliate link insertion

### Medium Priority

- [ ] Support for more AI models (Claude, Gemini)
- [ ] Advanced formatting templates
- [ ] Multi-language support
- [ ] SEO optimization automation
- [ ] Social media scheduling
- [ ] Advanced analytics dashboard

### Documentation

- [ ] Video tutorials for each workflow
- [ ] Troubleshooting database
- [ ] Case study collection
- [ ] Translation to other languages
- [ ] FAQ section
- [ ] Comparison with alternatives

### Community

- [ ] Discord server setup
- [ ] Monthly community calls
- [ ] Showcase successful e-books
- [ ] Template library
- [ ] Plugin/extension system

## Community Guidelines

### Code of Conduct

**Be Respectful:**
- Treat everyone with respect
- Welcome newcomers
- Accept constructive criticism
- Focus on the issue, not the person

**Be Collaborative:**
- Share knowledge
- Help others
- Provide feedback
- Credit contributors

**Be Professional:**
- Use appropriate language
- Stay on topic
- Respect different opinions
- Follow project guidelines

### Communication Channels

- **GitHub Issues**: Bug reports, feature requests
- **GitHub Discussions**: Questions, ideas, show & tell
- **Pull Requests**: Code contributions
- **Discord** (coming soon): Real-time chat

## Recognition

### Contributors

All contributors will be:
- Listed in CONTRIBUTORS.md
- Credited in release notes
- Mentioned in project README
- Eligible for special roles/badges

### Types of Contributions

- 💻 Code contributions
- 📖 Documentation improvements
- 🐛 Bug reports
- 💡 Feature suggestions
- 🎨 Design/UX improvements
- 🌍 Translations
- 📹 Videos/tutorials
- 💬 Community support

## Release Process

### Versioning

We use Semantic Versioning (SemVer):
- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes

Example: `v1.2.3`

### Release Checklist

Before release:
- [ ] All tests pass
- [ ] Documentation updated
- [ ] CHANGELOG updated
- [ ] Version bumped
- [ ] Security review completed
- [ ] Breaking changes documented

## Questions?

- Check existing issues/discussions
- Review documentation
- Ask in GitHub Discussions
- Tag maintainers if urgent

## Thank You!

Your contributions make this project better for everyone. Whether you're fixing a typo or adding a major feature, every contribution is valuable!

---

**Happy contributing!** 🎉
