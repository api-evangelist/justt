---
name: Submit evidence for a Justt chargeback
description: Upload an evidence file and submit it against an open chargeback, then poll the asynchronous submission to completion.
api: openapi/justt-rest-api-openapi-original.json
operations:
  - FilesController_create
  - EvidenceController_submitEvidence
  - EvidenceController_getEvidenceSubmissionStatus
  - ChargebackItemController_getChargeback
---

# Submit evidence for a Justt chargeback

Base URL `https://api.justt.ai/v1`. Every request needs
`Authorization: Bearer <api-key>` and `Content-Type: application/json`, over HTTPS
only. If the key spans several merchants, set the `reference-account-id` header to
pick the account.

## Steps

1. **Confirm the chargeback is still open.** `GET /chargebacks/{id}`
   (`ChargebackItemController_getChargeback`). Read `pspStatus`; only
   `needs_response` is actionable. `under_review`, `won` and `lost` are terminal
   for this purpose.

2. **Upload the file.** `POST /files` (`FilesController_create`) as
   `multipart/form-data`. The file field **must** be named exactly `file` — using
   `image` or `attachment` returns 400. Set `purpose` to `evidence_file` or
   `evidence_image`. File names are capped at 100 characters. The response returns
   `fileId` and a checksum.

3. **Submit it.** `POST /chargebacks/{id}/evidence/submit`
   (`EvidenceController_submitEvidence`) with body `{"fileId": "<fileId>"}`. This
   returns 201 immediately with a `submitEvidenceId`; the actual submission to the
   PSP happens in the background and can take up to 24 hours.

4. **Poll to completion.** `GET /chargebacks/{id}/evidence/submit/{submitEvidenceId}`
   (`EvidenceController_getEvidenceSubmissionStatus`). `status` moves through
   `created` → `inProgress` → `succeeded` or `failed`. On `failed`, read the
   free-text `error` field. Prefer subscribing to the `chargeback.evidence.submitted`
   webhook over tight polling.

## Rules

- **This step cannot be undone.** No cancel, withdraw or replace operation exists
  for a submitted evidence package. Verify the file before step 3.
- **There is no idempotency key.** If step 2 or 3 times out, do **not** blindly
  retry — a repeated `POST /files` creates a second file, and a repeated submit
  starts a second submission. Re-read the chargeback or the submission status first.
- **Rate limit** is 1000 requests/minute; exhaustion returns 429 with no
  `Retry-After` header, so implement your own exponential backoff.
- **Errors** come back as `{status, message, errorId}`. Quote `errorId` to Justt
  support. Retry 5xx with backoff; do not retry 400 or 404.
- Dates are ISO 8601 UTC or Unix seconds; currency is ISO 4217; never send `null`
  — omit the field instead.
