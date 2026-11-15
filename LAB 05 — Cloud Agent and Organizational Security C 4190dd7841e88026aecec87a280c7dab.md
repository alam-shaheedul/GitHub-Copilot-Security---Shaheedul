# LAB 05 — Cloud Agent and Organizational Security Configuration

**Type:** Theory + Hands-on

**Level:** Advanced

**Duration:** 90 Minutes

## **1. Objective**

Understand and secure GitHub Copilot Cloud Agent configurations, repository access, setup workflows, organizational policies, and centralized security monitoring.

## **2. Required Environment**

- GitHub account.
- Test GitHub repository.
- GitHub Copilot access with Cloud Agent availability.
- Repository administration permissions for relevant activities.
- Access to organizational settings where available.

## **3. Misconfigurations Covered**

| ID | Misconfiguration | Security Risk |
| --- | --- | --- |
| X6 | Assigning unread issues to Cloud Agent | Malicious issue instructions may manipulate the agent. |
| X7 | Opening Codespaces from unread issues | Prompt injection through untrusted issue content. |
| X10 | Unsafe Cloud Agent setup steps | Execution of untrusted downloaded code. |
| X11 | Insecure firewall and MCP secrets | Unauthorized network access and credential exposure. |
| X18 | Relying on individual settings instead of policies | Inconsistent security enforcement. |
| X19 | Not exporting Copilot audit logs | Limited centralized monitoring and investigation. |

## **4. Practical Activities**

### **Task 1: Review Cloud Agent Issue Assignment**

1. Open a test GitHub repository.
2. Navigate to its Issues section.
3. Review an issue before assigning it to Copilot.
4. Identify suspicious instructions or hidden content.
5. Inspect the resulting pull request before accepting changes.

**Expected Result:** Issues are reviewed before assignment, and generated changes receive appropriate review.

### **Task 2: Review Codespaces Security**

1. Select an issue in the test repository.
2. Review its contents before launching a Codespace.
3. Identify untrusted instructions.
4. Understand how issue content can influence Copilot.

**Expected Result:** Codespaces are launched only from reviewed content.

### **Task 3: Review Cloud Agent Setup Workflows**

1. Locate `copilot-setup-steps.yml`.
2. Review the workflow commands.
3. Identify external downloads and execution steps.
4. Check whether GitHub Actions are pinned by commit SHA.
5. Remove unsafe download-and-execute patterns.

**Expected Result:** Setup workflows should use trusted sources and verified dependencies.

### **Task 4: Review Firewall and MCP Secrets**

1. Open the Cloud Agent environment configuration.
2. Review firewall settings.
3. Identify unnecessary network access.
4. Inspect configured MCP tools.
5. Review the secrets supplied to MCP servers.
6. Restrict secrets to those required by each integration.

**Expected Result:** Firewall restrictions remain enabled and MCP servers receive only necessary secrets.

### **Task 5: Review Organizational Policies**

1. Examine the available VS Code enterprise policies.
2. Review the following security controls:
    - `ChatToolsAutoApprove`
    - `ChatAgentSandboxEnabled`
    - `ChatMCP`
    - `ChatAgentExtensionTools`
    - `ChatAllowManagedHooksOnly`
3. Understand how centrally managed policies differ from individual developer settings.
4. Identify security settings that should be enforced organization-wide.

**Expected Result:** Important security configurations should be centrally enforced rather than relying exclusively on individual developers.

### **Task 6: Review Copilot Audit Logs**

1. Open GitHub organization settings.
2. Locate the available audit log functionality.
3. Identify Copilot-related audit events.
4. Review available export or streaming options.
5. Understand the importance of SIEM integration and log retention.

**Expected Result:** Organizations should have a centralized process for collecting and retaining relevant Copilot audit logs.

## **5. Security Checklist**

- [ ]  Issues are reviewed before Cloud Agent assignment.
- [ ]  Codespaces are opened from reviewed content.
- [ ]  Cloud Agent setup workflows are inspected.
- [ ]  External actions are pinned by SHA.
- [ ]  Firewall restrictions are maintained.
- [ ]  MCP tools and secrets are restricted.
- [ ]  Organizational security policies are reviewed.
- [ ]  Copilot audit logs are exported or streamed centrally.