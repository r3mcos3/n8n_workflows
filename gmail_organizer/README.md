# Gmail Organizer - Auto Label Emails

Automatically categorize and label incoming Gmail emails based on sender and subject patterns.

## Features

- Automatically labels new unread emails
- Categorizes emails into 6 categories: Work, Newsletters, Social Media, Finance, Personal, To Review
- Runs every minute to process new emails
- Dynamically fetches label IDs (no hardcoded values)
- Includes setup workflow to create required labels

## Workflow Diagram

### Setup Workflow (Run Once)
```
Manual Trigger → Get Existing Labels → Check Missing → Filter → Create Label
```

### Main Organizer Workflow
```
Gmail Trigger → Get All Labels → Categorize Email → Add Label to Email
(new unread)     (fetch IDs)      (Code node)        (apply label)
```

## Categories and Detection Patterns

| Category | Label | Detection Patterns |
|----------|-------|-------------------|
| Work | Work | slack.com, notion.so, jira, github, zoom, teams, asana, monday.com |
| Newsletters | Newsletters | newsletter, digest, weekly, substack, mailchimp, unsubscribe |
| Social Media | Social Media | facebook, twitter, linkedin, instagram, youtube, discord, telegram |
| Finance | Finance | bank, paypal, stripe, invoice, payment, receipt, billing |
| Personal | Personal | gmail.com, outlook.com, hotmail.com, yahoo.com, icloud.com |
| Other | To Review | Everything that doesn't match any pattern |

## Requirements

- Gmail OAuth2 API credentials configured in n8n
- Gmail account with API access enabled

## Installation

### Step 1: Import the Setup Workflow
1. Import `gmail-labels-setup.json` into n8n
2. Connect your Gmail OAuth2 credentials to the Gmail nodes
3. Execute the workflow once to create the required labels

### Step 2: Import the Main Workflow
1. Import `gmail-organizer-auto-label.json` into n8n
2. Connect your Gmail OAuth2 credentials to all Gmail nodes
3. Activate the workflow

## Configuration

### Adding Custom Patterns

Edit the `Categorize Email` Code node to add custom patterns:

```javascript
const rules = {
  work: [
    'slack.com', 'notion.so', // ... existing patterns
    'your-company.com',       // Add your company domain
    'custom-tool.io'          // Add custom work tools
  ],
  // ... other categories
};
```

### Adding New Categories

1. Add the new label name to the setup workflow's `requiredLabels` array
2. Add the new category patterns to the `rules` object
3. Add the mapping in `labelMapping`
4. Re-run the setup workflow to create the new label

## Files

| File | Description |
|------|-------------|
| `gmail-labels-setup.json` | One-time setup workflow to create Gmail labels |
| `gmail-organizer-auto-label.json` | Main workflow that auto-labels incoming emails |

## Troubleshooting

### "Label not found" Error
Run the `Gmail Labels Setup` workflow first to create all required labels.

### Emails Not Being Labeled
- Check if the workflow is active
- Verify Gmail credentials are working
- Check the execution logs for errors

### Wrong Category Assignment
Edit the patterns in the `Categorize Email` Code node to better match your email sources.
