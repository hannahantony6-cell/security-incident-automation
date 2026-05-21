#  Security Incident Response Automation

An automated security incident response pipeline built with n8n that 
detects alerts, classifies severity using AI, creates Jira tickets, 
notifies the team on Slack and generates incident reports automatically.

##  What it does
- Receives security alerts via webhook
- AI classifies severity as CRITICAL / HIGH / LOW using LLaMA 3
- Auto-creates Jira tickets with full incident details
- Sends real-time Slack notifications to #incidents channel
- Generates structured incident reports automatically
- End-to-end response time under 30 seconds

##  Tech Stack
- **n8n** — workflow automation (self-hosted via Docker)
- **Groq API** — LLaMA 3.3 70B for AI classification
- **Jira REST API** — automatic ticket creation
- **Slack Webhooks** — real-time team notifications
- **Docker** — local deployment
- **JavaScript** — custom report generation

##  Pipeline Architecture
Security Alert (Postman/GitHub)
↓
n8n Webhook (trigger)
↓
Groq AI (LLaMA 3) — classifies severity
↓
Jira API — creates ticket automatically
↓
Slack Webhook — notifies #incidents channel
↓
JavaScript Code — generates incident report
↓
Slack — delivers full formatted report

##  How to run this project
1. Install Docker Desktop
2. Run n8n:
docker run -it --rm --name n8n -p 5678:5678 n8nio/n8n
3. Open `http://localhost:5678`
4. Import `workflow.json` into n8n
5. Add your API credentials:
   - Groq API key (free at console.groq.com)
   - Jira email + API token
   - Slack incoming webhook URL
6. Activate the workflow
7. Send a test request via Postman

##  Demo

<img width="1918" height="920" alt="image" src="https://github.com/user-attachments/assets/3f516d2f-f16a-4590-aa90-7eb47ccd3ed2" />

<img width="1918" height="907" alt="image" src="https://github.com/user-attachments/assets/02059bc6-398d-4971-8100-ac9002ef9169" />

<img width="1918" height="952" alt="image" src="https://github.com/user-attachments/assets/325f246a-785f-4960-9b64-274a2d54ee67" />

<img width="1917" height="1025" alt="image" src="https://github.com/user-attachments/assets/c0626ea2-937e-4e2e-97a9-9252a41430ad" />







##  Sample Alert Payload
```json
{
  "event_type": "secret_scanning_alert",
  "repository": "my-project",
  "severity": "high",
  "description": "AWS access key exposed in commit abc123",
  "timestamp": "2026-05-21T10:30:00Z",
  "actor": "john_dev"
}
```

## 📋 Sample Output
- Jira ticket auto-created (SCRUM-10)
- Slack notification sent to #incidents
- AI Classification: CRITICAL
- Full incident report generated in under 30 seconds


