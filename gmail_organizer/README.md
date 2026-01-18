# Gmail Organizer - Auto Label Emails (AI)

Automatically categorize and label incoming Gmail emails using AI-powered classification with OpenAI GPT-4o-mini.

## Features

- **AI-powered categorization** using OpenAI GPT-4o-mini for intelligent email classification
- Automatically labels new unread emails
- Categorizes emails into 6 categories: Work, Newsletters, Social Media, Finance, Personal, To Review
- Runs every minute to process new emails
- Dynamically fetches label IDs (no hardcoded values)
- Includes setup workflow to create required labels
- Low cost: ~$0.0001 per email (GPT-4o-mini)

## Workflow Diagram

### Setup Workflow (Run Once)
```
Manual Trigger → Get Existing Labels → Check Missing → Filter → Create Label
```

### Main Organizer Workflow (AI-Powered)
```
Gmail Trigger → Get Labels → Prepare Prompt → AI Categorize → Map Label → Add Label
(new unread)    (fetch IDs)   (build prompt)   (GPT-4o-mini)   (find ID)   (apply)
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

### Step 1: Import the Setup Workflow
1. Import `gmail-labels-setup.json` into n8n
2. Connect your Gmail OAuth2 credentials to the Gmail nodes
3. Execute the workflow once to create the required labels

### Step 2: Import the Main Workflow
1. Import `gmail-organizer-auto-label.json` into n8n
2. Connect your **Gmail OAuth2 credentials** to all Gmail nodes
3. Connect your **OpenAI API credentials** to the "AI Categorize" node
4. Activate the workflow

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

Then run the setup workflow to create the new label.

## Files

| File | Description |
|------|-------------|
| `gmail-labels-setup.json` | One-time setup workflow to create Gmail labels |
| `gmail-organizer-auto-label.json` | Main AI-powered workflow that auto-labels emails |

## Cost Estimation

Using GPT-4o-mini:
- ~150 input tokens per email
- ~5 output tokens per email
- Cost: ~$0.0001 per email
- 1000 emails/month ≈ $0.10

## Troubleshooting

### "Label not found" Error
Run the `Gmail Labels Setup` workflow first to create all required labels.

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
