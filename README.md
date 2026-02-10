# AI Lead Qualification & Follow‑Up Automation

A production‑style demo that shows how to **capture leads, qualify them with AI, take automated actions, and expose a full execution timeline** — built to demonstrate real‑world AI workflow automation skills, not a toy chatbot.

---

## ⚠️ Note

This repository contains architecture documentation and pseudocode only.
The live demo and source code are private and shared selectively with clients.

---

## Diagram

## ![Workflow Diagram](/diagrams/flow.png)

## What This Project Demonstrates

This system shows how to build an **AI‑driven automation pipeline** that:

- Accepts leads from a **web form or external APIs**
- Validates and normalizes incoming data
- Uses **OpenAI** to classify intent, priority, and next action
- Automatically stores qualified leads (Google Sheets as CRM demo)
- Sends personalized follow‑up emails
- Logs every step for transparency and debugging

This is the same architectural pattern used in:

- CRM automations
- Sales qualification systems
- Internal ops workflows
- AI decision engines

---

## High‑Level Architecture

```
Form / API / Webhook
        ↓
Validation
        ↓
Normalization
        ↓
AI Decision Engine (OpenAI)
        ↓
Business Rules
        ↓
Storage (CRM)
        ↓
Email / Side Effects
        ↓
Process Logging (Observability)
```

The same `processLead()` pipeline is reused across:

- **Server Actions** (web form)
- **API Routes** (`POST /api/leads`) for external systems

---

## Core Features

### 1. AI Lead Qualification

Uses OpenAI to determine:

- Lead intent (pricing, demo, automation request, etc.)
- Category (sales / support / other)
- Priority (low / medium / high)
- Confidence score (0.0 – 1.0)
- Recommended system action

Decisions are deterministic and schema‑validated.

---

### 2. Automated Follow‑Up Emails

If a lead is relevant:

- A professional follow‑up email is generated automatically
- Email is sent without manual intervention

If the lead is not a fit:

- No email is sent
- Lead is ignored safely

---

### 3. CRM Storage (Demo)

Qualified leads are appended to **Google Sheets** to simulate CRM storage.

This can be easily replaced with:

- HubSpot
- Airtable
- Notion
- Supabase
- Internal databases

---

### 4. Execution Timeline (Observability)

Every step is logged:

- Step name
- Status
- Message
- Details
- Timestamp

A built‑in result page displays the **full execution timeline**, making AI decisions transparent and debuggable.

---

## API Usage (External Platforms)

### Endpoint

```
POST /api/leads
```

### Example Request Body

```json
{
  "event": "website_form",
  "source": { "platform": "postman" },
  "lead": {
    "full_name": "John Doe",
    "email": "john@example.com",
    "message": "We want to automate lead handling",
    "company": "Acme Inc"
  }
}
```

### Example Response

```json
{
  "status": "success",
  "processLog": [
    {
      "step": "Lead Qualification by AI",
      "status": "Success",
      "message": "Lead is successfully qualified by AI",
      "time": "2026-02-09T12:30:10.000Z"
    }
  ]
}
```

This endpoint allows the system to be triggered from:

- Postman
- Webhooks
- External forms
- Automation tools

---

## Tech Stack

- **Next.js (App Router)** – Server Actions + API Routes
- **React 19**
- **Tailwind CSS v4**
- **OpenAI Responses API** (structured JSON output)
- **Google Sheets API** (CRM demo)
- **Resend** (email delivery)
- **Vercel Serverless Architecture**

---

## OpenAI Model Choice

- **Model:** `gpt-4.1-mini`

Chosen because:

- Fast and cost‑efficient
- Reliable structured JSON output
- Ideal for classification and decision workflows

The model can be upgraded easily if more complex reasoning is required.

---

## Important Notes

- The admin execution timeline is **demo‑focused** and currently stores only the latest run.
- In production, logs should be persisted in a database or logging system.
- This project is intentionally modular so each component can be swapped based on client needs.

---

## Intended Use

This project is **not a SaaS product**.

It is a:

- Proof of AI Automation skills
- Reference architecture
- Client demo
- Foundation for custom AI workflow solutions

Each client implementation would be customized based on:

- Data sources
- Business rules
- CRM tools
- Communication channels

---

## Author

**Muhammad Noman**
AI Workflow Automation Specialist (Freelancer)

Focus:

- AI decision systems
- Lead qualification & routing
- CRM & email automation
- API‑driven workflows

---

## License

This project is for demonstration and portfolio purposes.
