# n8n Workflows

This directory contains example n8n workflow definitions. These JSON files can be imported directly into an n8n instance to set up pre-configured automation workflows.

## Workflows:

-   **`authentication-no-env.json`**:
    Description: This workflow provides a simple authentication mechanism without using environment variables. It checks for a valid API key (passed in `X-API-Key` header) and a password (in the request body). This is useful for securing endpoints with basic credential checks. **Remember to change "VERANDER_DIT_NAAR_JOUW_API_KEY" and "VERANDER_DIT_NAAR_JOUW_WACHTWOORD" within the workflow to your actual API key and password.**

-   **`email-report-gmail.json`**:
    Description: This workflow automates the generation and sending of a weekly report via Gmail. It is triggered by a webhook, calculates current week information, retrieves relevant data from a Google Sheet, formats it into an HTML email, and sends it to a specified recipient. **Requires Google Sheets and Gmail credentials, and placeholders like `YOUR_SPREADSHEET_ID` and recipient email (`jouw-email@gmail.com`) need to be updated.**

-   **`time-tracking-sheets.json`**:
    Description: This workflow provides a comprehensive time-tracking solution integrated with Google Sheets. It exposes three API endpoints via webhooks:
    *   **GET `time/week`**: Retrieves and formats all time entries for the current week from Google Sheets.
    *   **POST `time/entry`**: Adds a new time entry to Google Sheets, automatically calculating total worked hours based on provided start time, end time, and break minutes.
    *   **DELETE `time/entry/:id`**: Deletes a specific time entry from Google Sheets based on the date (`:id`) provided in the URL.
    **Requires Google Sheets credentials and `YOUR_SPREADSHEET_ID` to be updated.**

## How to use:

1.  Open your n8n instance.
2.  Navigate to "Workflows".
3.  Click "New" or "Import from file".
4.  Select the desired JSON file from this directory and import it.
5.  Configure any necessary credentials or settings within the imported workflow.
