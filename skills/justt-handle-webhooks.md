---
name: Receive and verify Justt webhooks
description: Stand up a Justt webhook endpoint, verify the Standard Webhooks signature, handle the eleven event types, and behave correctly under Justt's retry schedule.
api: asyncapi/justt-webhook-events-openapi-original.json
operations:
  - chargeback.created
  - chargeback.updated
  - chargeback.status.updated
  - chargeback.evidence.submitted
  - chargeback.accepted
  - pre_chargeback_alert.received
  - pre_chargeback_alert.refund.succeeded
  - pre_chargeback_alert.refund.failed
  - pre_chargeback_alert.transaction_matched
  - subscription.cancel_immediately.success
  - subscription.cancel_immediately.failed
---

# Receive and verify Justt webhooks

Justt pushes eleven event types to an HTTPS endpoint you register in the hub. The
contract is OpenAPI 3.1 with the events under the top-level `webhooks` object.

## Steps

1. **Register the endpoint** in the webhook dashboard and copy its **signing
   secret**. Each endpoint has its own. Subscribe to all events while testing,
   then filter to what you need.

2. **Verify every request before parsing it.** Justt signs with HMAC-SHA256 and
   sends the Standard Webhooks header triple:
   `webhook-id`, `webhook-timestamp`, `webhook-signature`. Compute the signature
   over the **raw** request body — not a re-serialized copy — and allow about
   5 minutes of timestamp skew to defeat replay. On mismatch, return **401** and
   do not process the payload.

3. **Return 2xx fast.** Any 2xx is treated as delivered, even if your body says
   otherwise. The delivery timeout is 15 seconds. Acknowledge first, work after.

4. **Handle the events.**
   - `chargeback.created` — a new dispute arrived from a connected PSP.
   - `chargeback.updated` / `chargeback.status.updated` — field or PSP-status change.
   - `chargeback.evidence.submitted` — read `status`: `succeeded` or `failed`.
   - `chargeback.accepted` — acceptance confirmed by the PSP; `status` `succeeded`
     or `failed`.
   - `pre_chargeback_alert.received` — a CDRN, RDR or Ethoca alert; act before it
     becomes a chargeback.
   - `pre_chargeback_alert.refund.succeeded` / `.failed` — outcome of the refund.
   - `pre_chargeback_alert.transaction_matched` — opt-in only; Justt must enable
     `additional_event_types` on the account.
   - `subscription.cancel_immediately.success` / `.failed` — CRM (Chargebee,
     Recurly) cancellation after a refund. On failure read `failureCode` and
     `failureReason`: **the money left but the subscription is still live**, so
     raise this for manual follow-up.

## Retry behaviour you must design for

- Schedule: immediate, then 5s, 5m, 30m, 2h, 5h, 10h, 10h — eight attempts.
- Retried on any 4xx except 410, any 5xx, timeouts and connection failures.
- **410 Gone is permanent** — return it only when you want delivery to that
  endpoint to stop for good.
- Five consecutive days of total failure auto-disables the endpoint; re-enable it
  by hand in the dashboard.
- Because of retries, **your handler must be idempotent**. Deduplicate on
  `webhook-id`.

## Testing

Drive the whole lifecycle in the sandbox: `POST /sandbox/raw-data`
(`SandboxController_uploadRawData`) with a PSP payload at `needs_response`, then
re-post the same id at `under_review`, then `won` or `lost`. Each transition fires
the matching webhook. Sandbox uses a separate token from production.
