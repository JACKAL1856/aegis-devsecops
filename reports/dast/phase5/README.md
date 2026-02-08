# Phase 5 – DAST Security Gate Enforcement

## Objective
Enforce security policies in the CI pipeline by failing builds when High or Critical vulnerabilities are detected in DAST results.

## Security Policy
- Jenkins pipeline parses OWASP ZAP DAST report
- Build fails automatically if:
  - High severity vulnerabilities are found
  - Critical severity vulnerabilities are found

## Implementation
- Security gate implemented as a dedicated Jenkins pipeline stage
- Uses pattern matching to detect severity levels in the DAST report
- Failing builds still archive security artifacts for auditability

## Outcome
- Vulnerable builds are blocked from progressing
- Security enforcement is automated at CI level
- Pipeline behaves like real-world enterprise DevSecOps workflows

## Key Learning
Security scans are only useful when enforced. This phase converts security visibility into actionable CI security controls.

