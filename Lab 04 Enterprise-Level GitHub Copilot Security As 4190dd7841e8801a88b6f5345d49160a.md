# Lab 04: Enterprise-Level GitHub Copilot Security Assessment

**Type:** Theory + Hands-on

**Level:** Intermediate–Advanced

**Duration:** 90 minutes

## **1. Objective**

Conduct an enterprise-level assessment of GitHub Copilot security controls. Evaluate governance, identity, policy enforcement, isolation, supply-chain security, CI/CD, observability, and threat intelligence.

## **2. Enterprise Security Assessment**

### **Domain 1: Governance**

Evaluate organizational governance and accountability.

- Approved AI-assisted development security policy.
- Named owners for security policies and controls.
- Defined responsibilities for MCP, extensions, monitoring, and incident response.
- Security framework alignment.

**Evidence:** Approved policies, ownership records, and framework mappings.

### **Domain 2: Identity and Access**

Evaluate authentication and access management.

- SSO and phishing-resistant MFA.
- Copilot seat assignment and quarterly reviews.
- Restricted Cloud Agent issue assignment permissions.
- Fine-grained, repository-scoped automation tokens.

**Evidence:** Identity policies, seat reports, and token permission records.

### **Domain 3: Policy Enforcement**

Assess centralized configuration and policy enforcement.

- VS Code policies deployed through MDM, Windows registry, or `/etc/vscode/policy.json`.
- Global auto-approval disabled and agent sandbox enabled.
- MCP servers and hooks restricted through managed policies.
- Extensions restricted through `AllowedExtensions`.
- Copilot organization policies configured for features, models, MCP, and Cloud Agent access.

**Evidence:** Policy files, MDM profiles, and organizational policy settings.

### **Domain 4: Isolation**

Evaluate endpoint and network isolation controls.

- EDR protection on developer hosts.
- EDR coverage in WSL, dev containers, and Codespaces where required.
- Corporate proxy and certificate authority configuration.
- Network egress allowlists.
- Standard containers or Codespaces without credentials for untrusted code.

**Evidence:** EDR reports, network policies, and sandbox test results.

### **Domain 5: Supply Chain**

Assess the security of external tools and dependencies.

- MCP server and extension allowlists.
- Third-party integration review.
- Dependency and package controls.
- Configuration and setup-step review.
- Protection against untrusted repository instructions.

**Evidence:** Allowlists, intake records, and dependency review records.

### **Domain 6: CI/CD and Production**

Evaluate Cloud Agent, workflow, and production access security.

- Cloud Agent restricted to repositories with appropriate rulesets.
- Required reviews and passing checks on `copilot/` branches.
- Agent firewall enabled.
- Workflow execution requires approval.
- Setup steps pinned and reviewed.
- CODEOWNERS configured for sensitive configuration files.
- No standing agent write access to production.

**Evidence:** Repository rulesets, workflow files, branch protection settings, and production access records.

### **Domain 7: Observability and Response**

Evaluate enterprise monitoring and incident response.

- Enterprise audit logs streamed to the SIEM.
- Required log retention policies enforced.
- Detections for agent activity and configuration changes.
- Alerts for new MCP servers and changes to `.vscode/settings.json`.
- Incident response runbooks maintained.
- Tabletop exercise conducted within the last 12 months.

**Evidence:** SIEM records, detection rules, runbooks, and tabletop reports.

### **Domain 8: Threat Intelligence and Testing**

Evaluate ongoing security awareness and testing.

- Microsoft and GitHub security advisories monitored.
- Regular security updates shared with teams.
- Technical security tests repeated after upgrades and policy changes.
- Copilot included in annual penetration testing or red-team exercises.

**Evidence:** Advisory tracking records, test results, and penetration testing reports.

## **3. Assessment Checklist**

- [ ]  Review enterprise governance and security ownership.
- [ ]  Assess identity and access controls.
- [ ]  Verify centralized policy enforcement.
- [ ]  Evaluate endpoint and network isolation.
- [ ]  Review MCP, extension, and supply-chain controls.
- [ ]  Assess CI/CD and production access restrictions.
- [ ]  Verify audit logging, detections, and incident response.
- [ ]  Review threat intelligence and security testing practices.
- [ ]  Collect supporting evidence for all eight domains.