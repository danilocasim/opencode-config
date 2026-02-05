---
name: api
description: REST/OpenAPI conventions, error shapes, pagination, and versioning
---

# API Conventions

## Errors

- Use consistent JSON error shapes
- Prefer stable error codes over string matching
- Avoid leaking internals

## Pagination

- Prefer cursor pagination for large datasets
- Provide `next_cursor` and `has_more`

## Versioning

- Prefer URL versioning (`/v1/...`) or header versioning
- Avoid breaking changes in-place

## OpenAPI

- Keep spec in sync
- Include examples and error responses
