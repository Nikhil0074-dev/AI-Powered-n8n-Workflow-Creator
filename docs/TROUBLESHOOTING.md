# Troubleshooting Guide

## Common Issues and Solutions

---

## Issue 1: Chat Trigger Not Responding

### Symptoms
- User sends message but receives no response
- Workflow shows as active but no execution

### Possible Causes
1. Webhook URL is incorrect
2. Chat trigger is not activated
3. Firewall blocking requests

### Solutions
1. **Verify webhook URL**
   
```
   Check the webhook path in the Chat Trigger node
   Ensure it matches the URL being called
   
```

2. **Activate workflow**
   
```
   Go to n8n → Workflows → Find your workflow → Activate
   
```

3. **Check execution history**
   
```
   Open workflow → Click on executions → Check for errors
   
```

---

## Issue 2: AI Not Generating Workflow

### Symptoms
- Workflow creates but AI node shows error
- No JSON output from AI node

### Possible Causes
1. Invalid or expired Anthropic API key
2. API key doesn't have sufficient credits
3. Prompt template error

### Solutions
1. **Verify API key**
   
```
   Go to n8n → Credentials → anthropic-api → Test
   
```

2. **Check API credits**
   
```
   Log into anthropic.com console → Check usage
   
```

3. **Review prompt**
   
```
   Open AI node → Check prompt expression
   Ensure {{ $json.message }} is valid
   
```

---

## Issue 3: Workflow Deployment Fails

### Symptoms
- AI generates JSON but workflow not created
- Error in Deploy Workflow node

### Possible Causes
1. n8n API URL is incorrect
2. API key is invalid or expired
3. JSON structure is invalid

### Solutions
1. **Verify API URL**
   
```
   Check N8N_API_URL environment variable
   Should be: https://your-n8n-instance.com
   
```

2. **Test API key**
   
```
   curl -H "X-N8N-API-KEY: your-key" \
     https://your-n8n.com/api/v1/workflows
   
```

3. **Validate JSON output**
   
```
   Add a Set node after AI generator
   Inspect the output JSON structure
   
```

---

## Issue 4: Memory Not Working

### Symptoms
- No conversation history retained
- Context lost between messages

### Possible Causes
1. Redis not configured
2. Memory node not connected
3. Session ID not provided

### Solutions
1. **Configure Redis**
   
```
   Go to n8n → Credentials → Add → Redis
   Enter host, port, password
   
```

2. **Connect memory node**
   
```
   Ensure Memory node is connected to Store Context
   Check connections in workflow
   
```

3. **Provide session ID**
   
```
   Always include sessionId in request
   Without it, context won't be tracked
   
```

---

## Issue 5: Invalid JSON Generation

### Symptoms
- AI returns text instead of JSON
- JSON has syntax errors

### Possible Causes
1. Prompt not instructing AI to return JSON
2. AI model limitation
3. Max tokens too low

### Solutions
1. **Update prompt**
   
```
   Add to prompt: "Return ONLY valid JSON, no other text"
   
```

2. **Increase max tokens**
   
```
   Open AI node → Options → Max Tokens → Set to 2000+
   
```

3. **Add JSON validation**
   
```
   Add a Code node after AI to parse JSON
   Use: {{ JSON.parse($json.ai_output) }}
   
```

---

## Issue 6: Rate Limiting Errors

### Symptoms
- Too Many Requests error
- Workflow stops working after many calls

### Solutions
1. **Implement delay**
   
```
   Add Wait node between requests
   Set to 1-2 seconds
   
```

2. **Add queue system**
   
```
   Use n8n's queue mode
   Enable in n8n settings
   
```

3. **Contact for higher limits**
   
```
   Reach out to Anthropic for API limit increase
   
```

---

## Issue 7: Node Connection Errors

### Symptoms
- Nodes not connecting properly
- Workflow shows broken connections

### Solutions
1. **Check connection format**
   
```json
   {
     "main": [[{
       "node": "Node Name",
       "type": "main",
       "index": 0
     }]]
   }
   
```

2. **Verify node names**
   
```
   Connection references must match node names exactly
   Check for typos or extra spaces
   
```

---

## Debug Mode

### Enable Debug Logging

1. **Environment variable**
   
```
bash
   export DEBUG=*
   
```

2. **In workflow**
   
```
   Add Notice node with debug output
   Connect to see intermediate results
   
```

### Check Execution Steps

1. Open workflow in n8n
2. Click on specific node
3. View input/output data
4. Identify where process fails

---

## Getting Help

### Information to Collect

When reporting an issue, include:

1. **n8n version**
   
```
   Check: Settings → About
   
```

2. **Error message**
   
```
   Copy exact error from execution
   
```

3. **Workflow JSON**
   
```
   Export: Workflow → Download → JSON
   
```

4. **Steps to reproduce**
   
```
   List exact actions taken
   
```

### Resources

- **n8n Forum**: https://community.n8n.io/
- **Anthropic Support**: https://support.anthropic.com/
- **GitHub Issues**: Create issue in repository

---

## Prevention Tips

1. **Always test with simple requests first**
   
```
   Start with: "Create a simple webhook workflow"
   
```

2. **Keep API keys secure**
   
```
   Never commit to version control
   Use environment variables
   
```

3. **Monitor usage**
   
```
   Check API credits regularly
   Set up usage alerts
   
```

4. **Backup workflows**
   
```
   Export workflows frequently
   Keep local backups
   
```

---

## Known Limitations

1. **Complex workflows**: Very complex workflows may need manual editing
2. **Authentication**: OAuth flows require manual configuration
3. **Rate limits**: Subject to API rate limiting
4. **Context window**: Limited to AI model's context size

---

Last Updated: January 2025
