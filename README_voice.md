# AI Voice Agent Pipeline — n8n + VAPI + GPT-4o-mini

Automated AI voice agent system that handles inbound calls, analyzes transcripts with AI, logs leads to Google Sheets, and sends personalized SMS follow-ups — fully automated, no human needed.

## How It Works

```
Inbound Call → VAPI → n8n Webhook → AI Analysis → Google Sheets → SMS Follow-up
```

1. Customer calls your VAPI phone number
2. AI voice agent handles the conversation
3. After call ends, VAPI sends transcript to n8n
4. GPT-4o-mini analyzes the call and scores the lead
5. Results logged to Google Sheets automatically
6. Hot leads get instant personalized SMS follow-up

## What AI Extracts From Every Call

| Field | Description |
|-------|-------------|
| `caller_intent` | What the caller wanted |
| `lead_quality` | hot / warm / cold |
| `key_info` | Main points discussed |
| `next_action` | Recommended follow-up |
| `appointment_requested` | true / false |
| `follow_up_message` | Personalized SMS text |

## Quick Start

### 1. Set Up VAPI
- Create account at [vapi.ai](https://vapi.ai)
- Create a new assistant with your system prompt
- Set webhook URL to your n8n webhook URL

### 2. Import Workflow
- Go to your n8n instance
- Click **+** → **Import workflow**
- Upload `ai-voice-agent.json`

### 3. Configure Nodes

**AI Call Analysis node:**
- Add OpenAI API key

**Log to Google Sheets node:**
- Add Google Sheets OAuth2 credential
- Replace `YOUR_GOOGLE_SHEET_ID` with your Sheet ID
- Create a sheet named **Calls** with columns:
```
Call_ID | Phone | Intent | Lead_Quality | Key_Info | Next_Action | Appointment | Timestamp
```

**Send Follow-up SMS node (optional):**
- Add Twilio credentials
- Replace `YOUR_ACCOUNT_SID` and `YOUR_TWILIO_PHONE_NUMBER`

### 4. Activate
- Toggle workflow to **Active**
- Copy the webhook URL from the VAPI Webhook node
- Paste it into your VAPI assistant webhook settings

## Use Cases

- Real estate inbound calls — qualify buyers/sellers automatically
- Medical clinic — handle appointment requests 24/7
- E-commerce — handle order inquiries without staff
- Law firm — intake calls and capture lead info
- Dental/beauty clinic — booking and follow-up automation

## VAPI System Prompt Example

```
You are a helpful assistant for [COMPANY NAME]. 
Your job is to:
1. Greet the caller warmly
2. Understand what they need
3. Collect their name and email
4. Answer basic questions about our services
5. Offer to book an appointment

Be friendly, professional, and concise.
```

## Requirements

- n8n instance (cloud or self-hosted)
- VAPI account and phone number
- OpenAI API key
- Google Sheets OAuth2 credentials
- Twilio account (optional, for SMS)

## Tech Stack

- **n8n** — workflow orchestration
- **VAPI** — AI voice calls
- **OpenAI GPT-4o-mini** — call analysis
- **Google Sheets** — lead logging
- **Twilio** — SMS follow-up

---

Built by [Nurmuhammad Adkhamjonov](https://github.com/nurikk-66) — AI Automation Engineer
