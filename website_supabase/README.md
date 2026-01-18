# Hours Email Report - Mobile Optimized

A webhook-triggered workflow that generates beautiful, mobile-friendly HTML email reports for weekly hours tracking.

## Features

- Webhook endpoint for triggering email reports
- Mobile-first responsive HTML email design
- Industrial-themed "TIME // FORGE" branding
- Per-day breakdown with start time, end time, and breaks
- Total weekly hours calculation
- Support for notes per day entry
- Dutch language formatting

## Workflow Diagram

```
Webhook ──► Format Email ──► Gmail ──► Respond to Webhook
(POST)      (Code node)      (Send)     (JSON response)
```

## Webhook Endpoint

**Method:** POST
**Path:** `/webhook/email/week-report`

### Request Body

```json
{
  "weekNumber": 3,
  "formattedStartDate": "13-01-2025",
  "formattedEndDate": "19-01-2025",
  "total_hours": 40.5,
  "days": [
    {
      "date": "2025-01-13",
      "start_time": "08:30:00",
      "end_time": "17:00:00",
      "break_minutes": 30,
      "total_work_hours": 8.0,
      "notes": "Optional notes"
    }
  ]
}
```

### Response

```json
{
  "success": true,
  "message": "Email sent successfully"
}
```

## Email Design

The generated email features:

- **Header**: Orange gradient with TIME // FORGE branding and week number badge
- **Day Cards**: Individual cards for each day showing:
  - Day name and date
  - Work hours prominently displayed
  - Start/end times
  - Break duration
  - Optional notes in highlighted box
- **Total Box**: Gradient box showing total weekly hours
- **Footer**: Auto-generated timestamp

## Requirements

- Gmail OAuth2 API credentials

## Installation

1. Import `email-report-mobile-optimized.json` into n8n
2. Connect your Gmail OAuth2 credentials to the Gmail node
3. Update the recipient email address in the Gmail node
4. Activate the workflow
5. Note the webhook URL for your application

## Configuration

### Email Recipient

Update the `sendTo` field in the Gmail node:
```json
"sendTo": "your-email@example.com"
```

### Webhook Path

The default webhook path is `email/week-report`. To change it, update the Webhook node's `path` parameter.

## Integration

This workflow is designed to integrate with a time tracking application. Your application should:

1. Collect weekly hours data
2. Format the data according to the request body schema
3. POST to the webhook endpoint
4. Handle the JSON response

### Example cURL

```bash
curl -X POST https://your-n8n-instance/webhook/email/week-report \
  -H "Content-Type: application/json" \
  -d '{
    "weekNumber": 3,
    "formattedStartDate": "13-01-2025",
    "formattedEndDate": "19-01-2025",
    "total_hours": 40.5,
    "days": [
      {
        "date": "2025-01-13",
        "start_time": "08:30:00",
        "end_time": "17:00:00",
        "break_minutes": 30,
        "total_work_hours": 8.0
      }
    ]
  }'
```

## Troubleshooting

### Email not received
- Check Gmail credentials are valid
- Verify recipient email address
- Check n8n execution logs for errors

### Webhook not responding
- Ensure workflow is activated
- Check the webhook URL is correct
- Verify request body format matches expected schema

### Styling issues in email client
- The email uses inline styles for maximum compatibility
- Some email clients may strip certain CSS properties
- Test with multiple email clients if styling is critical
