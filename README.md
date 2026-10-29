# Invoice Chaser — plugin for Grok Bot, Cursor, and MCP hosts

**What it does.** Owners chase late invoices manually — or not at
all — and cash gets trapped in accounts receivable. Give your agent
an overdue invoice and it builds a polite, tracked 3-stage reminder
cadence: a friendly reminder, a firm reminder, and a final notice,
staged by how overdue the invoice is. Report what happens after
each reminder and the cadence advances — and if the customer
disputes the invoice, the cadence stops immediately and hands it
back to you.

Every reminder is a draft. Nothing is ever sent for you; you review
and send each one yourself. Drafts state facts only — the invoice,
the amount, the days overdue, and your own payment terms quoted
verbatim if you supply them. They never threaten, and they never
invent late fees, interest, legal action, or any other consequence.

**Why it matters.** A consistent reminder cadence is benchmarked to
cut average days-sales-outstanding by an ESTIMATED 10–15 days and
save an ESTIMATED 2–4 hours a week of owner chasing time
(AR-automation benchmarks). These are estimates, not promises: this
tool drafts reminders — it does not collect payments and cannot
guarantee any invoice will be paid.

**Tools**

| Tool | Label | What it does |
|---|---|---|
| `kairos_invoice_chaser_plan` | Write | Opens a 3-stage reminder cadence for one overdue invoice and returns the stage-appropriate drafts |
| `kairos_invoice_chaser_next` | Write | Records the outcome (no response / promised / paid / partial / disputed) and advances, pauses, escalates or closes the cadence |

**Configure variables.** None. The endpoint is public and
rate-limited; no key, no sign-in, and no credentials of yours are
ever requested or stored.

**Privacy.** The server stores nothing. Your invoice details travel
between calls inside a signed token your own agent carries, and are
used only to draft the reminders. Nothing is sent anywhere on your
behalf.

## Test locally

The package points at the hosted endpoint in `mcp.json`. To exercise
the tools from any MCP client, add the server from `mcp.json` and
ask your agent to "chase an overdue invoice".

Cursor IDE local load:

```bash
ln -s /path/to/kairos-invoice-chaser ~/.cursor/plugins/local/kairos-invoice-chaser
```

Then reload the window and confirm the `kairos-invoice-chaser`
skill and MCP server load.

## Submit

- Grok Bot / Cursor marketplace: https://x.ai/bot/marketplace/submit-a-plugin
- License: MIT (see LICENSE) — the plugin package is open; the
  reminder service itself is hosted by KAIROS AI Systems.

Built by KAIROS AI Systems — https://kairosasi.com
