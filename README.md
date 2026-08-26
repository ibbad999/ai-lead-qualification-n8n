 AI Lead Qualification & Routing Automation

An AI-powered lead qualification workflow built with **n8n** and the **Gemini API** that automatically analyzes incoming leads, classifies them, and routes them to the appropriate business systems.

The goal is to reduce manual lead processing and help businesses respond faster to high-value opportunities.

---

 What It Does

The workflow receives a lead through a webhook and uses Gemini to analyze the submitted message.

It then:

1. Receives the lead through a webhook
2. Sends the lead message to Gemini for classification
3. Validates and structures the AI response
4. Determines whether the lead is a hot lead
5. Routes hot leads to Slack
6. Logs other leads to Google Sheets
7. Generates a personalized follow-up email for hot leads
8. Creates the follow-up as a Gmail draft for review

### Workflow

```text
Lead Submission
       ↓
    Webhook
       ↓
   Gemini AI
       ↓
Classification & Validation
       ↓
   Hot Lead?
    ↙       ↘
  YES        NO
   ↓          ↓
 Slack     Google Sheets
   ↓
Gemini Email Draft
   ↓
Gmail Draft

```

##  AI Classification

Gemini analyzes each incoming lead message and returns a structured JSON response:

```json
{
  "is_hot": true,
  "urgency": "high",
  "category": "sales",
  "reasoning": "Strong purchase intent and urgent timeline."
}
```

The workflow validates the AI response before using it for downstream routing.

### Supported Categories

- `sales`
- `support`
- `spam`
- `other`

### Urgency Levels

- `low`
- `medium`
- `high`


| Technology            | Purpose                              |
| --------------------- | ------------------------------------ |
| **n8n**               | Workflow automation                  |
| **Google Gemini API** | AI classification & email generation |
| **REST API**          | Communication with Gemini            |
| **Webhooks**          | Lead intake                          |
| **Slack**             | Hot lead notifications               |
| **Google Sheets**     | Lead logging                         |
| **Gmail**             | Follow-up email drafts               |
| **JavaScript**        | Data processing & validation         |


##  Example Input

A lead can be submitted through the webhook using a structure such as:

```json
{
  "name": "Ali Khan",
  "email": "ali@example.com",
  "message": "We need help improving our website and would like to discuss the project this week."
}
```

##  Example AI Output

```json
{
  "is_hot": true,
  "urgency": "high",
  "category": "sales",
  "reasoning": "Strong project intent with an immediate timeline."
}
```
