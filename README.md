# n8n Workflow Templates

Import-ready [n8n](https://n8n.io) workflow templates for common automation gigs:
AI responders, lead capture, scheduled posting, and inbox triage.

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
| `workflows/lead-capture-to-sheets.json` | `POST /new-lead` with `{"name","email"}` → appends a row to Google Sheets + sends you an email alert | Google Sheets, Gmail |
| `workflows/scheduled-social-poster.json` | Runs daily at 09:00, composes a post, sends it to a posting API (replace the HTTP node URL with Buffer / Typefully / your API) | none until you wire the API |
| `workflows/gmail-ai-triage-to-slack.json` | Watches Gmail → AI classifies each email URGENT/NORMAL → posts urgent ones to `#alerts` in Slack | Gmail, OpenAI, Slack |

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

- [ ] Import all four and get each one green with your own credentials
- [ ] Add error handling (Error Trigger node → notify yourself)
- [ ] Swap the social poster HTTP node for a real scheduler API
- [ ] Add a rate-limit / dedupe step to the lead webhook

## Related

- [ai-faq-chatbot](https://github.com/maticcretic-commits/ai-faq-chatbot) — same idea in Python
- [lead-capture-crm-automation](https://github.com/maticcretic-commits/lead-capture-crm-automation)
- [social-media-auto-poster](https://github.com/maticcretic-commits/social-media-auto-poster)
