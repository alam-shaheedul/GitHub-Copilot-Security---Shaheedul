# Lab 04: Enterprise-Level GitHub Copilot Security Assessment

**Type:** Theory + Hands-on

**Level:** Intermediate–Advanced

**Duration:** 90 minutes

## Introduction

Enterprise-level GitHub Copilot security assessment evaluates security controls across the entire organization.

It examines governance, identity, centralized policy enforcement, isolation, supply-chain security, CI/CD, production access, monitoring, and threat intelligence.

This lab uses the enterprise checklist to assess the effectiveness of centralized security controls and collect supporting evidence.

![Enterprise_Policy_Enforcement.png](Lab%2004%20Enterprise-Level%20GitHub%20Copilot%20Security%20As/Enterprise_Policy_Enforcement.png)

## Lab Overview

In this lab, you will:

- Review enterprise security governance.
- Examine identity and access controls.
- Evaluate centralized policy enforcement.
- Assess isolation and network restrictions.
- Review supply-chain and CI/CD security.
- Examine observability and incident response.
- Collect evidence across eight security domains.

## Concepts Explained

### Enterprise Governance

Enterprise governance establishes security policies, responsibilities, ownership, and accountability for Copilot usage.

### Centralized Policy Enforcement

Centralized policy enforcement ensures that security settings are consistently applied across developer environments.

### Endpoint and Network Isolation

Endpoint and network isolation restrict the resources and external systems accessible to Copilot agents.

### Observability

Observability provides visibility into agent activities through audit logs, security detections, and monitoring systems.

## Hands-on: Conducting an Enterprise Security Assessment

Create an assessment workspace:

```bash
mkdir -p ~/copilot-assessment-lab/enterprise
cd ~/copilot-assessment-lab/enterprise
```

Create an evidence directory:

```bash
mkdir -p evidence/governance \
evidence/identity \
evidence/policy \
evidence/isolation \
evidence/supply-chain \
evidence/cicd \
evidence/observability \
evidence/threat-intelligence
```

### Domain 1: Governance

Review:

- Approved AI-assisted development security policy.
- Named owners for VS Code and Copilot organization policies.
- MCP and extension approval responsibilities.
- Security detection and incident response ownership.
- Framework alignment.

Collect approved policies and ownership records.

### Domain 2: Identity and Access

Review:

- GitHub SSO and phishing-resistant MFA.
- Copilot seat assignment through teams.
- Quarterly access reviews.
- Cloud Agent issue assignment permissions.
- Fine-grained, repository-scoped automation tokens.

Collect identity policies, seat reports, and access review records.

### Domain 3: Policy Enforcement

Review centrally managed VS Code policies.

Examine the following controls:

| Policy | Expected Configuration |
| --- | --- |
| `ChatToolsAutoApprove` | Off |
| `ChatAgentSandboxEnabled` | On |
| `ChatMCP` or `ChatAllowedMcpServers` | Restricted to approved MCP servers |
| `ChatAllowManagedHooksOnly` | Managed hooks only |
| `AllowedExtensions` | Approved extensions only |

Also verify:

- Policies are deployed through MDM, Windows registry, or `/etc/vscode/policy.json`.
- A sample of developer devices receives the policies.
- Copilot organization policies restrict features, models, MCP servers, and Cloud Agent access.

Collect policy files, MDM profiles, and verification records.

### Domain 4: Isolation

Review:

- EDR protection on developer hosts.
- EDR coverage in WSL, dev containers, and Codespaces where required.
- Corporate proxy and certificate authority configuration.
- Network egress allowlists.
- Standard containers or Codespaces without credentials for untrusted code.

Collect EDR reports, network policies, and sandbox test results.

### Domain 5: Supply Chain

Review:

- Approved MCP server allowlists.
- Extension and plugin approval processes.
- Third-party integration security.
- Package and dependency controls.
- Version pinning and setup-step reviews.

Collect allowlists, intake records, and dependency review evidence.

### Domain 6: CI/CD and Production

Review:

- Cloud Agent enabled only on approved repositories.
- Branch protection and required reviews.
- Required status checks on `copilot/` branches.
- Agent firewall enabled.
- Approval required before running workflows.
- Reviewed and pinned setup steps.
- CODEOWNERS protection for `.github/`, `.vscode/`, instruction files, and lockfiles.
- No standing agent write access to production.

Collect workflow files, ruleset configurations, branch protection settings, and production access records.

### Domain 7: Observability and Response

Review:

- Enterprise audit log streaming to the SIEM.
- Log retention beyond 180 days where policy requires.
- Detections for agent activities.
- Alerts for changes to `.vscode/settings.json`.
- Alerts for new MCP servers.
- Incident response runbooks.
- Tabletop exercise completed within the last 12 months.

Collect SIEM records, detection rules, runbooks, and tabletop results.

### Domain 8: Threat Intelligence and Testing

Review:

- Microsoft and GitHub security advisories.
- Regular security updates for the team.
- Repeated technical tests after upgrades and policy changes.
- Copilot coverage in annual penetration testing or red-team exercises.

Collect advisory tracking records, test reports, and penetration testing evidence.

### Step 3: Organize Enterprise Evidence

Create an evidence index:

```bash
nano evidence-index.md
```

Use the following structure:

```
1. Governance
   - Approved policy
   - Security ownership records
   - Framework mapping

2. Identity and Access
   - SSO and MFA evidence
   - Copilot seat report
   - Access review records

3. Policy Enforcement
   - Managed policy files
   - MDM profiles
   - Verification records

4. Isolation
   - EDR reports
   - Network policies
   - Sandbox test results

5. Supply Chain
   - MCP allowlists
   - Extension approval records
   - Dependency review

6. CI/CD and Production
   - Workflow review
   - Branch protection
   - Production access review

7. Observability and Response
   - SIEM records
   - Detection rules
   - Incident response runbooks

8. Threat Intelligence and Testing
   - Security advisories
   - Technical test results
   - Penetration testing reports
```

Save the actual evidence in the corresponding directories.

## Conclusion

You have evaluated enterprise GitHub Copilot security across eight domains and organized the supporting evidence. These records provide the foundation for enterprise maturity scoring and risk-based security improvement.

**Reference:** [GitHub Copilot Security Assessment – Enterprise Checklist](https://aisecuritylabs.org/resources/copilot-assessment/)