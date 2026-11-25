# Static Code Scanning (SAST) with Bandit

Static analysis of a Python/Django web application using Bandit, from a web application security analysis project. The scan output maps each finding to OWASP categories with severity and confidence.

**Scan output:** [bandit-scan-results.txt](bandit-scan-results.txt)

## Findings include

- Hardcoded database password in source (OWASP A6, Security Misconfiguration, high severity)
- XSS through Django `mark_safe` on user-controlled input (OWASP A7)
- Weak MD5 hashing of user passwords
