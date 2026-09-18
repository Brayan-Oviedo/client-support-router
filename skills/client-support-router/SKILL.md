---
name: client-support-router
description: "Handles every routine client message automatically — BOOKING, QUOTE, INFO, OBJECTION, ACK — so the operator only shows up for what truly needs them."
---

## WHEN TO LOAD
Before you answer any client message manually. Every sentence you type for a routine inquiry is a process you still own.

## CONFIG

```yaml
business_name: ""
service_type: ""       # beauty_salon | freelancer | agency | coach | other
response_voice: ""     # formal | conversational | warm
pricing:
  - service: ""
    price: ""
available_hours: ""
escalation_contact: ""
```

## INTENT — WHAT THIS REPLACES

| Intent | Manual process it takes over | Escalate |
|---|---|---|
| BOOKING | Checking availability and typing a reply | NO |
| QUOTE | Looking up prices and writing the same paragraph | NO |
| INFO | Explaining the same thing for the 10th time this week | NO |
| OBJECTION | Handling doubt without a script, hoping it lands | NO |
| ACK | Reading and typing "perfecto, con gusto" | NO |
| COMPLAINT | Needs you — escalate with full context | YES |
| UNKNOWN | Needs you — escalate with full context | YES |

## RESPONSE RULES

- `formal` — usted, complete sentences
- `conversational` — tú, relaxed
- `warm` — tú, emojis allowed

Never invent pricing. Never promise timelines not in config.
2–4 sentences max. BOOKING/QUOTE end with one open question.

## ESCALATION FORMAT

When `Escalate: YES`: classify intent, skip client response, output operator note with full context.

## PAIR WITH N8N

To remove the operator entirely from routine messages:

```
WhatsApp / IG DM → n8n webhook → HTTP node → Claude + this skill
→ Escalate=NO → reply via WhatsApp/DM node
→ Escalate=YES → notify operator via Telegram or Slack
```

Pair with `czlonkowski/n8n-mcp` to control n8n flows from Claude directly.

## OUTPUT FORMAT

```
Intent:     {BOOKING|QUOTE|INFO|COMPLAINT|OBJECTION|ACK|UNKNOWN}
Confidence: {HIGH|LOW}
Escalate:   {YES|NO}

Response:
{ready-to-send reply, or ESCALATED}

Note (operator):
{context for fast resolution — only when Escalate=YES}
```

## QUALITY GATE

- [ ] Intent classified
- [ ] Voice matches config
- [ ] No invented pricing or timelines
- [ ] COMPLAINT + UNKNOWN always Escalate=YES
- [ ] 2–4 sentences, BOOKING/QUOTE ends with question
