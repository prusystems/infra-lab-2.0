# Lab 2.0 – Hybrid Cloud Resilience Platform (Healthcare Specialty Vendor)

This repo contains a hands-on infrastructure lab for a **fictional medium-sized healthcare supply company** modernizing from on-prem Windows to Azure.

The goals:

- Design and deploy a **resilient, autoscaling platform** using:
  - Azure + AKS (Kubernetes)
  - Linux VMs (DB / bastion / ops)
  - Cloudflare (and simulated multi-CDN with Akamai-style failover)
  - Terraform from macOS
- Support **React + Python** apps for distributed teams (US & Canada).
- Model **cost, resilience, and downtime risk** vs a serverless alternative.
- Prove full lifecycle: **deploy → scale → fail → recover → destroy → redeploy**.

---

## Scenario

**Company:** family-owned medical office supply business that grew into a trusted name in **specialty equipment design and sourcing** for chiropractors, massage therapists, optical practices, and allied health clinics.

They:

- Ran on **on-prem Windows + AD** for years.
- Now have suppliers worldwide and staff across **US + Canada**.
- Are building **value-added apps** for small healthcare specialties:
  - inventory and ordering
  - device tracking
  - scheduling and reporting

This lab represents their **cloud migration and modernization** journey.

---

## High-Level Architecture

- **Edge / CDN Layer**
  - Cloudflare DNS + CDN + WAF (primary)
  - Secondary CDN pattern (Akamai-style failover, simulated if needed)

- **Application Layer (Azure)**
  - AKS (Kubernetes) for:
    - React frontend
    - Python APIs
  - Autoscaling with HPA + AKS cluster autoscaler
  - Time-zone-aware capacity planning (East → West business hours)

- **Data & Infra Layer**
  - Linux VMs:
    - `db-vm-01` (Postgres or similar)
    - `bastion-vm`
    - optional `ops-vm` for logging/monitoring
  - Azure storage (Blob) for static assets/backups

- **Identity**
  - Azure AD / Entra ID for SSO and RBAC (simulated in lab)

---

## Repo Structure (planned)

```text
infra-lab-2.0/
├── README.md
├── PROJECT-OUTLINE.md
├── STATUS.md
├── SECURITY.md
├── providers.tf
├── versions.tf
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars.example
│
├── modules/
│   ├── network/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── aks/
│   ├── linux-vms/
│   ├── dns-cdn/
│   └── storage/
│
└── docs/
    ├── architecture-diagram.md
    └── resilience-tests.md
```

## Status
- See STATUS.md for current phase and next steps.
- See PROJECT-OUTLINE.md for the full roadmap.

## Tech Stack
- Infra: Azure, Terraform, AKS, Linux VMs
- Delivery: Cloudflare (DNS/CDN/WAF), simulated multi-CDN failover
- Apps: React (frontend), Python (APIs)
- Ops: HPA, cluster autoscaler, scheduled scaling, runbooks
This is a learning + portfolio lab, not production infrastructure.
