---
name: client-support-router
description: "Routes incoming client messages by intent, generates on-brand responses, flags escalations. No operator required for BOOKING/QUOTE/INFO/OBJECTION/ACK. Always escalates COMPLAINT and UNKNOWN."
---

# Client Support Router

## WHEN TO LOAD
Load when processing any incoming client message that requires a response (WhatsApp, DM, email, contact form).

## CONFIG

```yaml
business_name: ""
service_type: ""          # beauty_salon | freelancer | agency | coach | other
response_voice: ""        # formal | conversational | warm
pricing:
  - service: ""
    price: ""
available_hours: ""
escalation_contact: ""
```

## INTENT CLASSIFICATION

| Signal words | Intent | Escalate |
|---|---|---|
| agendar · cita · reservar · disponibilidad · cuándo puedes | BOOKING | NO |
| precio · cuánto · costo · tarifa · presupuesto · cobras | QUOTE | NO |
| cómo funciona · qué incluye · explica · información · qué es | INFO | NO |
| problema · queja · mal · no funcionó · decepcionado · reclamo | COMPLAINT | YES |
| no sé si · duda · miedo · pero · aunque · no estoy seguro | OBJECTION | NO |
| gracias · ok · recibido · confirmado · perfecto · entendido | ACK | NO |
| anything else | UNKNOWN | YES |

## RESPONSE RULES

Use configured `response_voice` throughout:
- `formal` — usted, complete sentences, no contractions
- `conversational` — tú, relaxed, can use ellipsis
- `warm` — tú, emojis allowed, feels human

Never invent pricing — use `pricing` config only.
Never promise timelines not in config.
Response length: 2–4 sentences max.
End BOOKING and QUOTE responses with a single open question.

## ESCALATION FORMAT

When `Escalate: YES`:
- Still classify the intent
- Do not generate a client-facing response
- Generate an internal operator note explaining why escalation is needed

## OUTPUT FORMAT

```
Intent:     {BOOKING|QUOTE|INFO|COMPLAINT|OBJECTION|ACK|UNKNOWN}
Confidence: {HIGH|LOW}
Escalate:   {YES|NO}

Response:
{ready-to-send client response, or ESCALATED if Escalate=YES}

Note (operator):
{internal note — only when Escalate=YES}
```

## QUALITY GATE

- [ ] Intent classified with rationale
- [ ] Response voice matches config
- [ ] No invented pricing or timelines in response
- [ ] COMPLAINT and UNKNOWN always have Escalate=YES
- [ ] Response is 2–4 sentences
- [ ] BOOKING/QUOTE ends with one open question
