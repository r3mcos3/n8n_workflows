# Gmail Organizer - Auto Label Emails (AI)

Automatically categorize and label incoming Gmail emails using AI-powered classification with OpenAI GPT-4o-mini. The AI is fully autonomous - it creates new labels on-the-fly based on email content.

## Features

- **Fully autonomous AI categorization** - AI chooses the best category, no fixed list
- **Dynamic label creation** - new labels are created automatically when needed
- **Context-aware** - AI sees existing Gmail labels and reuses them when appropriate
- **Smart normalization** - consistent Title Case formatting for all labels
- Automatically labels new unread emails
- Runs every minute to process new emails
- Low cost: ~$0.0001 per email (GPT-4o-mini)

## How It Works

The AI receives:
1. Email details (from, subject, preview)
2. List of existing Gmail labels

Based on this context, the AI decides:
- Use an existing label if it fits
- Create a new descriptive label if no existing label matches

**Example:** A Bol.com order confirmation might get labeled "Shopping" or "Orders" - the AI decides based on what makes sense.

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

## Example Categories

The AI might create labels like:

| Category | Example Emails |
|----------|----------------|
| **Work** | GitHub, Slack, Jira, Zoom, colleagues |
| **Newsletters** | Subscriptions, digests, marketing |
| **Social Media** | Facebook, Twitter/X, LinkedIn, YouTube |
| **Finance** | Banks, payments, invoices, receipts |
| **Shopping** | Order confirmations, shipping updates |
| **Travel** | Flight bookings, hotel reservations |
| **Health** | Doctor appointments, pharmacy |
| **Government** | Tax office, municipality, official documents |
| **Education** | Courses, certifications, learning platforms |
| **Subscriptions** | Streaming services, software licenses |

The AI is not limited to these - it will create whatever category fits best.

## Requirements

- Gmail OAuth2 API credentials configured in n8n
- **OpenAI API credentials** configured in n8n
- Gmail account with API access enabled

## Installation

1. Import `gmail-organizer-auto-label.json` into n8n
2. Connect your **Gmail OAuth2 credentials** to all Gmail nodes
3. Connect your **OpenAI API credentials** to the "AI Categorize" node
4. Activate the workflow

That's it! Labels will be created automatically as emails arrive.

## Configuration

### AI Model Settings

| Setting | Value | Description |
|---------|-------|-------------|
| Model | gpt-4o-mini | Fast and cost-effective |
| Temperature | 0.1 | Low for consistent categorization |
| Max Tokens | 50 | Room for multi-word categories |

### Customizing AI Behavior

Edit the prompt in the "Prepare AI Prompt" Code node to:

- Suggest specific categories you prefer
- Add rules for certain senders or subjects
- Change the language of category names

Example: Preferring Dutch category names:
```javascript
// In the prompt, change:
// "create a NEW short category name (1-3 words, English)"
// to:
// "create a NEW short category name (1-3 words, Dutch)"
```

## Files

| File | Description |
|------|-------------|
| `gmail-organizer-auto-label.json` | Main AI-powered workflow with autonomous categorization |

## Cost Estimation

Using GPT-4o-mini:
- ~200 input tokens per email (includes existing labels)
- ~10 output tokens per email
- Cost: ~$0.0001 per email
- 1000 emails/month = $0.10

## Troubleshooting

### Emails Not Being Labeled
- Check if the workflow is active
- Verify Gmail credentials are working
- Verify OpenAI credentials are configured
- Check the execution logs for errors

### Too Many Different Labels
The AI creates specific labels. If you prefer fewer, broader categories:
1. Edit the prompt to encourage reusing existing labels
2. Add a line like: "Prefer using existing labels over creating new ones"

### Label Names Are Inconsistent
All labels are normalized to Title Case (e.g., "shopping" becomes "Shopping"). If you see duplicates:
- Check for leading/trailing spaces in AI responses
- The case-insensitive matching should prevent most duplicates

### OpenAI API Errors
- Verify your OpenAI API key is valid
- Check if you have sufficient API credits
- Ensure the API key has access to GPT-4o-mini

### Label Creation Fails
- Verify Gmail credentials have permission to create labels
- Check if a label with a similar name already exists
- Review execution logs for specific error messages
