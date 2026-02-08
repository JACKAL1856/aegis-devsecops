# Aegis – DevSecOps CI/CD Pipeline with Jenkins

Aegis is a hands-on DevSecOps CI/CD pipeline implemented using Jenkins, focused on real-world security scanning, governance, and automated alerting.  
This project demonstrates how security is embedded into CI/CD pipelines using industry-aligned practices.

---

## Tooling & Stack
- Jenkins (Declarative Pipeline)
- OWASP ZAP (DAST)
- Semgrep (SAST)
- Dependency-Check (SCA)
- Secret Scanning
- Gmail SMTP (Email Alerts)
- Docker
- GitHub
- Linux

---

## Security Phases Implemented

### Phase 4 – DAST Execution & Report Archival
- Automated OWASP ZAP DAST scanning
- JSON / HTML report generation
- Jenkins artifact archival for auditability

### Phase 5 – DAST Security Gate Enforcement
- Pipeline failure on detection of High/Critical vulnerabilities
- Console-based evidence of enforcement
- Fail-fast, security-first pipeline behavior

### Phase 6 – Advanced DAST Governance
- CVSS-based security gate (threshold ≥ 7.0)
- Automatic pipeline failure on policy violation
- Manual security waiver support via Jenkins parameters
- Governance-ready, audit-friendly pipeline design

---

## Phase 7 – Security Alerting & Email Notifications

### Objective
Provide real-time security alerting by integrating Jenkins with email notifications for SAST, SCA, DAST, and Secrets scan results.

### What Was Implemented
- Gmail SMTP integration with Jenkins
- Secure authentication using Google App Passwords
- TLS-enabled email transport (`smtp.gmail.com:587`)
- Jenkins Credentials Manager for secret storage
- Automated alert triggering based on security scan results

### Proof
- Test emails successfully delivered from Jenkins
- Alert engine triggered on detected vulnerabilities
- Evidence captured during live Jenkins execution and SMTP validation
- Screenshots available in `/screenshots/phase7`

### Skills Demonstrated
- Secure CI/CD configuration
- SMTP troubleshooting & authentication
- DevSecOps alerting design
- Real-world Jenkins debugging and validation

