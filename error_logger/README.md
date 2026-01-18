# Error Logger

Centralized error logging workflow that captures all n8n workflow errors, logs them to Google Sheets, and sends email notifications.

## Features

- Catches errors from any workflow in your n8n instance
- Logs error details to Google Sheets for tracking and analysis
- Sends email notifications with error details
- Includes execution URL for quick debugging

## Workflow Diagram

```
Error Trigger ──┬──► Append row in sheet (Google Sheets)
                │
                └──► Send a message (Gmail notification)
```

## Logged Information

Each error is logged with the following details:

| Field | Description |
|-------|-------------|
| Time | Timestamp when the error occurred (dd-MM-yyyy HH:MM) |
| Workflow | Name of the workflow that failed |
| URL | Direct link to the failed execution |
| Node | Name of the node that caused the error |
| Error Message | The actual error message |

## Requirements

- Google Sheets OAuth2 API credentials
- Gmail OAuth2 API credentials
- A Google Sheet with the following columns: Time, Workflow, URL, Node, Error Message

## Installation

1. Import `error_logger.json` into n8n
2. Create a Google Sheet with columns: `Time`, `Workflow`, `URL`, `Node`, `Error Message`
3. Update the Google Sheets node with your Sheet ID
4. Connect your Google Sheets OAuth2 credentials
5. Connect your Gmail OAuth2 credentials
6. Update the email recipient in the Gmail node
7. Activate the workflow

## Configuration

### Google Sheets Setup

Update the `documentId` in the Google Sheets node (line 18-22):
```json
"documentId": {
  "value": "YOUR_GOOGLE_SHEET_ID"
}
```

### Email Recipient

Update the `sendTo` field in the Gmail node (line 110):
```json
"sendTo": "your-email@example.com"
```

## Usage

Once activated, this workflow automatically:
1. Triggers whenever any workflow in your n8n instance fails
2. Appends a new row to your Google Sheet with error details
3. Sends an email notification with the error information

## Email Format

The email notification includes:
- Subject: `N8N Workflow: [Workflow Name] Failed!!`
- Body:
  - Workflow name
  - Node that failed
  - Timestamp
  - Error message
  - Link to the execution

## Troubleshooting

### Errors not being logged
- Ensure the workflow is activated
- Check that your Google Sheets credentials have write access
- Verify the Sheet ID is correct

### Not receiving email notifications
- Check Gmail credentials are valid
- Verify the recipient email address
- Check spam folder
