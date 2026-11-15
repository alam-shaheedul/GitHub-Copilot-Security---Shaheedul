# LAB 01 — Introduction to GitHub Copilot Security Misconfigurations

**Type:** Theoretical

**Level:** Beginner

**Duration:** 45 Minutes

## **1. Objective**

Understand GitHub Copilot's security architecture, common attack surfaces, and the 19 identified security misconfigurations.

## **2. Understanding GitHub Copilot Security**

**GitHub Copilot** is an AI-powered coding assistant that can generate, explain, and modify code. Its agentic capabilities also allow it to interact with files, execute terminal commands, and use external tools.

These capabilities introduce security risks when agents operate with excessive permissions or interact with untrusted content.

### **Key Security Concepts**

| Concept | Description |
| --- | --- |
| AI Coding Agent | AI system capable of performing development tasks. |
| Prompt Injection | Malicious instructions that manipulate AI behavior. |
| Attack Surface | Components or entry points that attackers may exploit. |
| Trust Boundary | Separation between trusted and untrusted components. |
| Excessive Permissions | Granting an agent more privileges than necessary. |
| Least Privilege | Providing only the permissions required for a task. |

## **3. Common Copilot Attack Surfaces**

- Repository files and project instructions.
- Workspace and user configurations.
- Terminal and file-editing tools.
- MCP servers and external integrations.
- Copilot CLI and Cloud Agent.
- Secrets, credentials, and development environments.

## **4. The 19 Security Misconfigurations**

The following misconfigurations are grouped according to their security severity.

| ID | Misconfiguration | Severity |
| --- | --- | --- |
| X1 | Global auto-approval enabled | Critical |
| X2 | Workspace Trust disabled or unsafe folders trusted | Critical |
| X3 | Broad terminal or file-edit auto-approval | High |
| X4 | Sandbox disabled or network unrestricted | High |
| X5 | Outdated Copilot development tools | High |
| X6 | Assigning unread issues to Cloud Agent | Critical |
| X7 | Opening Codespaces from unread issues | High |
| X8 | Untrusted MCP servers | High |
| X9 | Unreviewed instruction files | High |
| X10 | Unsafe Cloud Agent setup steps | High |
| X11 | Insecure Cloud Agent firewall and MCP secrets | High |
| X12 | Copilot CLI permission bypass | High |
| X13 | Malicious symbolic links | High |
| X14 | Exposed repository secrets | High |
| X15 | Unreviewed hooks, plugins, and marketplaces | Medium |
| X16 | Untrusted `.git/config` files | Medium |
| X17 | Treating content exclusions as a security boundary | Medium |
| X18 | Relying on individual settings instead of policies | Medium |
| X19 | Not exporting Copilot audit logs | Medium |

## **5. Security Severity Overview**

| Severity | Number |
| --- | --- |
| Critical | 3 |
| High | 11 |
| Medium | 5 |
| **Total** | **19** |