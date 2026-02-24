# SolarRun

## Solar Installation Company Reception List Agent

This repository now contains a practical blueprint for a **reception list agent** that helps a solar installation company intake and triage incoming leads.

### What this agent does

- Greets inbound callers/chats and captures contact details.
- Identifies request type (new quote, service issue, billing, permitting, partnership, other).
- Collects site and energy context for sales qualification.
- Applies priority/urgency rules and routes the case to the correct team.
- Produces a clean structured record for CRM entry and follow-up.

### Intake fields (minimum)

1. Full name
2. Phone number
3. Email
4. Service address
5. Homeowner status (owner/tenant)
6. Property type (single family, multifamily, commercial)
7. Utility provider
8. Average monthly electric bill
9. Roof type/age + shading notes
10. Reason for contact
11. Preferred callback time
12. Consent to contact (SMS/email)

### Routing rules

- **Sales (new install/quote):** lead has valid contact info and install intent.
- **Service:** existing system issue, inverter alert, monitoring offline, production drop.
- **Billing/Admin:** payment, invoices, financing, document requests.
- **Permitting/Project Ops:** HOA/permitting/interconnection timeline questions.
- **Emergency escalation:** electrical hazard, fire risk, exposed wiring, water ingress near electrical components.

### Example agent prompt

Use the following as a starter system prompt for your receptionist agent:

> You are the reception agent for a solar installation company. Be concise, polite, and safety-aware. Collect all required intake fields before ending the conversation unless the customer refuses. If there is potential electrical danger, immediately advise the customer to contact emergency services and escalate to on-call operations. Always summarize captured details and confirm the best callback window.

### Structured output example (JSON)

```json
{
  "contact": {
    "name": "Jane Doe",
    "phone": "+1-555-0100",
    "email": "jane@example.com"
  },
  "address": "1207 Elm St, Sacramento, CA 95814",
  "property": {
    "owner_status": "owner",
    "type": "single_family",
    "roof_notes": "composite shingle, ~8 years old, little shading"
  },
  "utility": {
    "provider": "SMUD",
    "avg_monthly_bill_usd": 210
  },
  "intent": "new_install_quote",
  "priority": "normal",
  "callback_window": "Weekdays after 4:30 PM",
  "consent": {
    "sms": true,
    "email": true
  },
  "handoff_team": "sales"
}
```

### KPI suggestions

- Intake completeness rate
- First-response SLA adherence
- Qualified lead rate
- Appointment booking conversion
- Misroute rate
- Safety escalation response time

### Next implementation steps

1. Add this schema to your CRM form.
2. Integrate telephony/chat source tags.
3. Add automated routing to sales/service/admin queues.
4. Add dashboard tracking for KPI metrics.
