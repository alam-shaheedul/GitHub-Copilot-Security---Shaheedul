# Lab 02: Copilot Configuration and Permission Security

**Type:** Theory + Hands-on

**Level:** Beginner–Intermediate

**Duration:** 60 minutes

## Introduction

GitHub Copilot operates using the permissions and configurations of its development environment. Insecure approval settings, disabled Workspace Trust, and excessive file-edit permissions can allow an agent to perform potentially dangerous actions.

This lab demonstrates how to inspect Copilot configurations, identify insecure settings, and apply basic security controls.

![Workspace_Trust_and_Approvals.png](Lab%2002%20Copilot%20Configuration%20and%20Permission%20Securi/Workspace_Trust_and_Approvals.png)

## Lab Overview

In this lab, you will:

- Inspect GitHub Copilot and VS Code configurations.
- Examine global auto-approval settings.
- Configure Workspace Trust.
- Review terminal and file-edit permissions.
- Identify insecure configurations.
- Apply recommended security settings.

## Concepts Explained

### Global Auto-Approval

Global auto-approval allows Copilot to execute tool calls without requesting individual user confirmation. Enabling it can expose the environment to unauthorized actions.

### Workspace Trust

Workspace Trust determines whether a project is trusted. Restricted Mode limits certain features when opening an untrusted project.

### Terminal Approval

Terminal approval controls whether Copilot can execute terminal commands automatically or requires user confirmation.

### File-Edit Approval

File-edit approval controls which files Copilot can modify without requesting permission.

## Hands-on: Inspecting and Securing Copilot Configurations

### Step 1: Create a Lab Workspace

Create a directory for the configuration exercises.

```bash
mkdir -p ~/copilot-misconfig-lab/lab02
cd ~/copilot-misconfig-lab/lab02
```

Verify the directory:

```bash
pwd
```

Expected output:

```
/home/poridhian/copilot-misconfig-lab/lab02
```

### Step 2: Create a Sample VS Code Configuration

Create a sample settings file:

```bash
mkdir -p .vscode
nano .vscode/settings.json
```

Add the following intentionally insecure configuration:

```json
{
  "chat.tools.global.autoApprove": true,
  "security.workspace.trust.enabled": false,
  "chat.tools.terminal.autoApprove": {
    "/.*/": true
  },
  "chat.tools.edits.autoApprove": {
    "**/*": true
  }
}
```

Save the file.

### Step 3: Inspect the Configuration

Display the configuration:

```bash
cat .vscode/settings.json
```

Validate its JSON syntax:

```bash
jq . .vscode/settings.json
```

The configuration contains several security weaknesses:

| Setting | Security Issue |
| --- | --- |
| `chat.tools.global.autoApprove` | Automatically approves all tool calls. |
| `security.workspace.trust.enabled` | Disables Workspace Trust. |
| `chat.tools.terminal.autoApprove` | Automatically approves terminal commands broadly. |
| `chat.tools.edits.autoApprove` | Allows broad file-edit approvals. |

### Step 4: Apply the Recommended Configuration

Replace the sample configuration with:

```bash
nano .vscode/settings.json
```

Use the following safer configuration:

```json
{
  "chat.tools.global.autoApprove": false,
  "chat.permissions.default": "default",
  "security.workspace.trust.enabled": true,
  "chat.tools.terminal.autoApprove": {
    "git status": true,
    "git diff": true,
    "git log": true,
    "ls": true,
    "pwd": true
  }
}
```

Save the file.

### Step 5: Verify the Configuration

Run:

```bash
jq . .vscode/settings.json
```

Check the important settings:

```bash
jq '{
  autoApprove: ."chat.tools.global.autoApprove",
  workspaceTrust: ."security.workspace.trust.enabled",
  terminalApprovals: ."chat.tools.terminal.autoApprove"
}' .vscode/settings.json
```

Expected results:

- Global auto-approval is disabled.
- Workspace Trust is enabled.
- Only selected read-only commands are automatically approved.
- Broad file-edit auto-approval is no longer configured.

**Note:** This exercise creates and validates a sample project configuration. For actual protection, apply the recommended settings to the VS Code user settings and enforce organization-managed policies where applicable. Project-level settings should not be treated as a security boundary.

## Conclusion

You have inspected an insecure Copilot configuration and replaced it with safer approval and Workspace Trust settings. These controls reduce the risk of unauthorized tool execution and file modification.

**Reference:** [VS Code AI Settings](https://code.visualstudio.com/docs/agents/reference/ai-settings) | [Tool Approvals](https://code.visualstudio.com/docs/agents/run/approvals)