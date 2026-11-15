# Lab 05: Security Maturity Scoring, Risk Evaluation, and Improvement Roadmap

**Type:** Hands-on

**Level:** Advanced

**Duration:** 90 minutes

## **1. Objective**

Evaluate GitHub Copilot security maturity across eight assessment domains using the five-level maturity model. Calculate weighted security scores, identify security gaps, prioritize findings, map risks to security frameworks, and prepare a professional security assessment report with an improvement roadmap.

## **2. Five-Level Security Maturity Model**

Assign a maturity level from 0 to 4 for each assessment domain based on collected evidence.

| Level | Maturity Name | Description |
| --- | --- | --- |
| 0 | Unmanaged | Personal accounts, no policies, and no visibility. |
| 1 | Aware | Written policies, approved accounts, developer training, and some user-level settings. |
| 2 | Managed | Managed settings enforced across the fleet, sandbox enabled, MCP and plugin allowlists, and telemetry enabled. |
| 3 | Monitored | Tested detections, isolated CI agents, enforced version requirements, and advisory-driven patching. |
| 4 | Optimised | Automated attack testing, metrics-driven policies, scoped agent identities, and verified production access restrictions. |

**Target maturity:** Level 2 across all domains and Level 3 for policy enforcement, isolation, and CI/CD.

## **3. Domain Maturity Scoring**

Evaluate each domain and assign a maturity level based on its supporting evidence.

| Assessment Domain | Weight | Evidence to Collect | Maturity Level |
| --- | --- | --- | --- |
| Governance | 10% | Security policies, ownership records, framework mapping | 0–4 |
| Identity and Access | 15% | SSO, SCIM, login enforcement, CI identity | 0–4 |
| Policy Enforcement | 20% | VS Code policy files, MDM profiles, Copilot organization policies, audit reports | 0–4 |
| Isolation | 15% | Sandbox settings, container configurations, technical test results | 0–4 |
| Supply Chain | 10% | MCP and extension allowlists, pinning, intake records | 0–4 |
| CI/CD and Production | 15% | Workflow reviews, branch protection, production access records | 0–4 |
| Observability and Response | 10% | Audit telemetry, detection results, tabletop records | 0–4 |
| Threat Intelligence and Testing | 5% | Security advisory tracking, assessment and testing records | 0–4 |

## **4. Calculate the Weighted Security Score**

Use the following formula:

\[
S=\sum_{i=1}^{8}W_i\times L_i
\]

Where:

- \(S\) = Overall weighted security score.
- \(W_i\) = Weight of each domain (decimal).
- \(L_i\) = Assigned maturity level (0–4).

The final score ranges from **0.0 to 4.0**.

### **Example Calculation**

| Domain | Weight | Assigned Level | Weighted Score |
| --- | --- | --- | --- |
| Governance | 0.10 | 2 | 0.20 |
| Identity and Access | 0.15 | 2 | 0.30 |
| Policy Enforcement | 0.20 | 3 | 0.60 |
| Isolation | 0.15 | 2 | 0.30 |
| Supply Chain | 0.10 | 2 | 0.20 |
| CI/CD and Production | 0.15 | 3 | 0.45 |
| Observability and Response | 0.10 | 2 | 0.20 |
| Threat Intelligence and Testing | 0.05 | 1 | 0.05 |
| **Total** | **1.00** |  | **2.30** |

**Overall weighted security score: 2.30 out of 4.0**

## **5. Risk Evaluation and Prioritization**

Review the identified security findings and prioritize remediation according to their severity and potential impact.

| Priority | Required Action |
| --- | --- |
| Critical | Address immediately. |
| High | Prioritize for urgent remediation. |
| Medium | Schedule remediation based on risk. |
| Low | Address through routine improvements. |
- Compare findings with the [Common Copilot Misconfigurations](https://aisecuritylabs.org/resources/copilot-misconfigurations/?utm_source=chatgpt.com).
- Record the corresponding misconfiguration IDs.
- Identify security gaps across the eight assessment domains.
- Prioritize remediation using the recommended [fix order](https://aisecuritylabs.org/resources/copilot-misconfigurations/?utm_source=chatgpt.com#fix-first).

## **6. Security Framework Mapping**

Map assessment findings to relevant security frameworks to organize and communicate identified risks.

| Framework | Purpose |
| --- | --- |
| OWASP Top 10 for Agentic Applications | Identify security risks associated with AI agents and their capabilities. |
| MITRE ATLAS | Map AI-related threats and adversarial techniques. |
| NIST AI RMF | Organize AI risk management activities. |

## **7. Prepare the Security Assessment Report**

Prepare a professional report containing the following sections:

1. **Executive Summary:** Overall security posture, maturity score, and major findings.
2. **Assessment Scope:** Environments, repositories, and systems included in the assessment.
3. **Assessment Methodology:** Assessment phases and testing procedures.
4. **Domain Maturity Scores:** Individual domain scores and overall weighted score.
5. **Security Findings:** Identified risks, misconfiguration IDs, and supporting evidence.
6. **Risk Evaluation:** Severity, potential impact, and remediation priority.
7. **Recommendations:** Proposed security controls and remediation measures.
8. **Improvement Roadmap:** Prioritized actions for improving security maturity.

## **8. Develop a Risk-Based Improvement Roadmap**

Organize remediation activities according to their security priority.

| Priority | Improvement Focus |
| --- | --- |
| 1 | Resolve Critical and High-risk misconfigurations. |
| 2 | Strengthen identity, access, and policy enforcement. |
| 3 | Improve sandboxing, isolation, and supply-chain security. |
| 4 | Secure Cloud Agent, CI/CD, and production access. |
| 5 | Improve monitoring, incident response, and threat testing. |
| 6 | Reassess maturity and track improvements quarterly. |

## **9. Deliverables**

By the end of this lab, learners should produce:

- Completed eight-domain maturity assessment.
- Evidence supporting each maturity score.
- Weighted overall security score.
- Risk-prioritized security findings.
- Mapping of findings to OWASP Top 10 for Agentic Applications, MITRE ATLAS, and NIST AI RMF.
- Professional GitHub Copilot security assessment report.
- Risk-based security improvement roadmap.