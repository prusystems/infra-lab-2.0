
# Project Outline – Lab 2.0 Hybrid Cloud Resilience

This document tracks the phases and tasks for building the lab.

---

## Phase 0 – Foundations

- [x] Create repo `infra-lab-2.0`
- [x] Add README, PROJECT-OUTLINE, STATUS, SECURITY, docs/
- [x] Configure Azure CLI on Mac
- [x] Confirm Cloudflare account + API token
- [x] Decide naming convention (RG, VNet, AKS, VMs, etc.)

---

## Phase 1 – Network & Identity Baseline

- [ ] Terraform:
  - [ ] Resource group
  - [ ] Virtual network (VNet)
  - [ ] Subnets: `aks`, `db`, `bastion`
  - [ ] NSGs (basic)
- [ ] Outputs for subnet IDs, VNet
- [ ] (Optional) Plan Azure AD / Entra integration for AKS identity
  - [ ] Research requirements for Entra then update prequisites

**Deliverable:** network module + successful apply/destroy.

---

## Phase 2 – AKS Cluster & Autoscaling

- [ ] Terraform AKS module:
  - [ ] Cluster creation
  - [ ] Default node pool with autoscaling (min/max)
- [ ] Install NGINX ingress controller
- [ ] Validate `kubectl get nodes`, `kubectl get pods`
- [ ] Deploy simple test API + frontend
- [ ] Configure Horizontal Pod Autoscaler (HPA)
- [ ] Verify HPA behavior with test load
- [ ] Verify AKS cluster autoscaler responds

**Deliverable:** working AKS cluster with autoscaling.

---

## Phase 3 – Linux VMs & Database

- [ ] Terraform linux-vms module:
  - [ ] `db-vm-01` (Postgres or similar)
  - [ ] `bastion-vm`
  - [ ] optional `ops-vm`
- [ ] Lock DB access to app subnet only
- [ ] Deploy test schema to DB
- [ ] Confirm API ↔ DB connectivity

**Deliverable:** DB online, secure network path, app can read/write.

---

## Phase 4 – App Deployment (React + Python)

- [ ] Create `app-lab` repo (separate)
- [ ] Containerize Python API
- [ ] Containerize or build React frontend
- [ ] Helm charts or manifests for:
  - [ ] API Deployment/Service/Ingress
  - [ ] Frontend Deployment/Service/Ingress
- [ ] Configure readiness/liveness probes
- [ ] End-to-end test: user → CDN → AKS → API → DB

**Deliverable:** functional app stack reachable via public endpoint.

---

## Phase 5 – CDN & Failover Pattern

- [ ] Terraform dns-cdn module:
  - [ ] Cloudflare zone + DNS records
  - [ ] Proxy (CDN) enabled
  - [ ] Basic WAF rules (block junk, limit bad patterns)
- [ ] Define secondary CDN / failover origin pattern (Akamai-style):
  - [ ] Real integration if possible, OR
  - [ ] Simulate with second endpoint / zone
- [ ] Document DNS + origin failover behavior
- [ ] Test breaking primary origin and recovering

**Deliverable:** CDN in front of AKS with documented failover pattern.

---

## Phase 6 – Time-Zone-Aware Scaling

- [ ] Define load pattern:
  - [ ] East clinics (US East/Central)
  - [ ] West clinics (US Mountain/Pacific)
- [ ] Implement scheduled scaling:
  - [ ] Morning: increase AKS min nodes
  - [ ] Evening: reduce to night baseline
  - [ ] Use az CLI, GitHub Actions, or automation script
- [ ] Validate with test load during “day/night” windows

**Deliverable:** documented scaling schedule + proof of behavior.

---

## Phase 7 – Resilience & Failure Drills

- [ ] Pod failure tests (delete pods)
- [ ] Node failure tests (cordon/drain/shutdown)
- [ ] DB outage test (stop service or block network)
- [ ] CDN origin failure test
- [ ] Record expected vs actual behavior
- [ ] Update runbooks with steps and lessons learned

**Deliverable:** `docs/resilience-tests.md` + runbooks.

---

## Phase 8 – Serverless Comparison

- [ ] Design serverless alternative:
  - [ ] Static frontend hosting
  - [ ] Azure Functions / Container Apps for API
  - [ ] Managed DB (Azure Database for PostgreSQL)
- [ ] Rough cost comparison:
  - [ ] Infra-based AKS design
  - [ ] Serverless design
- [ ] Evaluate:
  - [ ] Cost
  - [ ] Operational overhead
  - [ ] Downtime profile and risk

**Deliverable:** `docs/cost-analysis.md` + architecture B diagram.

---

You do **not** have to finish every phase to start showing this project.  
Even Phases 1–3 + basic docs already look very strong.
