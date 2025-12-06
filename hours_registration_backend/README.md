# Hours Registration Backend Workflow

This n8n workflow provides a complete hours registration system with two main functionalities:
1. **Hours Registration**: Submit work hours via a webhook endpoint
2. **Weekly Email Reports**: Generate and send formatted weekly hour reports via Gmail

## Overview

The workflow accepts hours registration data through a webhook, calculates worked hours (both gross and net after breaks), stores the data in an n8n data table, and can generate weekly HTML email reports summarizing all registered hours.

## Screenshots

<img width="1479" height="517" alt="hours_registration_website" src="https://github.com/user-attachments/assets/c4cbf5b9-ea91-41a7-8984-ffadbe2ec4b6" />

## Features

### 1. Hours Registration Endpoint (`/uren`)
- **Method**: POST
- **Functionality**: Receives work hours data and stores it in a data table
- **Input Fields**:
  - `Date`: The work date
  - `Start Time`: When work started (HH:MM format)
  - `End Time`: When work ended (HH:MM format)
  - `Break in minutes`: Break duration in minutes
  - `Week Number`: The week number for reporting
  - `Notes`: Optional notes about the work

### 2. Weekly Report Email Endpoint (`/mail`)
- **Method**: POST
- **Functionality**: Retrieves all hours from the data table, generates an HTML report, and sends it via Gmail
- **Output**: Professional HTML email with:
  - Weekly overview table with all registered hours
  - Individual day details (date, start, end, break, hours worked, notes)
  - Total calculated hours for the week
  - Alternating row colors for readability

## Workflow Components

### Nodes

1. **Uren (Webhook)**: POST endpoint to receive hours registration data
2. **Code in JavaScript**: Calculates gross and net hours worked
   - Computes total hours between start and end time
   - Subtracts break time to get net worked hours
   - Formats output as both raw numbers and HH:MM format
3. **Insert row (Data Table)**: Stores the hours data in the "Uren Registratie" data table
4. **Mail (Webhook)**: POST endpoint to trigger email report generation
5. **Get row(s) (Data Table)**: Retrieves all stored hours from the data table
6. **Code in JavaScript1**: Generates HTML email report
   - Groups hours by week number
   - Creates formatted HTML table with styling
   - Calculates weekly totals
7. **Send a message (Gmail)**: Sends the formatted report via Gmail

## Data Table Schema

The workflow uses an n8n data table named "Uren Registratie" with the following fields:
- `date`: Work date
- `starttime`: Start time
- `endtime`: End time
- `break_in_minutes`: Break duration
- `weeknumber`: Week number
- `notes`: Optional notes

## How It Works

### Registering Hours
1. Client sends POST request to `/uren` webhook with hours data
2. JavaScript code calculates:
   - Total hours (gross) = end time - start time
   - Worked hours (net) = total hours - break time
3. Data is inserted into the data table

### Generating Weekly Reports
1. Client sends POST request to `/mail` webhook
2. Workflow retrieves all rows from the data table
3. JavaScript code:
   - Filters data by week number
   - Generates professional HTML email with styled table
   - Calculates total hours for the week
4. Email is sent via Gmail to the configured recipient

## Setup Requirements

1. **n8n Instance**: A running n8n instance
2. **Gmail OAuth2 Credentials**: Configure Gmail OAuth2 credentials in n8n
3. **Data Table**: The workflow automatically references the "Uren Registratie" data table

## Configuration

Before using this workflow:

1. Import the workflow JSON into your n8n instance
2. Configure Gmail OAuth2 credentials:
   - Navigate to the "Send a message" node
   - Set up Gmail OAuth2 authentication
3. Update the email recipient in the "Send a message" node to your desired email address
4. Ensure the data table "Uren Registratie" exists or create it with the required schema

## Usage Example

### Registering Hours
```bash
curl -X POST https://your-n8n-instance.com/webhook/uren \
  -H "Content-Type: application/json" \
  -d '{
    "Date": "2025-12-04",
    "Start Time": "09:00",
    "End Time": "17:30",
    "Break in minutes": "30",
    "Week Number": "49",
    "Notes": "Regular work day"
  }'
```

### Requesting Weekly Report
```bash
curl -X POST https://your-n8n-instance.com/webhook/mail \
  -H "Content-Type: application/json"
```

## Email Report Features

The generated email includes:
- Week number and date range in the subject line
- Professionally styled HTML table with:
  - Date, start time, end time, break duration
  - Calculated hours worked
  - Notes for each day
- Alternating row colors for better readability
- Total hours summary at the bottom
- Responsive design for mobile viewing

## Notes

- All times are processed in UTC to avoid timezone issues
- Hours are calculated with precision and displayed in HH:MM format
- The workflow supports multiple entries per week
- Email reports automatically sort entries by date

## License

Part of the n8n workflows collection.
