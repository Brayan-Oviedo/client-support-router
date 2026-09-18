# Example: Beauty Salon

**Business type:** `beauty_salon`
**Voice:** `warm`
**Stack:** client-support-router + n8n-mcp + GreenAPI (WhatsApp)

## Config used

```yaml
business_name: "Estética Glamour"
service_type: "beauty_salon"
response_voice: "warm"
pricing:
  - service: "Corte de cabello"
    price: "$35.000 COP"
  - service: "Tinte completo"
    price: "$80.000 COP"
  - service: "Manicure"
    price: "$25.000 COP"
available_hours: "Mar–Sáb 9am–6pm"
escalation_contact: "@owner"
```

## Message examples

**BOOKING:**
```
Input:  "Hola! Quiero agendar una cita para corte"
Intent: BOOKING / Confidence: HIGH / Escalate: NO
Response: "¡Hola! 💇‍♀️ Claro que sí. Tenemos disponibilidad martes a sábado de 9am a 6pm.
           ¿Qué día te queda mejor para agendarte?"
```

**QUOTE:**
```
Input:  "Cuánto cuesta el tinte?"
Intent: QUOTE / Confidence: HIGH / Escalate: NO
Response: "¡Hola! El tinte completo está en $80.000 COP e incluye lavado y secado.
           ¿Te cuento qué marcas manejamos?"
```

**COMPLAINT:**
```
Input:  "El corte que me hicieron quedó mal, estoy muy molesta"
Intent: COMPLAINT / Confidence: HIGH / Escalate: YES
Response: ESCALATED
Note (operator): "Cliente insatisfecha con resultado de corte. Requiere atención personal.
                  No responder automáticamente."
```

## Results after 48h deployment

- WhatsApp response time: from 2–4 hours → under 2 minutes
- Owner time on messaging: from 3h/day → 20 min/day (review only)
- Complaints handled: 100% escalated, 0 auto-responses on sensitive cases
- Booking conversion via WhatsApp: maintained, no drop
