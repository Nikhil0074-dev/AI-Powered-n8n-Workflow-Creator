# AI-Powered n8n Workflow Creator - Setup Guide

This guide will help you set up the AI-Powered n8n Workflow Creator in your n8n instance.

## Prerequisites

Before you begin, ensure you have:

1. **n8n Instance** - Self-hosted or n8n Cloud
2. **Anthropic API Key** - Get it from [anthropic.com](https://www.anthropic.com)
3. **n8n API Key** - Generated from your n8n instance
4. **Redis** (optional) - For conversation memory storage

---

## Step 1: Configure n8n API Access

### Generate API Key in n8n

1. Log in to your n8n instance
2. Go to **Settings** → **API**
3. Click **Create New API Key**
4. Copy and save your API key securely

### Enable API Access

```
bash
# In your n8n environment variables
export N8N_API_ENABLED=true
export N8N_API_KEY=your-api-key-here
```

---

## Step 2: Configure Anthropic API

### Get Your Anthropic API Key

1. Go to [Anthropic Console](https://console.anthropic.com/)
2. Sign in or create an account
3. Navigate to **API Keys**
4. Create a new API key
5. Copy and save the key securely

### Add Credentials in n8n

1. In n8n, go to **Credentials**
2. Click **Add Credential**
3. Search for **Anthropic API**
4. Enter your API key
5. Name it `anthropic-api`

---

## Step 3: Import the Main Workflow

### Option A: Import via JSON

1. Open n8n
2. Click **Workflows** → **Import from File**
3. Select `main-workflow.json`
4. Click **Import**

### Option B: Manual Creation

1. Create a new workflow
2. Add nodes as defined in `main-workflow.json`
3. Configure connections between nodes
4. Set up credentials for each node

---

## Step 4: Configure Environment Variables

Create a `.env` file or set environment variables:

```
bash
# Required
ANTHROPIC_API_KEY=sk-ant-api03-your-key-here
N8N_API_URL=https://your-n8n-instance.com
N8N_API_KEY=your-n8n-api-key

# Optional
REDIS_HOST=localhost
REDIS_PORT=6379
```

---

## Step 5: Set Up Memory (Optional)

For conversation context retention:

1. Install Redis or use n8n's built-in memory
2. Configure Redis credentials in n8n:
   - Go to **Credentials** → **Add**
   - Search for **Redis**
   - Enter connection details
   - Name it `redis-memory`

---

## Step 6: Configure Google Drive (Optional)

For documentation retrieval:

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable Google Drive API
4. Create OAuth 2.0 credentials
5. Download credentials JSON
6. Add to n8n credentials as `google-drive`

---

## Step 7: Test the Setup

### Test 1: Chat Trigger

1. Activate the workflow
2. Open the chat interface
3. Send a message: "Create a workflow that sends an email every hour"
4. Verify you receive a response

### Test 2: Workflow Creation

1. Send: "Create a webhook that saves data to Google Sheets"
2. Check if a new workflow was created in n8n
3. Verify the workflow structure is correct

---

## Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| API key errors | Verify credentials are correctly configured |
| Workflow not deploying | Check n8n API URL and key |
| AI not responding | Verify Anthropic API key has credits |
| Memory not working | Check Redis connection |

### Debug Mode

Enable debug logging:

```
bash
# In n8n environment
export DEBUG=*
```

---

## Next Steps

- Review [API.md](./API.md) for API documentation
- Check [TROUBLESHOOTING.md](./TROUBLESHOOTING.md) for common issues
- Explore example workflows in `workflows/templates/`

---

## Security Best Practices

1. **Never commit API keys** to version control
2. **Use environment variables** for sensitive data
3. **Enable 2FA** on your n8n and API accounts
4. **Rotate API keys** regularly
5. **Limit API access** to necessary endpoints only

---

## Support

- n8n Documentation: https://docs.n8n.io/
- Anthropic Docs: https://docs.anthropic.com/
- Create an issue in the repository for help
