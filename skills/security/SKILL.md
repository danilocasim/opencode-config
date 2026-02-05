---
name: security
description: Security checklist and safe patterns across common stacks
---

# Security Skill

Use this when auditing or making security-sensitive changes.

## Universal checklist

- Validate and sanitize inputs at boundaries (HTTP, CLI, jobs, queues)
- Avoid secrets in logs
- Principle of least privilege (tokens, DB roles, IAM)
- Safe error handling (no stack traces / internals to users)
- Dependency hygiene (pin, audit, update)

## Web apps

- AuthN/AuthZ: deny by default
- CSRF protection for cookie-based auth
- XSS: escape outputs, avoid dangerouslySetInnerHTML
- SSRF: restrict outbound HTTP destinations
- File uploads: size limits, type validation, storage isolation

## APIs

- Rate limit sensitive endpoints
- Use consistent error responses
- Avoid leaking existence (user enumeration)

## Data

- Encrypt secrets at rest
- Avoid storing raw tokens
- Use rotation-ready credential design
