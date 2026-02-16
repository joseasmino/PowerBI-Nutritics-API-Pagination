# Power BI – Nutritics API Pagination (Cloud Compatible)

This repository documents the implementation of Nutritics API ingestion in Power BI Service using native M Query pagination without requiring an on-premises gateway.

---

## Objective

Enable API-based data ingestion from the Nutritics endpoint in Power BI Service (Web), supporting pagination beyond the API’s 100-record limit per request while allowing scheduled cloud refresh.

---

## Background

- Nutritics API limits responses to **100 records per request**.
- Initial implementation used Python and worked locally.
- Power BI Service does not execute Python natively.
- Dynamic URLs in M Query disable scheduled refresh.
- Power BI Service enforces a **4-minute timeout per query**.

To ensure cloud compatibility:
- A static base URL must be used.
- Query parameters must be defined using the `Query` record in `Web.Contents`.

---

## Implementation Approach

### 1. Static Base URL Pattern

To avoid Dynamic Data Source errors:

```m
Web.Contents(
    BaseUrl,
    [
        Query = [...]
    ]
)
