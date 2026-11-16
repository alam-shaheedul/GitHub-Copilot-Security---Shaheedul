# Lab 05: Security Maturity Scoring, Risk Evaluation, and Improvement Roadmap

**Type:** Hands-on

**Level:** Advanced

**Duration:** 90 minutes

## Introduction

Security maturity scoring evaluates how effectively an organization manages GitHub Copilot security across its assessment domains.

This lab uses the five-level maturity model and weighted scoring method to identify security gaps, prioritize findings, map risks to security frameworks, and prepare an improvement roadmap.

![Security_Maturity_Levels.png](Lab%2005%20Security%20Maturity%20Scoring,%20Risk%20Evaluation,/Security_Maturity_Levels.png)

## Lab Overview

In this lab, you will:

- Understand the five-level security maturity model.
- Assign maturity levels to eight assessment domains.
- Calculate the weighted security score.
- Evaluate and prioritize security findings.
- Map findings to OWASP, MITRE ATLAS, and NIST AI RMF.
- Prepare a professional security assessment report.

## Concepts Explained

### Security Maturity Model

A maturity model measures how effectively an organization implements, manages, monitors, and improves its security controls.

### Weighted Security Score

A weighted score combines individual domain maturity levels according to their assigned importance.

### Risk Evaluation

Risk evaluation examines the severity and potential impact of identified security weaknesses.

### Improvement Roadmap

An improvement roadmap defines prioritized actions to address security gaps and improve maturity over time.

## Hands-on: Security Maturity Assessment

### Step 1: Create the Assessment Workspace

```bash
mkdir -p ~/copilot-assessment-lab/maturity
cd ~/copilot-assessment-lab/maturity
```

Create a scoring file:

```bash
nano maturity-scores.csv
```

Add:

```
Domain,Weight,Level
Governance,0.10,0
Identity and Access,0.15,0
Policy Enforcement,0.20,0
Isolation,0.15,0
Supply Chain,0.10,0
CI/CD and Production,0.15,0
Observability and Response,0.10,0
Threat Intelligence and Testing,0.05,0
```

Replace the initial levels with the maturity levels supported by your assessment evidence.

### Step 2: Understand the Five-Level Maturity Model

| Level | Name | Description |
| --- | --- | --- |
| 0 | Unmanaged | Personal accounts, no policy, and no visibility. |
| 1 | Aware | Policy written, approved accounts, trained developers, and some user-level settings. |
| 2 | Managed | Managed settings enforced across the fleet, sandbox enabled, MCP and plugin allowlists, and telemetry enabled. |
| 3 | Monitored | Tested detections, isolated CI agents, enforced version requirements, and advisory-driven patching. |
| 4 | Optimised | Automated attack testing, metrics-driven policies, scoped agent identities, and verified production access restrictions. |

A recommended initial target is:

- Level 2 across all domains.
- Level 3 for Policy Enforcement.
- Level 3 for Isolation.
- Level 3 for CI/CD and Production.

### Step 3: Assign Domain Maturity Levels

Evaluate the eight domains using the collected assessment evidence.

| Domain | Weight | Evidence to Collect |
| --- | --- | --- |
| Governance | 10% | Policies, owners, framework mapping. |
| Identity and Access | 15% | SSO, SCIM, login enforcement, CI identity. |
| Policy Enforcement | 20% | VS Code policies, MDM profiles, Copilot organization policies, audit reports. |
| Isolation | 15% | Sandbox settings and technical test results. |
| Supply Chain | 10% | Allowlists, pinning, intake records. |
| CI/CD and Production | 15% | Workflow review, branch protection, production access review. |
| Observability and Response | 10% | Telemetry, detections, tabletop results. |
| Threat Intelligence and Testing | 5% | Advisory tracking, test results. |

Assign each domain a level from 0 to 4.

Do not assign a high maturity level without supporting evidence.

### Step 4: Calculate the Weighted Security Score

Use the following formula:

[

S=\sum_{i=1}^{8}W_i\times L_i

]

Where:

- (S) = Overall weighted security score.
- (W_i) = Weight of each domain expressed as a decimal.
- (L_i) = Assigned maturity level from 0 to 4.

The final score ranges from 0.0 to 4.0.

Create a scoring script:

```bash
nano score.py
```

Add:

```python
import csv

total = 0.0

with open("maturity-scores.csv", newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        weight = float(row["Weight"])
        level = int(row["Level"])

        if not 0 <= level <= 4:
            raise ValueError("Maturity level must be between 0 and 4")

        score = weight * level
        total += score

        print(f'{row["Domain"]}: {score:.2f}')

print(f"\nWeighted Security Score: {total:.2f} / 4.00")
```

Run:

```bash
python3 score.py
```

The script calculates the weighted score using the levels entered in the CSV file.

### Step 5: Evaluate Security Risks

Create a findings file:

```bash
nano security-findings.csv
```

Use the following structure:

```
Finding ID,Description,Severity,Domain,Recommendation
F01,Example security weakness,Critical,Policy Enforcement,Apply the recommended security control
F02,Example security weakness,High,Isolation,Restrict agent permissions
F03,Example security weakness,Medium,Supply Chain,Review and restrict integrations
```

Replace the sample findings with actual assessment results.

Prioritize findings using the following order:

| Priority | Action |
| --- | --- |
| Critical | Address immediately. |
| High | Prioritize for urgent remediation. |
| Medium | Schedule remediation based on risk. |
| Low | Address through routine improvements. |

Compare findings with the [Common Copilot Misconfigurations](https://aisecuritylabs.org/resources/copilot-misconfigurations/) and record the corresponding misconfiguration IDs.

### Step 6: Map Findings to Security Frameworks

Map the identified findings to relevant frameworks.

| Framework | Purpose |
| --- | --- |
| OWASP Top 10 for Agentic Applications | Identify risks associated with AI agents and their capabilities. |
| MITRE ATLAS | Map AI-related threats and adversarial techniques. |
| NIST AI RMF | Organize AI risk management activities. |

Use the relevant framework categories and techniques to support risk analysis and communicate findings.

### Step 7: Prepare the Security Assessment Report

Create the report:

```bash
nano security-assessment-report.md
```

Include the following sections:

```
1. Executive Summary
2. Assessment Scope
3. Assessment Methodology
4. Eight-Domain Maturity Scores
5. Overall Weighted Security Score
6. Security Findings and Evidence
7. Risk Evaluation and Prioritization
8. Security Framework Mapping
9. Remediation Recommendations
10. Risk-Based Improvement Roadmap
```

### Step 8: Develop the Improvement Roadmap

Organize remediation activities according to security priority.

| Priority | Improvement Focus |
| --- | --- |
| 1 | Resolve Critical and High-risk misconfigurations. |
| 2 | Strengthen identity, access, and policy enforcement. |
| 3 | Improve sandboxing, isolation, and supply-chain controls. |
| 4 | Secure Cloud Agent, CI/CD, and production access. |
| 5 | Improve monitoring, incident response, and threat testing. |
| 6 | Reassess maturity and track improvements quarterly. |

## Conclusion

You have completed a GitHub Copilot security maturity assessment using domain scoring, weighted calculations, risk prioritization, and security framework mapping. The final report and improvement roadmap provide a basis for tracking security improvements through quarterly reassessments.

**Reference:** [GitHub Copilot Security Assessment – AI Security Labs](https://aisecuritylabs.org/resources/copilot-assessment/)