# Setup

## 1. Run n8n
See the quick start in the main README.

## 2. Gmail (per account)
1. Create a Google Cloud project and enable the Gmail API.
2. Configure the OAuth consent screen and publish it to production so tokens
   do not expire after 7 days.
3. Create an OAuth client, then add a Gmail OAuth2 credential in n8n.

## 3. Microsoft 365
1. Register a new app in Microsoft Entra.
2. Add an Outlook OAuth2 credential in n8n using that app's client ID/secret.

## 4. Senders table
Create the `senders` Data Table (see [senders-table.md](senders-table.md)).

## 5. Import the workflows
1. Import `workflows/failure-sms-alert.json` and `workflows/mail-cleaner.json`.
2. In `mail-cleaner`, point **Get senders** at your `senders` table and link
   your own Gmail / Outlook credential on each branch. Delete the branches you
   do not need.
3. Set up SMS in the alert workflow (see [sms-providers.md](sms-providers.md)).
4. In `mail-cleaner` settings, set **Error workflow** to `Failure SMS Alert`.
5. Run once manually with a single test sender before publishing.
