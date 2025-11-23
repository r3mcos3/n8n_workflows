# n8n Workflows

This repository serves as a collection of various [n8n](https://n8n.io/) workflows. Each workflow is organized into its own dedicated folder, containing the workflow's JSON definition and a corresponding screenshot for easy reference.

## Structure

Each workflow resides in its own directory, named after the workflow. Inside each directory, you will find:

- `workflow_name.json`: The n8n workflow definition in JSON format.
- `Screenshot_DATE_TIME.png`: A screenshot of the workflow for visual overview.

Example:
```
.
└── youtube_digest_workflow/
    ├── Screenshot_2025-11-23_17-36-58.png
    └── youtube_digest_workflow.json
```

## Workflows

Here's a list of the workflows currently available in this repository:

- **YouTube Digest Workflow**: A workflow designed to [brief description of what the workflow does, e.g., create a digest of new YouTube videos].

## How to Use

### Importing a Workflow into n8n

1.  Navigate to the specific workflow's folder (e.g., `youtube_digest_workflow`).
2.  Open the `.json` file (e.g., `youtube_digest_workflow.json`) in a text editor and copy its entire content.
3.  In your n8n instance, click on "Workflows" in the left sidebar.
4.  Click on "New" or the "+" icon to create a new workflow.
5.  In the workflow editor, click on the "Import" button (usually represented by an arrow pointing down).
6.  Paste the copied JSON content into the import dialog.
7.  Click "Import" to add the workflow to your n8n instance.

### Viewing Screenshots

To get a quick visual understanding of any workflow, simply open the `Screenshot_*.png` file located within its respective workflow folder.

## Contributing

Feel free to add your own n8n workflows to this repository! Please ensure that:

1.  Each workflow is in its own clearly named folder.
2.  The folder contains both the `.json` workflow definition and a screenshot.
3.  You provide a brief description of your workflow in the `Workflows` section of this `README.md`.
