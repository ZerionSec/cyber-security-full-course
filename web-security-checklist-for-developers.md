# 🛡️ Web Security Checklist for Developers

**The 25 most commonly forgotten security issues that get websites hacked.**

A practical, no-fluff guide written for developers. Every item includes:
- **Cause** — why this happens
- **How to fix** — what to actually do
- **How to verify** — how to confirm it’s fixed

> Security must be enforced by the **backend/server**, not merely hidden in the frontend.  
> Removing a button does not make the action secure.

---

## 1. Broken Access Control / IDOR

**Cause:** Server does not verify that the logged-in user is authorized to access or modify the resource. Relies on hidden IDs or frontend restrictions.

**How to fix:** Always check authorization on the server before any read/update/delete. Use ownership checks and proper role-based access control.

**How to verify:** Change the resource ID in the request (e.g. `/user/123` → `/user/124`) while logged in as another user. Expect 403 or 404.

---

## 2. Weak Authentication

**Cause:** Weak password storage, missing MFA, or easy brute-force attacks.

**How to fix:** Use Argon2id or bcrypt, add MFA when appropriate, implement login rate limiting, and use secure account recovery flows.

**How to verify:** Attempt weak passwords and confirm rate limiting. Check that passwords in the database are properly hashed (never plain text).

---

## 3. Session Flaws

**Cause:** Predictable session IDs, missing expiration, or sessions not invalidated after logout / privilege change.

**How to fix:** Use cryptographically random session IDs, set proper expiration, rotate the session after login or privilege change, and invalidate on logout.

**How to verify:** Copy the session cookie, log out, then try to reuse it. It should no longer be valid.

---

## 4. Unprotected API Endpoints

**Cause:** Endpoint is only hidden in the frontend but remains accessible via direct requests.

**How to fix:** Enforce authentication and authorization on the API itself. Frontend hiding is not security.

**How to verify:** Call the endpoint directly with tools (curl, Postman, etc.) without a valid token or as an unauthorized user.

---

## 5. SQL Injection

**Cause:** User input is concatenated directly into SQL queries.

**How to fix:** Use parameterized queries / prepared statements or a trusted ORM. Never concatenate raw user input into SQL strings.

**How to verify:** Try classic payloads such as `' OR 1=1 --`. The application should not return unexpected data or errors that reveal the injection.

---

## 6. Cross-Site Scripting (XSS)

**Cause:** User-controlled input is rendered without proper encoding.

**How to fix:** Apply context-aware output encoding, use safe templating engines, validate input, and set a strong Content Security Policy (CSP).

**How to verify:** Inject `<script>alert(1)</script>` or event handlers. The payload should not execute.

---

## 7. Cross-Site Request Forgery (CSRF)

**Cause:** State-changing requests can be triggered from another site without protection.

**How to fix:** Use CSRF tokens for state-changing requests and set an appropriate `SameSite` cookie attribute.

**How to verify:** Attempt to submit a form from a different origin. The request should be rejected without a valid token.

---

## 8. Unsafe File Upload

**Cause:** Any file type is accepted and stored in a location that can be executed.

**How to fix:** Allowlist file types, validate actual file content (not just extension), limit file size, randomize filenames, and store uploads outside the web root when possible.

**How to verify:** Try uploading `.php`, `.jsp`, or other executable files. They should be rejected or made non-executable.

---

## 9. Path Traversal

**Cause:** User input is used directly as a filesystem path.

**How to fix:** Never use raw user input as a path. Use allowlisted identifiers and canonicalize/validate paths on the server.

**How to verify:** Attempt payloads like `../../etc/passwd`. Sensitive files should not be accessible.

---

## 10. Security Misconfiguration

**Cause:** Debug mode left on, default credentials, or unnecessary services exposed.

**How to fix:** Disable debug mode in production, remove defaults, restrict admin interfaces, and harden server configuration.

**How to verify:** Inspect error pages, response headers, and open ports. No sensitive information or default credentials should be present.

---

## 11. Exposed API Keys / Secrets

**Cause:** Secrets are committed to the repository or embedded in frontend JavaScript.

**How to fix:** Store secrets in environment variables or a secret manager. If already exposed, revoke and rotate immediately.

**How to verify:** Search source code, browser Network tab, and Git history. No secrets should appear.

---

## 12. Outdated Dependencies

**Cause:** Libraries with known vulnerabilities are not updated.

**How to fix:** Perform regular dependency scanning, keep lockfiles, monitor for vulnerabilities, and remove unused packages.

**How to verify:** Run tools such as `npm audit`, `pip-audit`, Snyk, or Dependabot and act on the findings.

---

## 13. Bad CORS Configuration

**Cause:** Overly permissive `Access-Control-Allow-Origin` (especially `*`) combined with credentials.

**How to fix:** Use an explicit allowlist of trusted origins. Avoid wildcards when cookies or credentials are involved.

**How to verify:** Inspect CORS headers on cross-origin requests. Only expected origins should be allowed.

---

## 14. Missing Security Headers

**Cause:** Protective headers such as CSP, HSTS, and X-Content-Type-Options are not set.

**How to fix:** Configure appropriate security headers based on the application’s requirements.

**How to verify:** Use securityheaders.com or browser DevTools → Network → Headers.

---

## 15. Information Leakage

**Cause:** Detailed error messages, stack traces, or internal paths are shown to users.

**How to fix:** Return generic messages to clients. Keep detailed logs on the server only.

**How to verify:** Trigger errors (invalid input, 404, 500). Responses should be generic.

---

## 16. Client-side-only Validation

**Cause:** Validation exists only in the browser and can be bypassed.

**How to fix:** Re-validate everything on the server. Client-side validation is a UX feature, not a security control.

**How to verify:** Disable JavaScript or modify the request with DevTools/Postman. Invalid data should still be rejected.

---

## 17. No Rate Limiting

**Cause:** Login, OTP, password reset, or sensitive endpoints have no request limits.

**How to fix:** Apply rate limits to authentication and other sensitive or resource-intensive endpoints.

**How to verify:** Send many requests in a short time. The endpoint should throttle or block further attempts.

---

## 18. Weak Password Reset

**Cause:** Reset tokens are predictable or remain valid too long.

**How to fix:** Use cryptographically random, short-lived, single-use tokens and invalidate them after use.

**How to verify:** Try reusing the same reset link or guessing the token. It should fail.

---

## 19. Mass Assignment

**Cause:** All incoming JSON fields are automatically bound to the database model.

**How to fix:** Explicitly allowlist only the fields a user is permitted to change.

**How to verify:** Add extra fields (e.g. `isAdmin: true`) to the request body. They should be ignored.

---

## 20. Business Logic Bugs

**Cause:** Application workflow rules are not enforced on the backend.

**How to fix:** Enforce ownership, payment status, quantity limits, permissions, and state transitions on the server.

**How to verify:** Attempt out-of-order or unauthorized steps (e.g. checkout without payment). The action should be rejected.

---

## 21. Exposed Database / Storage

**Cause:** Database or storage is publicly reachable or has overly broad permissions.

**How to fix:** Restrict network access, require authentication, apply least-privilege IAM, and keep buckets private.

**How to verify:** Attempt external access to the database or storage. It should be blocked.

---

## 22. Verbose Errors

**Cause:** Stack traces and internal details are returned in production responses.

**How to fix:** Show generic client-facing errors and keep detailed logs server-side only.

**How to verify:** Trigger exceptions. No stack traces or internal paths should appear in the response.

---

## 23. No Security Monitoring

**Cause:** No logging or alerting for suspicious activity.

**How to fix:** Log authentication events, privilege changes, suspicious requests, and administrative actions. Set up alerts.

**How to verify:** Confirm that failed logins and unusual activity generate logs and alerts.

---

## 24. Insecure Cookies

**Cause:** Sensitive cookies lack `Secure`, `HttpOnly`, or a proper `SameSite` attribute.

**How to fix:** Set `Secure`, `HttpOnly`, and an appropriate `SameSite` value on sensitive cookies.

**How to verify:** Inspect cookie attributes in browser DevTools → Application → Cookies.

---

## 25. HTTPS / TLS Problems

**Cause:** HTTP is still allowed, mixed content exists, or TLS configuration is outdated.

**How to fix:** Force HTTPS, enable HSTS, remove mixed content, and use a modern TLS configuration.

**How to verify:** Access the site over HTTP (should redirect) and check the SSL Labs rating.

---

## Recommended Security Workflow

Use this mental model on every feature:

1. **Authentication** — Who is the user?
2. **Authorization** — Does this user actually have permission?
3. **Input Validation** — Is the data valid and expected?
4. **Business Logic** — Is the operation allowed by the application rules?
5. **Database Security** — Parameterized queries? Least privilege?
6. **Session / Cookie Security** — Is the session lifecycle secure?
7. **API Security** — Is the API protected the same way as the frontend?
8. **Configuration** — No debug mode, default credentials, or exposed secrets?
9. **Dependencies** — Are libraries updated and monitored?
10. **Monitoring** — Will you notice suspicious activity quickly?
11. **Security Testing** — Test only systems you are authorized to test. Practice on intentionally vulnerable labs such as OWASP Juice Shop, DVWA, or WebGoat.

---

## Final Rule

> **Never trust the frontend.**  
> If the backend still accepts an unauthorized or malicious request after the UI button is removed, the application is still vulnerable.

---

Made for developers who are tired of seeing the same preventable hacks.
