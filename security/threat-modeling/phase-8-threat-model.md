# Phase 8 – Threat Modeling & Risk Analysis

## 1. System Overview
The system is a DevSecOps CI/CD pipeline running Jenkins locally on a Mac M1 system.  
The pipeline pulls source code from a Git repository, performs SAST and DAST scans,
builds application artifacts, stores scan results, and deploys the application
to a target environment.

## 2. Identified Assets
- Source code stored in the Git repository
- Jenkins credentials and access tokens
- Secrets used in pipelines (API keys, passwords)
- Security scan reports (SAST and DAST)
- Build artifacts and container images

## 3. Threat Modeling Methodology
STRIDE threat modeling methodology was used to identify potential threats
across CI/CD components.

## 4. Key Threat Identified
**Threat:** Information Disclosure  
Sensitive secrets such as API tokens or passwords may be exposed in Jenkins
build logs due to misconfigured pipeline scripts or insufficient masking.

## 5. Risk Analysis
- Likelihood: High  
- Impact: High  

**Overall Risk Rating:** High

## 6. Business Context
Although the technical impact is high, the overall exposure is currently
moderate because the Jenkins instance is locally hosted with limited access.

## 7. Risk Decision
Risk will be mitigated by implementing secure secret handling, log masking,
and access control hardening in Jenkins.

## Phase 8 Summary
Phase 8 focused on security architecture and governance.
Threat modeling and STRIDE analysis were performed for the CI/CD pipeline.
Risks were prioritized using likelihood and impact.
Mitigations were implemented including secure secret handling, CVSS-based
security gates, and role-based access control.
This phase ensures the pipeline is secure by design, not just secure by tools.

