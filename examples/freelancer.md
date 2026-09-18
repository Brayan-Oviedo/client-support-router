# Example: Freelancer / Solo Operator

**Business type:** `freelancer`
**Voice:** `conversational`
**Stack:** client-support-router + skill-creator (for methodology encoding)

## Config used

```yaml
business_name: "Estudio Digital"
service_type: "freelancer"
response_voice: "conversational"
pricing:
  - service: "Diseño de logo"
    price: "$350 USD"
  - service: "Landing page"
    price: "$600 USD"
  - service: "Bot WhatsApp"
    price: "$400 USD"
available_hours: "Lun–Vie 9am–5pm"
escalation_contact: "@operator"
```

## Message examples

**QUOTE:**
```
Input:  "Hola, cuánto cuesta hacer una landing page?"
Intent: QUOTE / Confidence: HIGH / Escalate: NO
Response: "¡Hola! La landing page está en $600 USD e incluye diseño, desarrollo
           y un mes de soporte. ¿Me cuentas para qué producto o servicio es?"
```

**INFO:**
```
Input:  "Cómo es el proceso para contratar?"
Intent: INFO / Confidence: HIGH / Escalate: NO
Response: "El proceso es: llamada de 30 min para entender qué necesitas → propuesta
           con alcance y precio → depósito del 50% para empezar → entrega en el
           plazo acordado. ¿Tienes algo específico en mente?"
```

**OBJECTION:**
```
Input:  "Es que no sé si es el momento, tengo dudas"
Intent: OBJECTION / Confidence: HIGH / Escalate: NO
Response: "Entiendo. La mayoría de personas que trabajan conmigo llegaron en el
           mismo punto — querían avanzar pero no sabían por dónde empezar.
           ¿Qué es lo que más te genera duda?"
```

## Why this works for solopreneurs

A solo operator cannot respond to every message in real time without becoming the bottleneck. This skill separates:

- **Routine messages** (BOOKING · QUOTE · INFO · ACK) → handled automatically
- **Sensitive messages** (COMPLAINT · UNKNOWN) → always reach the operator

The result: the operator reviews a filtered queue of what actually needs them, not every incoming message.

## Pair with skill-creator

After configuring this skill, use [skill-creator](https://github.com/anthropics/claude-plugins-official) to encode deeper business rules:
- Your negotiation style
- Your objection-handling methodology
- Project scoping questions you always ask

The two skills together make Claude operate with your full decision-making logic, not just routing.
