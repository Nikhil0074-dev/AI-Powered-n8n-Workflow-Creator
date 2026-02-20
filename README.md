# AI-Powered n8n Workflow Creator

An intelligent automation system that allows users to create, modify, and manage n8n workflows using natural language chat prompts.

## Overview

The AI-Powered n8n Workflow Creator (also known as n8n Developer Agent) transforms manual workflow configuration into an intelligent, conversational experience. Users describe what they want to automate in plain English, and the system automatically generates, deploys, and provides access to working n8n workflows.

## Features

- **Natural Language Workflow Creation**: Describe your automation needs in plain English
- **AI-Based Workflow Generation**: Intelligent node selection and connection logic
- **Dynamic Workflow Deployment**: Automatically creates and activates workflows in n8n
- **Context Retention**: Maintains conversation history for follow-up requests
- **Workflow Sharing**: Provides shareable workflow URLs

## System Architecture


┌─────────────────┐
│   Trigger Layer │ ← Chat Trigger, Workflow Trigger
└────────┬────────┘
         ▼
┌─────────────────────┐
│  AI Processing Layer │ ← Prompt Analysis, Logic Generation
└────────┬────────────┘
         ▼
┌─────────────────────┐
│ Documentation Layer │ ← Google Drive Retrieval
└────────┬────────────┘
         ▼
┌─────────────────────────┐
│ Workflow Management Layer │ ← JSON Validation, Deployment
└────────┬────────────────┘
         ▼
┌─────────────────┐
│  Memory Layer   │ ← Context Storage, Sticky Notes
└─────────────────┘
```

## Tech Stack

- **Frontend**: n8n Chat Trigger
- **Backend**: n8n Workflow Engine
- **AI Models**: Claude Opus 4 (Anthropic)
- **File Storage**: Google Drive
- **API**: n8n REST API

## Getting Started

### Prerequisites

- n8n instance (self-hosted or cloud)
- Anthropic API key (for Claude Opus 4)
- Google Drive API credentials (optional, for documentation retrieval)

### Installation

1. Clone or download this repository
2. Import the main workflow into your n8n instance
3. Configure the required credentials:
   - Anthropic API credentials
   - n8n API key (for workflow deployment)
   - Google Drive credentials (optional)
4. Activate the workflow
5. Open the chat interface and start creating workflows!

## Usage Examples

### Example 1: Email Automation
**User Input:**

Create a workflow that sends an email when a new Google Sheet row is added.


**System Action:**
1. Analyzes prompt → identifies Google Sheets Trigger + Email node needed
2. Generates JSON workflow with proper node configuration
3. Deploys workflow in n8n
4. Returns workflow URL

### Example 2: Slack Notifications
**User Input:**

Send a Slack message when a webhook is triggered with customer data.


**System Action:**
1. Identifies Webhook Trigger + Slack node
2. Creates workflow with message formatting
3. Deploys and returns URL

## Project Structure


n8n-ai-workflow-creator/
├── README.md
├── workflows/
│   ├── main-workflow.json          # Main AI Workflow Creator
│   ├── sub-workflows/
│   │   ├── prompt-analyzer.json    # Analyzes user prompts
│   │   ├── workflow-generator.json  # Creates n8n JSON
│   │   ├── workflow-deployer.json  # Deploys to n8n
│   │   └── memory-manager.json     # Handles context
│   └── templates/                  # Example workflow templates
├── docs/
│   ├── SETUP.md                    # Setup instructions
│   ├── API.md                      # API documentation
│   └── TROUBLESHOOTING.md          # Common issues
└── config/
    └── credentials.json.example     # Example credentials


## Configuration

### Required Credentials

| Credential | Description |
|------------|-------------|
| `anthropic-api` | Anthropic API key for Claude Opus 4 |
| `n8n-api` | n8n API key for workflow management |
| `google-drive` | Google Drive credentials (optional) |

### Environment Variables


json
{
  "ANTHROPIC_API_KEY": "your-api-key",
  "N8N_API_URL": "https://your-n8n-instance.com",
  "N8N_API_KEY": "your-n8n-api-key"
}


## Workflow Process


1. User sends chat request
       │
       ▼
2. AI analyzes prompt
       │
       ▼
3. Required nodes identified
       │
       ▼
4. JSON workflow generated
       │
       ▼
5. Workflow deployed in n8n
       │
       ▼
6. User receives workflow link


## API Reference

### Chat Trigger Endpoint


POST /webhook/chat
{
  "message": "Create a workflow that...",
  "userId": "user-123",
  "sessionId": "session-456"
}


### Workflow Response


json
{
  "success": true,
  "workflowId": "workflow-789",
  "workflowUrl": "https://n8n-instance.com/workflow/workflow-789",
  "message": "Workflow created successfully!"
}

