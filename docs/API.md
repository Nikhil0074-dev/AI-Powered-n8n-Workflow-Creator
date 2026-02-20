# API Documentation

## Overview

The AI-Powered n8n Workflow Creator exposes the following endpoints and interfaces.

---

## Chat Trigger

### Endpoint

```
POST /webhook/{webhook-path}
```

### Request Body

```
json
{
  "message": "Create a workflow that sends email when Google Sheet is updated",
  "userId": "user-123",
  "sessionId": "session-456"
}
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| message | string | Yes | Natural language workflow request |
| userId | string | No | Unique user identifier |
| sessionId | string | No | Session identifier for context |

### Response

#### Success

```
json
{
  "success": true,
  "workflowId": "workflow-789",
  "workflowName": "Email on Google Sheet Update",
  "workflowUrl": "https://n8n-instance.com/workflow/workflow-789",
  "message": "Workflow created successfully! 🎉"
}
```

#### Error

```
json
{
  "success": false,
  "error": {
    "code": "WORKFLOW_ERROR",
    "message": "Failed to create workflow"
  }
}
```

---

## n8n API Integration

### Create Workflow

```
POST {N8N_API_URL}/api/v1/workflows
```

#### Headers

```
Content-Type: application/json
X-N8N-API-KEY: {your-api-key}
```

#### Body

```
json
{
  "name": "Workflow Name",
  "nodes": [
    {
      "id": "node-1",
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "parameters": {},
      "position": [250, 300]
    }
  ],
  "connections": {},
  "active": false
}
```

### Update Workflow

```
PATCH {N8N_API_URL}/api/v1/workflows/{workflowId}
```

### Delete Workflow

```
DELETE {N8N_API_URL}/api/v1/workflows/{workflowId}
```

### Get Workflow

```
GET {N8N_API_URL}/api/v1/workflows/{workflowId}
```

---

## Anthropic AI Integration

### Analyze Prompt

The AI analyzes user input to determine:

- **Trigger Type**: What starts the workflow
- **Required Nodes**: What actions are needed
- **Configuration**: Specific settings mentioned
- **Connections**: How nodes should link together

### Response Format

```
json
{
  "trigger": {
    "type": "googleSheets",
    "name": "Google Sheets - Row Created"
  },
  "nodes": [
    {
      "type": "emailSend",
      "name": "Send Email",
      "parameters": {}
    }
  ],
  "connections": [
    {
      "from": "Google Sheets - Row Created",
      "to": "Send Email"
    }
  ],
  "description": "Sends an email when a new row is added to Google Sheets"
}
```

---

## Memory API

### Store Context

```
POST /webhook/memory/store
```

```
json
{
  "userId": "user-123",
  "sessionId": "session-456",
  "message": "Create workflow for email",
  "context": {
    "lastWorkflow": "email-workflow",
    "preferences": {}
  }
}
```

### Retrieve Context

```
POST /webhook/memory/retrieve
```

```
json
{
  "userId": "user-123",
  "sessionId": "session-456"
}
```

---

## Webhook Events

### Workflow Activated

```
json
{
  "event": "workflow.activated",
  "workflowId": "workflow-123",
  "timestamp": "2025-01-13T12:00:00Z"
}
```

### Workflow Error

```
json
{
  "event": "workflow.error",
  "workflowId": "workflow-123",
  "error": "Node execution failed",
  "timestamp": "2025-01-13T12:00:00Z"
}
```

---

## Rate Limits

| Endpoint | Limit |
|----------|-------|
| Chat Trigger | 60 requests/minute |
| API (Create) | 100 requests/minute |
| AI Analysis | 20 requests/minute |

---

## Error Codes

| Code | Description |
|------|-------------|
| `INVALID_INPUT` | User message is empty or invalid |
| `AI_ERROR` | AI analysis failed |
| `JSON_ERROR` | Generated workflow JSON is invalid |
| `WORKFLOW_ERROR` | Failed to create/update workflow |
| `AUTH_ERROR` | API authentication failed |
| `RATE_LIMIT` | Too many requests |

---

## Example Requests

### cURL - Create Workflow

```bash
curl -X POST https://your-n8n.com/webhook/chat \
  -H "Content-Type: application/json" \
  -d '{
    "message": "Create a workflow that sends Slack notification when webhook is triggered",
    "userId": "user-123",
    "sessionId": "session-456"
  }'
```

### JavaScript - Frontend Integration

```
javascript
async function createWorkflow(message) {
  const response = await fetch('https://your-n8n.com/webhook/chat', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      message: message,
      userId: 'user-123',
      sessionId: 'session-456'
    })
  });
  
  return await response.json();
}

// Usage
const result = await createWorkflow('Send email when new row in Google Sheets');
console.log(result.workflowUrl);
```

---

## Versioning

Current API Version: **v1**

Future versions will be available at:
- `/api/v2/`
- `/api/v3/`

---

## Support

For API issues, contact support or create an issue in the repository.
