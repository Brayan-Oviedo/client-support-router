# client-support-router

> A Claude skill that routes client messages by intent and generates ready-to-send responses — without the operator as the bottleneck.

Built from a real deployment: a one-person service business went from manual WhatsApp responses all day to 24/7 automated coverage in 48 hours.

---

## The problem

You are the only one who responds to clients. Every quote request, booking question, and "how much do you charge" sits in your inbox waiting for you. Your business stops when you stop.

This is not a time management problem. It is a structural one.

## What this skill does

1. **Classifies** the incoming message by intent — booking, quote, question, complaint, objection
2. **Generates** a ready-to-send response in your configured business voice
3. **Flags** messages that genuinely need you — complaints, unknown intents, edge cases
4. **Logs** the intent decision for your async review

You stay in the loop where it matters. Everything else is handled.

---

## Install

```bash
npx skills add https://github.com/Brayan-Oviedo/client-support-router --skill client-support-router
```

---

## Configure

Open `skills/client-support-router/SKILL.md` and fill in the config block:

```yaml
business_name: "Your Business"
service_type: "freelancer"          # beauty_salon | freelancer | agency | coach | other
response_voice: "conversational"    # formal | conversational | warm
pricing:
  - service: "Logo design"
    price: "$350 USD"
available_hours: "Mon–Fri 9am–6pm"
escalation_contact: "@you"
```

---

## Usage

Pass any incoming client message to Claude with the skill loaded:

**Input:**
```
Hola, cuánto cobras por un logo?
```

**Output:**
```
Intent:     QUOTE
Confidence: HIGH
Escalate:   NO

Response:
"¡Hola! El diseño de logo está en $350 USD e incluye 3 propuestas iniciales
+ 2 rondas de ajustes. ¿Te cuento cómo funciona el proceso?"
```

---

## Intents handled

| Intent | Trigger signals | Action |
|---|---|---|
| `BOOKING` | agendar · cita · disponibilidad · cuándo | Availability response |
| `QUOTE` | precio · cuánto · costo · presupuesto | Configured pricing response |
| `INFO` | cómo funciona · qué incluye · explícame | Informational response |
| `COMPLAINT` | problema · mal · queja · decepcionado | **Escalate to operator** |
| `OBJECTION` | no sé si · duda · pero · aunque | Objection-handling response |
| `ACK` | gracias · ok · recibido · confirmado | Brief acknowledgment |
| `UNKNOWN` | anything else | **Flag for operator review** |

> COMPLAINT and UNKNOWN always escalate. The skill never auto-responds to these.

---

## Real case

A one-person beauty salon was spending 3–4 hours/day responding to WhatsApp. After deploying this skill with [n8n-mcp](https://github.com/czlonkowski/n8n-mcp) and GreenAPI:

- Booking requests → handled automatically
- Quote questions → answered in seconds
- Complaints → flagged and escalated in real time
- Operator time on messaging → dropped to 20 min/day (review only)

Deployed in 48 hours. Running continuously since day one.

See [`examples/beauty-salon.md`](examples/beauty-salon.md) for the full setup breakdown.

---

## Pair with

| Skill | What it adds |
|---|---|
| [n8n-mcp](https://github.com/czlonkowski/n8n-mcp) | Connect to WhatsApp, automate message delivery via n8n |
| [n8n-skills](https://github.com/czlonkowski/n8n-skills) | Build the automation workflows that power the routing |
| [skill-creator](https://github.com/anthropics/claude-plugins-official) | Encode your full business methodology into Claude |
| [personal-productivity](https://github.com/refoundai/lenny-skills) | Structure the rest of your week with the same logic |

---

## License

MIT — use it, modify it, build on it.

---

Built by [Brayan Oviedo](https://github.com/Brayan-Oviedo)
