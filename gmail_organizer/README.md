# Gmail Organizer - Auto Label Emails (AI)

Automatically categorize and label incoming Gmail emails using AI-powered classification with OpenAI GPT-4o-mini. Labels are created automatically if they don't exist.

## Features

- **AI-powered categorization** using OpenAI GPT-4o-mini for intelligent email classification
- **Auto-create labels** - labels are created on-the-fly if they don't exist
- Automatically labels new unread emails
- Categorizes emails into 6 categories: Work, Newsletters, Social Media, Finance, Personal, To Review
- Runs every minute to process new emails
- Dynamically fetches label IDs (no hardcoded values)
- Low cost: ~$0.0001 per email (GPT-4o-mini)

## Workflow Diagram

```
Gmail Trigger → Get Labels → Prepare Prompt → AI Categorize → Find or Create Label
(new unread)    (fetch IDs)   (build prompt)   (GPT-4o-mini)   (check existence)
                                                                      │
                                         ┌────────────────────────────┴────────────────────────────┐
                                         │                                                         │
                                         ▼                                                         ▼
                                  [Label Exists]                                          [Label Missing]
                                         │                                                         │
                                         ▼                                                         ▼
                                 Use Existing Label                                         Create Label
                                         │                                                         │
                                         │                                                         ▼
                                         │                                                Use Created Label
                                         │                                                         │
                                         └─────────────────────┬───────────────────────────────────┘
                                                               │
                                                               ▼
                                                      Add Label to Email
```

## Categories

The AI categorizes emails based on context, not just keywords:

| Category | Description |
|----------|-------------|
| **Work** | Professional emails, work tools (Slack, GitHub, Jira, Zoom), colleagues, business communications |
| **Newsletters** | Subscriptions, digests, marketing emails, promotional content |
| **Social Media** | Facebook, Twitter/X, LinkedIn, Instagram, YouTube, Discord notifications |
| **Finance** | Banks, payments, invoices, receipts, subscriptions, financial services |
| **Personal** | Emails from friends, family, personal contacts |
| **To Review** | Cannot determine category or doesn't fit others |

## Requirements

- Gmail OAuth2 API credentials configured in n8n
- **OpenAI API credentials** configured in n8n
- Gmail account with API access enabled

## Installation

1. Import `gmail-organizer-auto-label.json` into n8n
2. Connect your **Gmail OAuth2 credentials** to all Gmail nodes
3. Connect your **OpenAI API credentials** to the "AI Categorize" node
4. Activate the workflow

That's it! Labels will be created automatically when needed.

## Configuration

### AI Model Settings

The "AI Categorize" node uses these settings for optimal performance:

| Setting | Value | Description |
|---------|-------|-------------|
| Model | gpt-4o-mini | Fast and cost-effective |
| Temperature | 0.1 | Low for consistent categorization |
| Max Tokens | 20 | Only need category name |

### Customizing Categories

To modify the AI's categorization behavior, edit the prompt in the "Prepare AI Prompt" Code node. You can:

- Add new categories
- Modify category definitions
- Add specific rules for your use case

Example: Adding a "Shopping" category:
```javascript
// In the prompt, add:
- Shopping: Online stores, order confirmations, shipping notifications, retail promotions
```

New labels will be created automatically when the AI categorizes an email into a new category.

## Files

| File | Description |
|------|-------------|
| `gmail-organizer-auto-label.json` | Main AI-powered workflow that auto-labels emails and creates missing labels |

## Cost Estimation

Using GPT-4o-mini:
- ~150 input tokens per email
- ~5 output tokens per email
- Cost: ~$0.0001 per email
- 1000 emails/month ≈ $0.10

## Troubleshooting

### Emails Not Being Labeled
- Check if the workflow is active
- Verify Gmail credentials are working
- Verify OpenAI credentials are configured
- Check the execution logs for errors

### Wrong Category Assignment
The AI learns from context. If categorization is consistently wrong:
1. Check the prompt in "Prepare AI Prompt" node
2. Add more specific definitions for your categories
3. Consider adding example emails to the prompt

### OpenAI API Errors
- Verify your OpenAI API key is valid
- Check if you have sufficient API credits
- Ensure the API key has access to GPT-4o-mini

### Label Creation Fails
- Verify Gmail credentials have permission to create labels
- Check if a label with a similar name already exists
- Review execution logs for specific error messages
