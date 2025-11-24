# Hours Registration Workflow

This directory contains an n8n workflow that allows you to easily register your worked hours via a web form. The entered data is automatically written to a Google Sheet, including calculated totals.

## Files

- `hours_registration.json`: The workflow file that you can import into n8n.

## Installation & Configuration

1.  **Import Workflow:**
    *   Open your n8n dashboard.
    *   Create a new workflow.
    *   Click on the three dots in the top right -> "Import from File".
    *   Select the `hours_registration.json` file.

2.  **Prepare Google Sheet:**
    *   Create a new Google Sheet (e.g., "Hours Registration").
    *   Add the following column headers in the first row (copy exactly or adjust in the workflow):
        *   `Date`
        *   `Week Number`
        *   `Start Time`
        *   `End Time`
        *   `Break in minutes`
        *   `Total Duration`
        *   `Worked Hours`

3.  **Configure Google Sheets Node:**
    *   Double-click the "Google Sheets" node in n8n.
    *   Select your Google Sheets credentials (or create new ones).
    *   For "Spreadsheet ID", select the sheet you just created.
    *   For "Sheet Name", select the tab (usually "Sheet1").
    *   Ensure the "Map Automatically" option is enabled.

4.  **Activate Workflow:**
    *   Click "Execute Workflow" to test.
    *   Open the "Test URL" of the "Hours Form" node to see the form and submit a test entry.
    *   If everything works, set the workflow to "Active".
    *   Use the "Production URL" of the "Hours Form" node to fill in your hours daily.

## Functionality

*   **Form:** Asks for Date, Start Time, End Time, and Break (optional).
*   **Calculation:** Automatically calculates:
    *   **Total Duration:** The total time between Start and End.
    *   **Worked Hours:** The total time minus the break.
*   **Google Sheets:** Appends a new row with all this data to the connected sheet.

## Screenshots

![Hours Registration Workflow](../.pictures/hours_registration_workflow.png)
<br>
![Hours Registration Form](../.pictures/hours_registration_workflow1.png)

