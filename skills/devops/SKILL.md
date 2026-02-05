---
name: devops
description: DevOps, CI/CD, and infrastructure conventions
---

# DevOps & CI/CD Conventions

High-level patterns for Docker, CI, and cloud infra.

## Docker

- Use small base images (alpine/distroless when appropriate)
- Multi-stage builds for production images
- Avoid baking secrets into images
- Prefer health checks and explicit entrypoints

## CI/CD

- Separate **lint/test/build** steps
- Cache dependencies safely
- Fail fast on lint/test errors
- Keep pipelines deterministic and reproducible

## Infrastructure

- Infrastructure as Code (Terraform, CloudFormation, etc.)
- Principle of least privilege for all credentials
- Separate staging/production with clear promotion flow

Use this skill as a reference when the debugger or optimizer needs to touch CI, Dockerfiles, or deployment configs.
