Consent-based home valuation lead capture
A small lead-capture system for South African estate agents. A homeowner opts in on a landing page, the lead is stored in a CRM, the agent is alerted, and the agent follows up with a valuation (CMA).
Built as a pilot with Claude (Anthropic), Make and Notion. Status: pilot in progress, not production-ready.
How it works
Landing page (index.html): owner enters their details, chooses whether they want a free valuation (Yes/No), says whether they are thinking of selling, ticks the contact channels they allow, and gives consent. The page records the consent wording and timestamp.
Webhook: the form posts to a Make webhook.
Intake scenario (Make): drops spam and non-consented entries, creates a row in a Notion database, and emails the agent an alert.
Agent follow-up: the agent adds real comparable sales to the lead record and sends the valuation report.
What works and what does not (honest status)
Part
Status
Landing page with consent capture
Built
Webhook to Notion row and agent alert
Tested once with a dummy lead; a single request fired the scenario four times, so duplicate protection is still needed
Confirmation email to the owner
Not working: the Gmail connection type did not match Make's send-email step
Automatic deletion of leads after 6 months
Not working: the Notion query step returned an error
CMA generation
Manual: comparable sales must come from a licensed data source. The system does not invent comps
WhatsApp and SMS
Not built. WhatsApp needs a Business API provider and Meta-approved templates
Setup
Create a Make webhook and paste its URL into WEBHOOK_URL in index.html.
Replace every bracketed placeholder ([Agent name], [Agency name], [privacy email], and the details in privacy-notice.html).
Create a Notion database with: name, address, cell, email, valuation requested, selling intent, consent given, consent text, consent time, status.
Host index.html and privacy-notice.html in the same folder on a public HTTPS site.
Compliance notes (South Africa)
This design relies on opt-in. Cold messaging to purchased owner lists risks breaching POPIA and the ECTA direct-marketing rules.
The privacy notice is a draft and has not been reviewed by an attorney. Get legal review, including on cross-border data transfers, before using it.
Do not use a published webhook URL in a public repo: anyone can send junk to it.
This is not legal advice.
Licence
Add a licence of your choice before others reuse this.