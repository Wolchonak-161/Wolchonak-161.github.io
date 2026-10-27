# 👾 Cybersecurity Portfolio

**Security Engineer in Training · DevSecOps · Penetration Testing · Threat Analysis**

> Building automated security pipelines that find vulnerabilities before attackers do.

---

## 🛠️ Core Competencies

| Domain | Skills |
|---|---|
| **Vulnerability Scanning** | Nuclei, OWASP ZAP, custom YAML templates |
| **DevSecOps & CI/CD** | GitHub Actions, automated security gates, Linear integration |
| **Cloud Security** | AWS staging security, S3 exposure checks, subdomain takeover detection |
| **Frameworks** | NIST CSF v2.0 (ID, PR, DE, RS), OWASP Top 10 |
| **Languages & Tools** | TypeScript, Node.js, Bash, YAML, REST APIs |
| **Methodologies** | Threat modeling, CVSS severity routing, SLA-driven ticket lifecycle |

---

## 📂 Projects

---

### 🔬 Project 1 — Automated Pentest Pipeline (Nuclei × Linear × AWS)

> **Internship Project @ Panos.ai** · EINT-103 · NIST CSF Aligned

Designed and built a full DevSecOps vulnerability scanning pipeline that automatically discovers security weaknesses in AWS staging environments and routes them into the developer workflow — zero manual triage required.

**What I built:**

- **Custom Nuclei YAML templates** targeting the exact Panos.ai tech stack (Next.js, Hono API, AWS Amplify):
  - Exposed `.env` / config file detection over HTTP/HTTPS
  - Missing HTTP security headers (HSTS, CSP, X-Content-Type-Options)
  - CORS misconfiguration checks against the Hono backend
  - API key leak detection via regex patterns (`lin_api_*`, `AKIA*`)
  - Next.js `_next/data/` over-fetching and source map exposure

- **TypeScript sync engine** (`nuclei-to-linear.ts`) that:
  - Parses Nuclei JSON output and creates structured tickets in Linear
  - Deduplicates findings — no ticket spam on re-scans
  - Auto-closes resolved vulnerabilities when a clean scan runs
  - Routes severity to Linear priority: Critical → Urgent, High → High, etc.

- **GitHub Actions CI/CD workflow** with hard build gates:
  - Critical/High findings exit code `1` → **blocks deployments**
  - Medium/Low generate warnings, info-level findings logged to markdown
  - Versioned output folders committed to git for traceability

- **Documented staging isolation policy** to prevent accidental production scanning

**Architecture:**

```
GitHub Actions (scheduled / PR trigger)
        │
        ▼
   Nuclei CLI ──► Custom YAML Templates ──► AWS Staging Targets
        │
        ▼
   results.json (versioned in outputs/)
        │
        ▼
nuclei-to-linear.ts
        ├── Deduplication check (query active Linear issues)
        ├── Create tickets (Backlog, severity-mapped priority)
        └── Auto-close resolved findings → Done
```

**NIST CSF v2.0 Alignment:**

| Function | Implementation |
|---|---|
| **Identify** | Scans identify misconfigurations and exposed secrets in AWS staging |
| **Protect** | Client bundle scanning prevents API key leaks to production |
| **Detect** | Automated CI/CD scans on every deployment catch regressions instantly |
| **Respond** | Linear ticket automation ensures findings reach developers within minutes |

**Severity & SLA Matrix:**

| Severity | Linear Priority | CI/CD Gate | SLA |
|---|---|---|---|
| Critical | Urgent (1) | ❌ Hard Fail | < 24 hours |
| High | High (2) | ❌ Hard Fail | 3 days |
| Medium | Medium (3) | ⚠️ Warning | Next sprint |
| Low | Low (4) | ✅ Pass | Backlog triage |
| Info | — | ✅ Pass | Logged to markdown |

**Stack:** `Nuclei` · `TypeScript` · `Node.js` · `GitHub Actions` · `Linear SDK` · `AWS` · `NIST CSF v2.0`

🔗 [View Repository](https://github.com/Wolchonak-161/Nuclei) *(private — available on request)*

---

### 📋 Nuclei vs. ZAP — Why Both?

As part of the Panos.ai security program, I documented why the pipeline uses two complementary tools:

| | ZAP (DAST Proxy) | Nuclei (Template Scanner) |
|---|---|---|
| **Method** | Crawls and fuzzes live sessions | Targeted declarative YAML checks |
| **Best for** | Auth flows, CSRF, XSS injection | Config audits, CVE checks, CI/CD |
| **Output** | HTML/XML for manual review | Structured JSON → auto-synced to Linear |

They are not interchangeable — both are required for comprehensive coverage.

---

### 🗺️ OWASP AI Top 10 — LLM Security Audit Prompt

> **Independent Research Project**

Researched the OWASP Top 10 for Large Language Model Applications (2025 edition) and built a comprehensive **agent-ready audit prompt** covering all 10 threat categories:

- **LLM01: Prompt Injection** — Direct (jailbreaks), Indirect (RAG/tool poisoning), Obfuscation (Base64, homoglyphs, multilingual)
- **LLM02–LLM10** — Sensitive disclosure, supply chain, data poisoning, improper output handling, excessive agency, system prompt leakage, vector/embedding weaknesses, misinformation, unbounded consumption
- Structured output schema: per-threat status, severity, evidence, remediation, risk matrix, priority roadmap
- Python red-team test suite skeleton included

The prompt is designed to be passed directly to an AI security auditor agent and produce a structured Markdown threat report.

**Stack:** `Python` · `OpenAI API` · `OWASP LLM Top 10 2025` · `NIST AI RMF` · `MITRE ATLAS`

---

## 🎓 Learning & Development

- **Active focus areas:** Penetration testing, DevSecOps pipelines, cloud security (AWS), AI/LLM security
- **Frameworks studied:** NIST CSF v2.0, OWASP Top 10 (Web & LLM), MITRE ATT&CK
- **Currently building:** Security automation tooling, custom Nuclei templates, OWASP audit tooling

---

## 📬 Contact

- 🐙 GitHub: [github.com/Wolchonak-161](https://github.com/Wolchonak-161)

---

*"Documentation is the difference between a hacker and a security engineer."*
