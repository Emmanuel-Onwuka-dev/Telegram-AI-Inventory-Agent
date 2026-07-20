# Telegram-AI-Inventory-Agent
📦Telegram AI Inventory Agent
A conversational inventory manager: message it in plain English on Telegram, and it reads, updates, and reports on your Google Sheets inventory in seconds. No spreadsheet to open, no form to fill.
## Why
Inventory tracking usually means opening a spreadsheet, finding the right row, and manually editing it, even for a quick check like "how many eggs do we have left?" This agent removes that friction entirely: you just ask, the same way you'd message a coworker.

## Workflow diagram
<img width="1523" height="588" alt="Telegram AI inventory assistant" src="https://github.com/user-attachments/assets/2d23b08e-8413-4aaf-b12c-3c3040ca90a4" />


## How it works
**Trigger**: Incoming Telegram message from the user
**Receive query** — captures the user's message on Telegram
**Wait** — brief pause before processing
**Inventory AI Agent (Gemini Flash)** — interprets the intent of the message (add stock, check stock, update stock, etc.)
**Memory layer** — retains conversation context, so follow-up messages don't need to repeat earlier details
**Tools available to the agent:**
**Lookup tool** — reads current inventory from Google Sheets
**Append/update tool** — writes new or updated inventory rows, including auto-generated descriptions
**Response branch:**
**Success** → replies to the user directly on Telegram with the requested info or confirmation
**Error** → routes to error handling instead of failing silently
**Error handling:**
Emails an alert to the admin/engineer via Gmail
Checks whether the error is a rate limit ("too many requests") vs. another failure type, and notifies accordingly via separate Telegram alerts
## Example interaction
<img width="1227" height="790" alt="Telegram ai inventory chat" src="https://github.com/user-attachments/assets/a3f101cd-f0ea-41f8-a638-d2744f0e58ad" />
<img width="973" height="652" alt="Telegram ai inventory sheet" src="https://github.com/user-attachments/assets/d797f55e-77f3-4de7-ae89-78f587ab4fe0" />

## Stack
**n8n** — orchestration
**Google Gemini (Flash)** — natural language understanding / agent brain
**Google Sheets** — inventory database
**Telegram** — user interface
**Gmail** — admin error alerts
**Simple Memory** — conversation context retention
## Setup
Import `workflow.json` into n8n
Connect the following credentials:
Telegram Bot (+ chat ID)
Google Gemini API
Google Sheets (with access to your inventory sheet)
Gmail (for error alerts)
Point the Lookup and Append/Update tools at your own Google Sheet
Activate the workflow
## Known limitations
Relies on Gemini correctly interpreting free-text intent; very ambiguous phrasing may need a follow-up clarifying message
Rate limits from the AI provider are caught and surfaced as a distinct alert type, but heavy concurrent use could still cause delays
Inventory sheet must follow a consistent column structure for the lookup/append tools to work correctly
## License
MIT — feel free to use or adapt this workflow.
