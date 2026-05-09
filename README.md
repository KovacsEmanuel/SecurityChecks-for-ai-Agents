# AI App Security Checklist

Security checks for AI-powered applications — designed to be run by automated agents through code analysis, config inspection, and HTTP probing. Designed and written by AI.

---

## What's in it

**~230 checks across 15 sections:**

| # | Section | Covers |
|---|---------|--------|
| 1 | Authentication & Session Security | Cookies, JWT, MFA, OAuth2, brute-force |
| 2 | Authorization & Access Control | RBAC, IDOR, BOLA, least privilege |
| 3 | Input & Output Security | XSS, SQLi, SSRF, SSTI, prompt injection |
| 4 | Cryptography & Data Protection | Hashing, CSPRNG, key management, TLS |
| 5 | Server & Infrastructure Hardening | Headers, CORS, rate limiting, containers |
| 6 | Software Supply Chain | CVE scanning, lockfiles, CI/CD, SRI hashes |
| 7 | AI-Specific Security | Prompt injection, jailbreaks, agent scope, MCP |
| 8 | Framework: Web | React/Next.js, Vue/Nuxt, Angular, SvelteKit, Ionic |
| 9 | Framework: Desktop | Tauri v2, Electron, .NET MAUI, Qt |
| 10 | Framework: Mobile | Flutter, React Native, Kotlin Multiplatform |
| 11 | Framework: Backend/API | Node.js, Python, Go, Java, GraphQL, gRPC |
| 12 | Security Code Review | Dangerous functions, auth, injection, memory, AI code |
| 13 | Application Permissions Audit | Windows, Linux, macOS, cloud, mobile |
| 14 | Privacy & Compliance | GDPR, PII, data retention, audit trails |
| 15 | Monitoring & Incident Response | Detection, alerting, rate limiting, CVE monitoring |

---

## Aligned with

OWASP Top 10:2025 · OWASP API Security Top 10:2023 · OWASP LLM Top 10:2025 · MITRE CWE Top 25:2024 · NIST SP 800-53 · OWASP ASVS 4.0 · PTES

---

## How each check works

Every check has four fields an agent can act on directly:

```
DETECT:  what to read, grep, or request
PASS IF: condition that means the check passes
FAIL IF: condition that means it fails
CWE/REF: framework reference
```

Detection types: `[GREP]` source files · `[FILE]` config/manifest · `[HTTP]` live request · `[CODE]` logic/data flow

**Agent output format:**
```
CHECK_ID | STATUS (PASS/FAIL/PARTIAL/NA) | EVIDENCE | REMEDIATION
```

**Stack auto-detection** — agents detect the framework from the repo and run only relevant sections:

| File found in repo | Section to run |
|--------------------|----------------|
| `src-tauri/tauri.conf.json` | §9.1–9.8 (Tauri) |
| `"electron"` in `package.json` | §9.9–9.14 (Electron) |
| `pubspec.yaml` | §10.1–10.6 (Flutter) |
| `metro.config.js` | §10.7–10.10 (React Native) |
| `next.config.js` | §8.1–8.3 (Next.js) |
| `manage.py` | §11.5–11.7 (Django) |
| `schema.graphql` or `typeDefs` | §11.12–11.14 (GraphQL) |
| `*.proto` files | §11.15 (gRPC) |
| `*.go` + `main.go` | §11.8–11.9 (Go) |
| `*.c` / `*.cpp` | §12.8 (C/C++) |

**Execution phases:**
1. Phase 1 (source access): all `[GREP]`, `[CODE]`, `[FILE]` checks
2. Phase 2 (running app): all `[HTTP]` checks
3. Phase 3 (system access): all §13 permissions checks

---

## Agent orchestration

An orchestration plan is included that coordinates 9 specialized agents across 3 parallel phases, ending with a deduplicated Markdown report with CVSS scores and attack chains. See `security-agent-orchestration-plan.txt`.

---

## Files

| File | Description |
|------|-------------|
| `ai-app-security-checklist.txt` | Full agent-executable checklist (~230 checks) |
| `security-agent-orchestration-plan.txt` | 9-agent orchestration plan |
| `README.md` | This file |

---

## ⚠️ Disclaimer

The checks and agents in this repo perform **automated security hygiene** — they catch common, well-known issues: hardcoded secrets, outdated dependencies, missing headers, basic injection patterns, misconfigured permissions.

**This is not a penetration test.**

Automated agents will not find business logic flaws, complex attack chains, race conditions, custom crypto issues, or anything that requires real adversarial thinking and application context. There is a significant gap between "passes these checks" and "is secure."

**Every application should have a professional penetration test** performed by a certified security professional — before going to production, after major releases, and at minimum once per year. This is non-negotiable for applications handling financial data, PII, authentication, or anything regulated.

Use this tooling to fix the obvious issues first. Then get a real pentest.

---

