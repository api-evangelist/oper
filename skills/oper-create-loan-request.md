---
name: oper-create-loan-request
description: Create a mortgage loan request in Oper Connect and attach the primary
  borrower (client), grounded in real Oper Connect operationIds.
api: Oper Connect API
source: openapi/oper-api.json
generated: '2026-07-20'
method: generated
operations:
- api_jwt_create
- api_loan_requests_create
- api_loan_requests_clients_create
- api_loan_requests_clients_retrieve
---

# Create a loan request in Oper Connect

Use this skill to open a new mortgage loan request and register its primary borrower.

## Prerequisites

- A tenant user credential (and, on OTP tenants, the phone code).
- Base host: `https://api.opercredits.com` (tenant-routed).

## Steps

1. **Authenticate.** `POST /api/jwt/` (`api_jwt_create`) with the user credentials to
   obtain an access token and refresh token. Send the access token as
   `Authorization: Bearer <token>` on every subsequent call. Refresh with
   `POST /api/jwt/refresh/` when it expires.
2. **Create an empty loan request.** `POST /api/loan-requests/`
   (`api_loan_requests_create`). Per Oper's model, always start from an empty loan
   request; capture the returned `loan_request_id`.
3. **Add the borrower.** `POST /api/loan-requests/{loan_request_id}/clients/`
   (`api_loan_requests_clients_create`) with the borrower details.
4. **Verify.** `GET /api/loan-requests/{loan_request_id}/clients/`
   (`api_loan_requests_clients_retrieve`) to confirm the client is linked.

## Conventions & notes

- Pagination on list endpoints is page-number (`page`, `page_size`) with a
  `count`/`next`/`previous`/`results` envelope.
- No idempotency-key header is documented, so avoid blind retries on POST — check
  with a GET before recreating.
- Loan-request data is anonymised after a tenant-configured retention window (GDPR).
