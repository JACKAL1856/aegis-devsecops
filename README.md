# Aegis – DevSecOps CI/CD Pipeline with Jenkins

Aegis is an end-to-end **DevSecOps CI/CD pipeline** implemented using Jenkins, designed to demonstrate real-world security automation, governance, and risk-based decision-making across the software delivery lifecycle.

This project goes beyond tool integration and focuses on **security-by-design**, **policy enforcement**, and **audit-ready documentation**.

---

## Project Objectives

- Integrate security testing into CI/CD pipelines
- Enforce risk-based security gates
- Prevent secret leakage and misconfigurations
- Apply governance and least-privilege access control
- Produce compliance and SOC-ready security artifacts

---

## Architecture Overview

- Jenkins CI/CD Pipeline
- SAST, DAST, and Secrets Scanning
- CVSS-based Security Gates
- Jenkins Credentials Manager
- Role-Based Access Control (RBAC)
- GitHub as source-of-truth for security design and reporting

---

## Phase Breakdown

### **Phase 1 – CI/CD Pipeline Foundation**
**Objective:** Establish Jenkins-based CI/CD pipeline  
- Jenkins installation and job setup  
- Source code checkout from GitHub  
- Baseline pipeline execution  

**Skills:** Jenkins fundamentals, pipeline structure

---

### **Phase 2 – SAST Integration**
**Objective:** Detect code-level security issues early  
- Static code analysis integration  
- Fail pipeline on critical findings  

**Skills:** Secure SDLC, SAST automation

---

### **Phase 3 – Secrets Detection**
**Objective:** Prevent credential leakage  
- Secrets scanning in source code  
- Immediate pipeline failure on detection  

**Skills:** Secrets management, shift-left security

---

### **Phase 4 – DAST Integration**
**Objective:** Identify runtime vulnerabilities  
- Dynamic application security testing  
- Vulnerability report generation  

**Skills:** Web security testing, DAST orchestration

---

### **Phase 5 – CVSS-Based Security Gate**
**Objective:** Enforce risk-based pipeline control  
- CVSS threshold evaluation (≥ 7.0)  
- Pipeline failure on high-risk findings  

**Skills:** Risk scoring, policy enforcement

---

### **Phase 6 – DAST Governance & Reporting**
**Objective:** Add structured validation and evidence  
- DAST report validation  
- Governance logic in pipeline  
- Audit-friendly outputs  

**Skills:** Security governance, reporting discipline

---

### **Phase 7 – Security Alerting & Notifications**
**Objective:** Enable real-time security awareness  
- Gmail SMTP integration with Jenkins  
- Secure authentication via app passwords  
- Automated alerts for security findings  

**Skills:** Alerting design, secure SMTP configuration

---

### **Phase 8 – Threat Modeling & Security Architecture**
**Objective:** Design security, not just scan for issues  

- STRIDE-based threat modeling  
- Risk analysis using likelihood × impact  
- Secure secret handling using Jenkins Credentials Manager  
- CVSS security waiver governance  
- Role-Based Access Control (RBAC) with least privilege  

 Documentation:  
`security/threat-modeling/phase-8-threat-model.md`

**Skills:** Security architecture, threat modeling, governance

---

### **Phase 9 – Compliance, Reporting & SOC Readiness**
**Objective:** Communicate security posture clearly  

- Executive-level security summary  
- Compliance alignment (OWASP Top 10)  
- SOC-style reporting and traceability  
- Audit-ready documentation  

 Documentation:  
`security/reports/phase-9-security-report.md`

**Skills:** Compliance thinking, SOC readiness, security reporting

---

## Key Security Features

- CVSS-based security gates  
- Secure secrets handling (no hardcoded credentials)  
- RBAC-enforced governance  
- Risk-based security decisions  
- Full traceability via Git history  

---



