# 🧠 Long-Term Memory

*Curated knowledge and decisions that persist across sessions.*

---

## 📋 Project Context

### Architecture Decisions

**API Design (2026-01-15)**
- Chose GraphQL over REST for new endpoints
- Reasoning: Better query flexibility, reduced over-fetching
- Migration: Keep REST for v1, add GraphQL as v2
- #architecture #api #decision

**Database Strategy (2026-01-10)**
- Primary: PostgreSQL for transactional data
- Cache: Redis for sessions and hot data
- Analytics: ClickHouse for time-series
- #database #infrastructure

### Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React 18, TypeScript, Tailwind |
| Backend | Node.js, Express, GraphQL |
| Database | PostgreSQL 15, Redis 7 |
| Infrastructure | GKE, CloudFlare, Vercel |
| CI/CD | GitHub Actions, ArgoCD |

---

## 👥 Team & Contacts

### Key Stakeholders
- **Product Lead**: Reviews all major features
- **Engineering Lead**: Approves architecture changes
- **Security Team**: Required for auth changes

### External Services
- AWS Account: Production workloads
- Vercel: Frontend deployments
- Sentry: Error tracking
- DataDog: APM and monitoring
- #contacts #services

---

## 🎯 Preferences & Workflows

### Code Review Standards
- All PRs require 1 approval minimum
- Security-related changes need 2 approvals
- Auto-merge enabled for dependency updates (patch only)
- #workflow #code-review

### Communication Preferences
- Urgent issues: Slack DM immediately
- Non-urgent: Async via GitHub issues
- Weekly sync: Mondays 10am
- #communication

### Deployment Process
1. Feature branch → Main (PR)
2. Auto-deploy to staging
3. Manual promotion to production
4. Canary rollout (10% → 50% → 100%)
- #deployment #process

---

## 📚 Lessons Learned

### What Worked Well
- **Incremental migrations**: Breaking large changes into smaller PRs
- **Feature flags**: Safer rollouts, easy rollback
- **Automated testing**: Caught 3 critical bugs before production

### What to Avoid
- ❌ Large PRs (>500 lines) — hard to review
- ❌ Friday deployments — no one wants weekend incidents
- ❌ Skipping staging — always test first
- #lessons #retrospective

---

## 🔐 Credentials & Access

> Note: Actual credentials stored in 1Password

### Service Accounts
- **GitHub Bot**: For automated PRs and releases
- **Slack Bot**: For notifications
- **CI Service Account**: GCP access for deployments

### API Keys Location
- Production: GCP Secret Manager
- Development: `.env.local` (gitignored)
- #credentials #security

---

## 📅 Important Dates

- **Q1 2026 Goals**: Ship API v2, Mobile app beta
- **Security Audit**: Annually in January
- **SOC 2 Renewal**: March 2026
- **Team Offsite**: April 2026
- #dates #planning

---

*Last updated: 2026-02-01*
