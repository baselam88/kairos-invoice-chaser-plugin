---
name: kairos-invoice-chaser
description: Chase an overdue invoice with a polite, systematic reminder cadence. Use when the user has an unpaid invoice past its due date, wants a reminder message for a late payer, or is spending their own time chasing money that's already been earned.
---

# Invoice Chaser

Owners chase late invoices manually — or not at all — and cash
gets trapped. This skill runs a polite 3-stage reminder cadence for
one overdue invoice at a time: a friendly reminder, a firm
reminder, and a final notice, staged by how overdue the invoice is.
Every reminder is a draft — the user reviews and sends each one
themselves.

## How to run it

1. Gather the invoice details from the user (ask only for what's
   missing — never guess a value):
   - `customerName` — who owes the invoice
   - `senderName` and `businessName` — the sign-off
   - `invoiceNumber`, `amount` and `currency` (USD, CAD, GBP, EUR,
     AUD)
   - `dueDaysAgo` — days since the due date (0 = due today)
   - optional: `workDescription`, `paymentInstructions` (how to
     pay), `tone` (friendly / professional / direct), and
     `paymentTerms` — the user's OWN terms (e.g. "Net 30"), which
     are quoted verbatim and only if supplied
2. Call `kairos_invoice_chaser_plan`. It returns the draft for the
   stage the invoice is at, plus the full cadence and a `state`
   value. Show the user the current-stage draft; they send it when
   ready.
3. Afterward, report the outcome via `kairos_invoice_chaser_next`
   with the `state` from the previous result (pass it back
   unchanged):
   - `no_response` — returns the next stage's draft; after stage 3
     the cadence closes and follow-up becomes the user's personal
     call
   - `promised_payment` — closes with a thank-you draft
   - `paid` — closes with a payment-received note
   - `partial_payment` (with `paidAmount`) — drafts an
     acknowledgement showing the remaining balance; the cadence
     stays open for the balance
   - `disputed` — stops the cadence immediately and escalates to
     the user. No further reminders are drafted for that invoice.

## Presenting results

Relay drafts exactly as the tool returns them — the user edits
before sending. Name the stage so the user knows where the invoice
sits in the cadence.

## Hard rules

- **Drafts only.** Never send a reminder on the user's behalf, and
  never claim one was sent.
- **Never threaten, and never invent consequences.** No late fees,
  interest, legal action, collection agencies, or credit reporting
  may be added by you — in a draft or in chat — unless the user
  states it is in their own terms, in which case it is their words,
  passed through the `paymentTerms` field verbatim.
- **Never promise a collection outcome.** This tool drafts
  reminders; it does not collect payments. If you mention the
  time or payment-speed figures, use only the estimate the tool
  returns, with its ESTIMATE label attached.
- **Never waive, discount, or write off any part of an amount.**
  A dispute or a request for different terms is the user's own
  decision, in person — escalate, don't draft around it.
- **Never invent invoice details.** Amounts, dates, invoice
  numbers and names come from the user, not from you.
- If a tool call errors (expired or invalid state), say so plainly
  and offer to start a fresh cadence — don't paper over it.
