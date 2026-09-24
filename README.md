# n8n Workflow Templates

[![GitHub stars](https://img.shields.io/github/stars/maticcretic-commits/n8n-workflow-templates?style=social)](https://github.com/maticcretic-commits/n8n-workflow-templates/stargazers)
[![Last commit](https://img.shields.io/github/last-commit/maticcretic-commits/n8n-workflow-templates)](https://github.com/maticcretic-commits/n8n-workflow-templates/commits/main)
[![Cost: Free](https://img.shields.io/badge/cost-%E2%82%B90-brightgreen)](https://github.com/maticcretic-commits/n8n-workflow-templates)


Import-ready [n8n](https://n8n.io) workflow templates for common automation gigs:
AI responders, lead capture, scheduled posting, inbox triage, and error alerting.

> Starter templates built for learning. Connect your own API credentials after
> importing — nothing here runs without your keys.

## How to import

1. Open your n8n instance → **Workflows** → **⋯ → Import from file**
2. Pick a `.json` from `workflows/`
3. Open each node with a warning badge and add your credentials
4. **Activate** the workflow

## Workflows

| File | What it does | Credentials you need |
|---|---|---|
| `workflows/ai-faq-webhook-responder.json` | `POST /faq-ask` with `{"question": "..."}` → GPT answer returned as JSON | OpenAI |
| `workflows/lead-capture-to-sheets.json` | `POST /new-lead` with `{"name","email"}` → checks for duplicate email → appends a row to Google Sheets + sends you an email alert | Google Sheets, Gmail |
| `workflows/scheduled-social-poster.json` | Runs daily at 09:00, composes a post, sends it to a posting API (replace the HTTP node URL with Buffer / Typefully / your API) | none until you wire the API |
| `workflows/gmail-ai-triage-to-slack.json` | Watches Gmail → AI classifies each email URGENT/NORMAL → posts urgent ones to `#alerts` in Slack | Gmail, OpenAI, Slack |
| `workflows/error-trigger-to-slack.json` | Catches any workflow failure → posts the error to `#alerts` in Slack + emails you | Slack, Gmail |

## Error alerts

1. Import `workflows/error-trigger-to-slack.json` and activate it
2. In each workflow → **Settings → Error Workflow** → select "Error Alerts to Slack"
3. Any failure will now ping `#alerts` and email you with the workflow name, error, and execution link

## Try it

```bash
# Fire a test question at the FAQ responder (after importing + activating)
curl -X POST https://YOUR-N8N-DOMAIN/webhook/faq-ask \
  -H 'Content-Type: application/json' \
  -d '{"question": "What are your working hours?"}'

# Fire a test lead
curl -X POST https://YOUR-N8N-DOMAIN/webhook/new-lead \
  -H 'Content-Type: application/json' \
  -d '{"name": "Test Lead", "email": "test@example.com"}'
```

## Learning TODOs

- [x] Import all five and get each one green with your own credentials
- [x] Add error handling (Error Trigger workflow → Slack + email alerts)
- [ ] Swap the social poster HTTP node for a real scheduler API
- [x] Add a rate-limit / dedupe step to the lead webhook

## Related

- [ai-faq-chatbot](https://github.com/maticcretic-commits/ai-faq-chatbot) — same idea in Python
- [lead-capture-crm-automation](https://github.com/maticcretic-commits/lead-capture-crm-automation)
- [social-media-auto-poster](https://github.com/maticcretic-commits/social-media-auto-poster)

## ❤️ Support My Work

> If you find this project useful, please consider supporting my work with a Bitcoin donation:
>
> **₿ `BC1Q6Q75K8ZJXVW7W02LMDPRPY6XX6QK4LZZ2RMVAY`**

## ☕ Support my work
If this project was useful, you can support it with Bitcoin: `bc1q6q75k8zjxvw7w02lmdprpy6xx6qk4lzz2rmvay`
