---
name: oper-add-offer-with-documents
description: Simulate and attach a mortgage offer to an existing Oper Connect loan
  request and upload supporting documents, grounded in real operationIds.
api: Oper Connect API
source: openapi/oper-api.json
generated: '2026-07-20'
method: generated
operations:
- api_simulators_offers_create
- api_loan_requests_offers_create
- api_loan_requests_offers_list
- api_loan_requests_documents_create
---

# Add an offer and documents to a loan request

Use this skill once a loan request exists (see `oper-create-loan-request`).

## Steps

1. **Authenticate** with a bearer JWT (`POST /api/jwt/`).
2. **Simulate an offer.** `POST /api/simulators/offers/`
   (`api_simulators_offers_create`) to compute offer terms before committing.
3. **Create the offer on the loan request.**
   `POST /api/loan-requests/{loan_request_id}/offers/`
   (`api_loan_requests_offers_create`).
4. **Upload supporting documents.**
   `POST /api/loan-requests/{loan_request_id}/documents/`
   (`api_loan_requests_documents_create`) for each proof/document.
5. **List offers to confirm.**
   `GET /api/loan-requests/{loan_request_id}/offers/`
   (`api_loan_requests_offers_list`).

## Conventions & notes

- All calls require `Authorization: Bearer <token>`.
- Error payload shapes are not modeled in the OpenAPI; treat non-2xx responses
  defensively.
- Document and offer objects are proprietary to their loan request and cannot be
  shared across requests.
