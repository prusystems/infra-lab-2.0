# Security Policy – Lab 2.0

This repo is an educational / portfolio lab, not production infrastructure.

## Data & Secrets

- No production data.
- No PHI / healthcare records.
- No real customer data.
- No real internal company configs.

**Secrets must never be committed**, including:

- Cloud provider credentials
- Terraform backend credentials
- kubeconfig files
- API tokens (Cloudflare, GitHub, etc.)
- Database passwords or connection strings

Use:

- Local environment variables
- Secret stores (e.g., Azure Key Vault)
- `.gitignore` for:
  - `*.tfvars`
  - `*.kubeconfig`
  - any local config files containing secrets

## Scope

This repo:

- Models infrastructure patterns for a fictional company.
- Is intended to showcase design, IaC, resilience, and documentation skills.
- Should remain safe to share publicly.

If you ever adapt this work for real infrastructure:

- Move secrets to a proper secret manager.
- Use private repos for org-specific configs.
- Follow your org’s security and compliance policies.
