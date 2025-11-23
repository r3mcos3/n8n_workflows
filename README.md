# n8n Workflows

This repository serves as a collection of various [n8n](https://n8n.io/) workflows. Each workflow is organized into its own dedicated folder, containing the workflow's JSON definition and a corresponding screenshot for easy reference.

## Structure

Each workflow resides in its own dedicated folder. Inside each workflow folder, you will find:

- `workflow_name.json`: The n8n workflow definition in JSON format.
- `README.md`: A description of the workflow, including an embedded screenshot.

All workflow screenshots are centrally stored in the hidden `.pictures/` directory at the repository root.

Example:
```
.
├── .pictures/
│   └── youtube_digest_workflow.png
└── youtube_digest_workflow/
    ├── README.md
    └── youtube_digest_workflow.json
```

## Workflows

Here's a list of the workflows currently available in this repository. Click on the workflow's folder and open its `README.md` for details and screenshots.

- **YouTube Digest Workflow**: (Details and screenshot available in `youtube_digest_workflow/README.md`)

## How to Use

### Importing a Workflow into n8n

1.  Navigate to the specific workflow's folder (e.g., `youtube_digest_workflow`).
2.  Open the `.json` file (e.g., `youtube_digest_workflow.json`) in a text editor and copy its entire content.
3.  In your n8n instance, click on "Workflows" in the left sidebar.
4.  Click on "New" or the "+" icon to create a new workflow.
5.  In the workflow editor, click on the "Import" button (usually represented by an arrow pointing down).
6.  Paste the copied JSON content into the import dialog.
7.  Click "Import" to add the workflow to your n8n instance.

### Viewing Workflow Details and Screenshots

To get a visual understanding and detailed description of any workflow, navigate to its dedicated folder (e.g., `youtube_digest_workflow/`) and open the `README.md` file located there. The screenshot will be embedded directly in that file.

