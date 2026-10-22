# `senders` Data Table

Create an n8n Data Table named `senders` with these columns:

| Column | Type | Example | Notes |
| --- | --- | --- | --- |
| `sender` | string | `promo@example.com` or `@example.com` | Full address, or a domain |
| `action` | string | `trash` | `trash` or `delete`. Rows with any other value are ignored |

## Matching rules

- **Full address** (`promo@example.com`): matches that exact sender.
- **Domain** (`example.com` or `@example.com`): matches the domain and its
  subdomains on Outlook. On Gmail it is passed into a `from:(...)` search.
- Matching is case-insensitive and ignores surrounding spaces.

Add or remove rows any time; the workflow reads the table on every run.
Setting `action` to something else (for example `keep`) is a simple way to park
a row without deleting it.
