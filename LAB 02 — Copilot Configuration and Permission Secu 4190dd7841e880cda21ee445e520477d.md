# LAB 02 — Copilot Configuration and Permission Security

**Type:** Theory + Hands-on

**Level:** Beginner–Intermediate

**Duration:** 60 Minutes

## **1. Objective**

Identify and secure common GitHub Copilot configuration and permission weaknesses in Visual Studio Code.

## **2. Required Environment**

- Visual Studio Code.
- GitHub account.
- GitHub Copilot extension.
- A test project or repository.

## **3. Misconfigurations Covered**

| ID | Misconfiguration | Security Risk |
| --- | --- | --- |
| X1 | Global auto-approval enabled | Actions execute without individual confirmation. |
| X2 | Workspace Trust disabled | Untrusted project configurations may influence the environment. |
| X3 | Broad terminal or file-edit auto-approval | Dangerous commands or modifications may be approved automatically. |
| X5 | Outdated development tools | Known vulnerabilities may remain unpatched. |

## **4. Practical Activities**

### **Task 1: Check Copilot Installation and Version**

1. Open Visual Studio Code.
2. Navigate to Extensions.
3. Search for GitHub Copilot.
4. Check the installed version.
5. Check for available updates.

**Expected Result:** Copilot and the development environment should be updated.

### **Task 2: Configure Workspace Trust**

1. Open VS Code Settings.
2. Search for `Workspace Trust`.
3. Locate `Security: Workspace: Trust Enabled`.
4. Ensure Workspace Trust is enabled.
5. Open an unfamiliar test project in Restricted Mode.

**Expected Result:** Unknown workspaces should not automatically receive full trust.

### **Task 3: Review Global Auto-Approval**

1. Open VS Code Settings.
2. Search for `chat.tools.global.autoApprove`.
3. Check whether global auto-approval is enabled.
4. Disable global auto-approval if enabled.

Relevant setting:

```
{
  "chat.tools.global.autoApprove": false
}
```

**Expected Result:** Copilot should not globally bypass tool approval requirements.

### **Task 4: Review Terminal and File-Edit Permissions**

1. Open VS Code settings.
2. Review terminal auto-approval lists.
3. Review file-edit auto-approval lists.
4. Identify broad patterns or dangerous commands.
5. Remove unnecessary automatic approvals.

**Expected Result:** Only explicitly justified, low-risk operations should be automatically approved.

## **5. Security Checklist**

- [ ]  Copilot and VS Code are updated.
- [ ]  Workspace Trust is enabled.
- [ ]  Unknown projects are opened in Restricted Mode.
- [ ]  Global auto-approval is disabled.
- [ ]  Broad terminal approval rules are removed.
- [ ]  Broad file-edit approval rules are removed.