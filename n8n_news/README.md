# n8n News Workflow

This workflow automates the process of gathering the latest news about n8n and sending a weekly digest via email.

## Overview

The workflow runs on a weekly schedule, searches for the latest n8n news using Tavily, formats the results into a clean HTML email, and sends it to the configured recipient.

## Workflow Steps

1.  **Schedule Trigger**: Triggers the workflow every Saturday at 08:00.
2.  **Edit Fields**: Sets the search query to "latest news about n8n".
3.  **Search (Tavily)**: Performs a web search using the Tavily API to find relevant articles.
4.  **Code (JavaScript)**:
    *   Filters search results to remove low-quality matches.
    *   Generates a responsive HTML email template.
    *   Populates the template with the article data.
5.  **Send a message (Gmail)**: Sends the generated HTML email to the subscriber.

## Prerequisites

To use this workflow, you need the following credentials configured in n8n:

*   **Tavily API**: For searching the web.
*   **Gmail OAuth2**: For sending the email.

## Configuration

*   **Recipient Email**: Update the `sendTo` field in the "Send a message" node to your desired email address.
*   **Search Query**: You can modify the search query in the "Edit Fields" node if you want to track different topics.

## Screenshots

<img width="1498" height="398" alt="n8n_weekly_news_workflow" src="https://github.com/user-attachments/assets/dc74ded2-aa8c-47b4-b0d0-1a7b322633d0" />


## License

This project is licensed under the terms of the MIT license.
