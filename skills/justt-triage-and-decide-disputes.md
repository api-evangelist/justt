---
name: Triage Justt chargebacks and set the fight/accept decision
description: List open chargebacks, read Justt's ROI recommendation, enrich the weak ones, and override the representment decision — escalating acceptance to a human because it is irreversible.
api: openapi/justt-rest-api-openapi-original.json
operations:
  - ChargebackController_findAll
  - ChargebackItemController_getChargeback
  - ChargebackItemController_updateChargeback
  - TransactionController_createTransaction
  - ChargebackItemController_markShouldFight
  - ChargebackItemController_acceptChargeback
  - ChargebackItemController_getAcceptChargebackStatus
---

# Triage Justt chargebacks and set the fight/accept decision

Base URL `https://api.justt.ai/v1`, bearer API key, JSON, HTTPS only.

## Steps

1. **List the work.** `GET /chargebacks` (`ChargebackController_findAll`) with
   `status`, `pspStatus=needs_response`, `psp`, `startDate`/`endDate` and
   `minEnrichmentScore`/`maxEnrichmentScore`. Paginate with `page` and `limit`
   (default 10, max 100) and continue while `hasMore` is true — there is no total
   count, so you cannot size the job in advance.

2. **Read Justt's own recommendation.** Each `ChargebackDto` carries
   `DisputeOptimizationResult` (`Fight` or `Accept`) and an enrichment score. Sort
   your queue by these rather than by amount.

3. **Enrich the thin cases.** For a chargeback Justt cannot yet argue, add data
   points with `PATCH /chargebacks/{id}`
   (`ChargebackItemController_updateChargeback`), and add related purchases with
   `POST /transactions` (`TransactionController_createTransaction`). Both are
   overwrite/upsert semantics, so a wrong value can be corrected by writing the
   right one. The field names come from the account's own data-points list in the
   hub — do not guess them.

4. **Override the decision when you disagree.** `PATCH /chargebacks/{id}/should-fight`
   (`ChargebackItemController_markShouldFight`) with `{"shouldFight": true|false}`.
   This is a boolean override of the contractual default and is its own inverse —
   re-issue with the opposite value to change your mind. Justt does **not** publish
   how long it stays changeable, so treat it as bounded by the PSP evidence
   deadline and act early.

## Stop here without a human

5. **`POST /chargebacks/{id}/accept`** (`ChargebackItemController_acceptChargeback`)
   returns the funds to the cardholder and Justt states plainly: *once accepted, the
   chargeback cannot be reversed.* Never call it autonomously. Require explicit
   human approval per chargeback, then poll
   `GET /chargebacks/{id}/accept` (`ChargebackItemController_getAcceptChargebackStatus`)
   until `status` is `succeeded` or `failed`, or handle the `chargeback.accepted`
   webhook.

## Rules

- No idempotency key exists on any of these writes. Reconcile with a GET before
  retrying a timed-out POST.
- 1000 requests/minute, 429 on exhaustion, no rate-limit headers.
- Set `reference-account-id` when one key serves several merchants — the API has no
  scopes, so the key alone does not constrain which account you touch.
