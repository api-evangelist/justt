---
name: Work Justt pre-chargeback alerts
description: Pull Ethoca and Verifi CDRN/RDR alerts, act on them before they become chargebacks, and report the outcome back to Justt using the networks' own outcome codes.
api: openapi/justt-pre-chargeback-alerts-openapi-original.json
operations:
  - AlertController_findAll
  - AlertController_findOne
  - PreChargebackAlertsController_createOutcome
---

# Work Justt pre-chargeback alerts

A pre-chargeback alert is an early warning from Verifi RDR, Verifi CDRN or Ethoca.
Resolving one — usually by refunding — stops a chargeback from ever being filed.
Base URL `https://api.justt.ai/v1`, bearer API key.

## Steps

1. **Pull the queue.** `GET /pre-chargeback-alerts/alerts`
   (`AlertController_findAll`) by search criteria, paginating with `page`/`limit`
   and continuing while `hasMore`. Justt also supports real-time push of alerts —
   ask your account manager to enable it, and prefer the
   `pre_chargeback_alert.received` webhook over polling.

2. **Read one.** `GET /pre-chargeback-alerts/alerts/{internalAlertId}`
   (`AlertController_findOne`).

3. **Act in your own systems** — refund, cancel, or resolve. Justt does not
   perform the refund through this API; it records what you did.

4. **Report the outcome.** `POST /pre-chargeback-alerts/alerts/outcome`
   (`PreChargebackAlertsController_createOutcome`) with:
   - `providerName` — `Verifi RDR`, `Verifi CDRN` or `Ethoca`
   - `alertId` — Justt's UUID for the alert
   - `refunded` — `refunded`, `not refunded` or `not settled`
   - `outcome` — from the `OutcomeStatus` enum, which carries both readable values
     (`resolved`, `previously_refunded`, `unresolved_dispute`, `stopped`,
     `partially_stopped`, `previously_cancelled`, `missed`, `notfound`,
     `account_suspended`, `in_progress`, `shipper_contacted`, `other`) and the
     alert networks' numeric codes (`100`, `101`, `102`, `130`, `900`, `901`,
     `902`, `940`, `950`–`957`, `951`)
   - `comments` — free text

   If you already speak Ethoca/Verifi outcome codes, send the numeric code you
   already produce; Justt accepts the network vocabulary directly.

5. **Watch the follow-up events.** `pre_chargeback_alert.refund.succeeded` and
   `pre_chargeback_alert.refund.failed` tell you whether the linked transaction
   was actually refunded through the PSP. If you cancel CRM subscriptions on
   refund, also handle `subscription.cancel_immediately.failed` — that one means
   the refund went through but the subscription did not cancel.

## Rules

- Timeliness is the whole point: alerts have short network deadlines. Poll or
  subscribe frequently and report the outcome as soon as you act.
- Reporting an outcome is a plain create with no idempotency key; if it times out,
  re-read the alert before posting again.
- Errors are `{status, message, errorId}`; 1000 requests/minute; 429 on exhaustion
  with no `Retry-After`.
