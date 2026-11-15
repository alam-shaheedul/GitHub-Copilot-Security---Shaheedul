# LAB 03 — Sandbox, Copilot CLI, and Execution Environment Security

**Type:** Hands-on

**Level:** Intermediate

**Duration:** 60 Minutes

## **1. Objective**

Understand and configure execution restrictions for GitHub Copilot agents, including sandboxing, network access, and Copilot CLI permissions.

## **2. Required Environment**

- Visual Studio Code.
- GitHub Copilot.
- Copilot CLI.
- A non-production test environment.

## **3. Misconfigurations Covered**

| ID | Misconfiguration | Security Risk |
| --- | --- | --- |
| X4 | Sandbox disabled or network unrestricted | Agent commands may access unrestricted resources. |
| X12 | CLI permission bypass | Commands may execute without normal approval. |
| X17 | Content exclusions treated as a security boundary | Sensitive files may remain accessible to agents. |

## **4. Practical Activities**

### **Task 1: Configure VS Code Agent Sandbox**

1. Open VS Code Settings.
2. Search for `chat.agent.sandbox.enabled`.
3. Enable agent sandboxing.
4. Search for `chat.agent.sandbox.allowNetwork`.
5. Disable network access for the sandbox.

Relevant settings:

```
{
  "chat.agent.sandbox.enabled": "on",
  "chat.agent.sandbox.allowNetwork": false
}
```

**Expected Result:** Agent execution should operate with sandbox restrictions and without unnecessary network access.

### **Task 2: Review Copilot CLI Sandbox**

1. Open the Copilot CLI environment.
2. Locate its sandbox configuration.
3. Check whether sandboxing is enabled.
4. Enable sandboxing where supported.
5. Review the available execution restrictions.

**Expected Result:** Copilot CLI should not operate with unnecessary unrestricted execution privileges.

### **Task 3: Review CLI Permission Bypass**

1. Inspect the commands or scripts used to launch Copilot CLI.
2. Identify allow-all flags and `-yolo` aliases.
3. Review saved approvals in `permissions-config.json`, where applicable.
4. Remove unnecessary permission bypasses.
5. Review the CLI permission configuration.

**Expected Result:** The CLI should retain appropriate approval requirements.

### **Task 4: Understand Content Exclusion Limitations**

1. Open GitHub Copilot settings.
2. Locate content exclusion configurations.
3. Review which Copilot features support exclusions.
4. Understand the limitations for Edit and Agent modes.
5. Identify why sensitive credentials should not be stored in accessible repositories.

**Expected Result:** Learners should understand that content exclusions are not a security boundary for agent access.

## **5. Security Checklist**

- [ ]  VS Code agent sandbox is enabled.
- [ ]  Unnecessary sandbox network access is disabled.
- [ ]  Copilot CLI sandbox is reviewed.
- [ ]  CLI permission bypass options are removed.
- [ ]  Saved approvals are reviewed.
- [ ]  Content exclusions are not relied upon to protect secrets.