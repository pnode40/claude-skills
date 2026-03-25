---
name: security-vibe-coded-apps
description: Conduct comprehensive security audits of AI-generated codebases. Use this skill whenever you need to audit a web application built with Claude, Cursor, Copilot, or other AI coding assistants. This covers vibe-coded Next.js, React, or full-stack apps using OWASP Top 10, CWE database, and LLM-specific vulnerabilities (hallucinated packages, missing RLS, hardcoded secrets, weak auth middleware). Triggers on phrases like "security audit," "code review," "find vulnerabilities," or when analyzing any vibe-coded codebase.
---

# Security Audit for AI-Generated Codebases

## Overview

When AI coding assistants generate applications quickly, they routinely introduce security gaps that a human developer would catch. This skill provides a **systematic two-pass methodology** to find every one of those gaps.

You are a senior application security engineer specializing in AI-generated codebases with deep expertise in OWASP Top 10, CWE database, and vulnerability patterns introduced by LLM code generation.

---

## Methodology: Two-Pass Approach

### PASS 1 — DISCOVERY
Read the entire codebase before making any findings. Build a mental model of:
- Framework (Next.js, React, Vue, etc.)
- Database (Supabase, Firebase, PostgreSQL, etc.)
- Auth provider (NextAuth, Auth0, Supabase Auth, etc.)
- API layer and entry points (pages, API routes, server actions, webhooks, cron jobs)
- Data flow from user input to database and back

### PASS 2 — SYSTEMATIC AUDIT
Work through each checklist item below. For every item, produce one of four verdicts:

- **✅ PASS** — The codebase handles this correctly. Cite the file/line.
- **❌ FAIL** — A vulnerability exists. Document it fully (see format below).
- **⚠️ PARTIAL** — Some coverage but gaps remain. Explain what's missing.
- **⬚ N/A** — Not applicable to this codebase. State why briefly.

Do not skip items. Do not summarize groups of items. Every single checklist item gets its own explicit verdict.

---

## Security Audit Checklist

### Section 1: Environment Variables and Secret Management

- **1.1 Hardcoded Secrets**
  Search every file for API keys, tokens, passwords, connection strings, and webhook URLs.
  Patterns: `sk_live_`, `sk_test_`, `Bearer`, `eyJ` (JWT), `ghp_`, `gho_`, `github_pat_`, `xoxb-`, `xoxp-` (Slack), `AKIA` (AWS), any 32+ char alphanumeric strings in quotes.

- **1.2 .gitignore Coverage**
  Verify `.env`, `.env.local`, `.env.production`, `.env*.local` are all in `.gitignore`.
  Check git history: secrets in git history are exposed even if later removed.

- **1.3 Public Prefix Leaks**
  Ensure server-only secrets do NOT use framework public prefixes (`NEXT_PUBLIC_`, `VITE_`, `REACT_APP_`).
  Never public-prefix: database service role keys, Stripe secret keys, OpenAI/Anthropic API keys, SMTP credentials, keys granting write/admin access.

- **1.4 Console/Error Leaks**
  Search for `console.log`, `console.error`, and error boundary components that might print environment variables or secrets to browser console or client-visible error messages.

- **1.5 Build Artifact Exposure**
  Check if source maps are enabled in production (`productionBrowserSourceMaps` in next.config.js, Vite sourcemap config). Source maps let anyone reconstruct original source code including inlined secrets.

- **1.6 Startup Validation**
  Verify the app fails fast if required environment variables are missing, rather than silently running with undefined values.

---

### Section 2: Database Security

(Adapt for your database architecture: Supabase/Firebase with client access vs. server-only Prisma/PostgreSQL)

- **2.1 RLS Enabled**
  Verify Row Level Security is enabled on EVERY table in the public schema. A single unprotected table exposes all its data to anyone with the anon key.

- **2.2 RLS Policies Exist**
  A table with RLS enabled but NO policies silently returns empty results for all queries (looks like a bug, not a security issue). Verify every RLS-enabled table has at least SELECT and INSERT policies.

- **2.3 WITH CHECK Clauses**
  Verify all INSERT and UPDATE policies include WITH CHECK clauses. Without WITH CHECK on INSERT, a user can insert rows with any `user_id` (impersonating others). Without WITH CHECK on UPDATE, a user can change ownership.

- **2.4 Policy Identity Source**
  Ensure RLS policies use `auth.uid()` for identity, NOT `auth.jwt()->'user_metadata'`. User metadata can be modified by authenticated end users.

- **2.5 Service Role Key Isolation**
  The service_role key bypasses all RLS. Verify it is NEVER used in client-side code, never imported in components, and only used in server-side code where RLS bypass is necessary (admin operations, webhooks).

- **2.6 Storage Bucket Policies**
  If using Supabase Storage, verify storage buckets have RLS policies. By default, storage buckets are publicly accessible.

- **2.7 SQL Injection**
  Check for any raw SQL queries using string concatenation or template literals instead of parameterized queries.

- **2.8 SECURITY DEFINER Functions**
  Check for any database functions marked SECURITY DEFINER. These run with function creator privileges (usually superuser). Verify they don't expose data or bypass RLS.

---

### Section 3: Authentication and Session Management

- **3.1 Session Storage**
  If using sessions (JWT in httpOnly cookie, server session store), verify they are stored securely.
  httpOnly cookies prevent JavaScript access. Secure flag requires HTTPS. SameSite=Strict prevents CSRF.

- **3.2 JWT Claims**
  If using JWT, verify the token includes user identity and does not include sensitive data (passwords, API keys, payment info).

- **3.3 Token Expiration**
  Verify access tokens expire within 15 minutes. Verify refresh tokens are long-lived, single-use, and transmitted securely.

- **3.4 Password Storage**
  If storing passwords server-side, verify they are hashed with a modern algorithm (bcrypt, scrypt, Argon2), not plaintext or weak hashing.

- **3.5 Password Reset Tokens**
  If implementing password reset, verify tokens are cryptographically random, short-lived (15-60 minutes), single-use, and transmitted securely (not in query string).

---

### Section 4: Server-Side Validation

- **4.1 Schema Validation**
  Verify all API routes and server actions validate input using a schema library (Zod, Yup, Valibot, ArkType) on the server side. Frontend validation is UX, not security.

- **4.2 Identity from Session**
  Verify user identity for write operations is ALWAYS derived from authenticated session or JWT token, never from request body fields like `{ userId: "..." }`.

- **4.3 Input Sanitization**
  Check that user-generated content rendered in HTML is properly sanitized to prevent XSS. Look for `dangerouslySetInnerHTML`, `v-html`, `[innerHTML]`, or unescaped template literals rendering user content.

- **4.4 HTTP Method Enforcement**
  Verify state-changing operations use POST/PUT/PATCH/DELETE, not GET. GET requests can be triggered by image tags, link prefetching, and browser extensions without user intent.

- **4.5 Error Information Leaks**
  Verify error responses don't leak internal details (stack traces, SQL errors, file paths, environment variable names) to the client.

- **4.6 Webhook Signature Verification**
  If the app receives webhooks (Stripe, GitHub, etc.), verify it validates the webhook signature before processing.

---

### Section 5: Dependency and Package Security

- **5.1 Audit Results**
  Run the package manager's audit command (`npm audit`, `pnpm audit`, `yarn audit`, `bun audit`) and report any vulnerabilities found, grouped by severity.

- **5.2 Hallucinated Packages**
  Check for any installed packages with suspiciously low download counts, very recent publish dates, or names that don't match well-known packages. AI tools sometimes hallucinate package names.

- **5.3 Lockfile Committed**
  Verify a lockfile (`package-lock.json`, `pnpm-lock.yaml`, `yarn.lock`, `bun.lockb`) is committed to the repository.

- **5.4 Outdated Packages**
  Check for outdated packages, especially those with known CVEs. Pay particular attention to auth libraries, crypto libraries, and framework versions.

- **5.5 Unused Dependencies**
  AI tends to install packages it ends up not using. Each unused package is unnecessary attack surface. Check for packages in package.json that aren't imported anywhere.

---

### Section 6: Rate Limiting

- **6.1 Expensive Operations**
  Identify all API routes that call external paid APIs (OpenAI, Anthropic, Stripe, email/SMS providers) and verify they have rate limiting.

- **6.2 Auth Endpoints**
  Verify login, signup, password reset, and OTP endpoints have rate limiting to prevent brute force attacks.

- **6.3 Implementation Check**
  If rate limiting exists, verify it's applied server-side (not just frontend debouncing) and uses a reliable backing store (Redis, Upstash) rather than in-memory storage.

---

### Section 7: CORS Configuration

- **7.1 API Route CORS**
  If the app exposes API routes intended only for its own frontend, verify CORS headers restrict access to the app's own domain(s). Check for `Access-Control-Allow-Origin: *` on sensitive endpoints.

- **7.2 Credentials Mode**
  If CORS is configured, verify `Access-Control-Allow-Credentials` is only true when paired with specific (not wildcard) origins.

---

### Section 8: File Upload Security

- **8.1 Server-Side Validation**
  If the app handles file uploads, verify file type and size are validated on the server, not just the frontend. Check MIME type, not just file extension.

- **8.2 Storage Permissions**
  Verify uploaded files are stored with appropriate access controls. Public uploads (profile photos) and private uploads (documents) should have different policies.

- **8.3 Execution Prevention**
  Verify uploaded files cannot be executed on the server. Check that upload directories are not in the web root's executable path.

---

## Vulnerability Report Format

For every **❌ FAIL** finding, use this exact structure:

```
FINDING #[number]: [Title]
Severity: CRITICAL / HIGH / MEDIUM / LOW
Location: file/path.ts:line_number
CWE: CWE-XXX (Name)

What's wrong:
[Plain English description of the vulnerability]

Why it matters:
[What an attacker could actually do with this]

How to fix it:
[Plain English plan, no code. E.g., "Move the key to .env, reference via process.env, ensure .env is in .gitignore"]

Effort: ~[X] minutes
```

---

## Final Report Structure

After completing all checklist items, compile findings into:

### 1. Security Posture Rating
Rate the overall codebase:
- 🔴 **CRITICAL** — Active data exposure or auth bypass. Stop and fix now.
- 🟠 **NEEDS WORK** — Significant gaps that would be exploitable.
- 🟡 **ACCEPTABLE** — Minor issues, no immediate data exposure risk.
- 🟢 **STRONG** — Well-secured with only informational findings.

Include a one-paragraph executive summary explaining the rating.

### 2. Critical and High Findings
List all CRITICAL and HIGH severity findings here for immediate visibility.

### 3. Quick Wins
List fixes that take under 10 minutes each but meaningfully improve security posture.

### 4. Prioritized Remediation Plan
A numbered list of ALL findings ordered by:
1. Severity (critical before high before medium before low)
2. Effort (quick fixes before complex refactors within each tier)

For each item, include estimated fix time.

### 5. What's Already Done Right
List security measures that are properly implemented. This tells the developer what NOT to accidentally break and reinforces good patterns to continue.

### 6. Checklist Summary
Output a compact summary of every checklist item and its verdict:
```
1.1 ✅  1.2 ✅  1.3 ❌  1.4 ✅  1.5 ⚠️  1.6 ⬚ ...
```

---

## How to Use This Skill

**Provide:**
1. The full codebase (or relevant file excerpts if the codebase is very large)
2. Architecture overview (framework, database, auth provider, deployment)
3. Any known context (e.g., "this is a Next.js app with Supabase, deployed to Vercel")

**You'll receive:**
1. A complete security audit with all checklist items explicitly addressed
2. Detailed findings with severity, location, CWE, and plan to fix
3. A prioritized remediation plan
4. Quick wins you can tackle immediately

**Example trigger phrases:**
- "Security audit my Next.js codebase"
- "Find vulnerabilities in this React app I built with Cursor"
- "Audit this Supabase + Next.js app for security gaps"
- "Check this code for vibe-coding security issues"

