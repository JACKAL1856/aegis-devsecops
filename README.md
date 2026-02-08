# Aegis – DevSecOps CI/CD Pipeline with Jenkins

This project demonstrates a practical DevSecOps CI/CD pipeline implemented using Jenkins, focusing on real-world security validation and governance.

## Tooling & Stack
- Jenkins (Declarative Pipeline)
- OWASP ZAP (DAST)
- GitHub
- Docker
- Linux

## Security Phases Implemented

### Phase 4 – DAST Execution & Report Archival
- Automated OWASP ZAP DAST scanning
- HTML report generation
- Jenkins artifact archival for auditability

### Phase 5 – DAST Security Gate Enforcement
- Pipeline failure on detection of High/Critical vulnerabilities
- Clear console evidence of policy enforcement
- Security-first fail-fast approach

## Phase 6 – Advanced DAST Governance

- CVSS-based DAST security gate (threshold ≥ 7.0)
- Automatic pipeline failure on policy violation
- Manual security waiver support via Jenkins parameters
- Audit-friendly and governance-ready pipeline design
