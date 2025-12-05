# YouTube Daily Digest Workflow (No Duplicates)

An n8n workflow that automatically collects new YouTube videos from your favorite channels and sends them as a daily digest email with intelligent duplicate detection.

## Features

This workflow:
- 🔄 Runs automatically **every 6 hours**
- 📺 Monitors **7 YouTube channels** via RSS feeds
- 📅 Filters videos from the **last 7 days**
- ✅ Checks for **duplicates** using Google Sheets
- 📧 Sends an **HTML email digest** with new videos
- 💾 Logs sent videos to prevent future duplicates

## Workflow Overview

```
Schedule Trigger (every 6 hours)
    ↓
Set Channel IDs
    ↓
Split per channel
    ↓
Read RSS Feed
    ↓
Filter last 7 days
    ↓
Store Videos
    ↓
Read Sent Videos (Google Sheets)
    ↓
Dedupe Check
    ↓
Has new videos?
    ↓
Generate Email
    ↓
├─→ Send Email (Gmail)
└─→ Log Sent Videos (Google Sheets)
```

## Requirements

### n8n Credentials
1. **Google Sheets OAuth2 API** - for reading/writing the video log
2. **Gmail OAuth2** - for sending emails

### Google Sheets Setup
Create a Google Sheet with the following columns:
- `video_id` - YouTube video ID
- `sent_date` - Date the email was sent
- `title` - Video title
- `channel` - Channel name

## Configuration

### Adding/Changing YouTube Channels

Edit the **Channel IDs** node (lines 30-31 in the JSON file):

```json
"channelids": ["UCoy6cTJ7Tg0dqS-DI-_REsA", "UCg6gPGh8HU2U01vaFCAsvmQ", ...]
```

To find a YouTube channel ID:
1. Go to the YouTube channel
2. Click on the channel page
3. Copy the ID from the URL: `youtube.com/channel/[CHANNEL_ID]`

### Changing Email Recipient

Edit the **Send Email** node (line 217):

```json
"sendTo": "your-email@gmail.com"
```

### Adjusting the Schedule

The workflow runs every 6 hours by default. To change this, modify the cron expression in the **Schedule Trigger** node (line 9):

```json
"expression": "0 */6 * * *"  // Every 6 hours
```

Examples:
- `0 9 * * *` - Daily at 9:00 AM
- `0 */12 * * *` - Every 12 hours
- `0 0 * * 1` - Every Monday at midnight

### Changing Google Sheets URL

Update the document IDs in:
- **Read Sent Videos** node (line 126)
- **Log Sent Videos** node (line 258)

## How the Dedupe Check Works

The workflow uses a robust duplicate detection system:

1. **Storage**: All sent video IDs are stored in Google Sheets
2. **Check**: On each run, new videos are compared against the log
3. **Flexible**: Works with any column structure by scanning all values
4. **Clean IDs**: Converts `yt:video:` format to clean video IDs
5. **Validation**: Checks if strings match YouTube ID format (11 characters)

## Email Format

The email contains for each video:
- 🖼️ Thumbnail image
- 📌 Video title
- 👤 Channel name
- 📅 Publication date
- 🔗 Direct link to the video

## Troubleshooting

### Not receiving emails?
- Check if the Gmail OAuth2 credentials are correct
- Verify there are new videos in the last 7 days
- Review the workflow execution logs in n8n

### Duplicates not being filtered?
- Verify the Google Sheets URL is correct
- Check that the sheet is accessible with the provided credentials
- Ensure the `video_id` column exists in your sheet

### Videos not being found?
- Verify the YouTube channel IDs are correct
- Check if RSS feeds are available
- Test the RSS URL manually: `https://www.youtube.com/feeds/videos.xml?channel_id=[CHANNEL_ID]`

## Installation

1. Import the `youtube_daily_digest_workflow.json` file into n8n
2. Configure the Google Sheets OAuth2 credentials
3. Configure the Gmail OAuth2 credentials
4. Create a Google Sheet with the required columns
5. Update the Google Sheets URLs in the workflow
6. Update the email address
7. (Optional) Modify the YouTube channel IDs
8. Activate the workflow

## License

This is an open-source n8n workflow for personal use.

## Credits

Built with n8n - workflow automation platform
