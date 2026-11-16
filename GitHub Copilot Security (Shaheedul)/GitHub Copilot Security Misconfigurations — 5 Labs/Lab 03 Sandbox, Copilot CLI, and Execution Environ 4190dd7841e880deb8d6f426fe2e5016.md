# Lab 03: Sandbox, Copilot CLI, and Execution Environment Security

**Type:** Hands-on

**Level:** Intermediate

**Duration:** 60 minutes

## Introduction

GitHub Copilot agents can execute terminal commands and interact with the development environment. Without appropriate sandboxing and permission restrictions, an agent may access sensitive files, execute unsafe commands, or communicate with external networks.

This lab demonstrates how to inspect sandbox configurations and secure the Copilot CLI execution environment.

![Sandbox_and_CLI_Permissions.png](Lab%2003%20Sandbox,%20Copilot%20CLI,%20and%20Execution%20Environ/Sandbox_and_CLI_Permissions.png)

## Lab Overview

In this lab, you will:

- Understand agent sandboxing.
- Inspect VS Code sandbox configurations.
- Configure network restrictions.
- Review Copilot CLI permission settings.
- Disable permission bypass options.
- Verify the security configurations.

## Concepts Explained

### Agent Sandboxing

Sandboxing restricts an agent's access to the host environment, files, and system resources.

### Network Isolation

Network isolation limits an agent's ability to communicate with external systems.

### Copilot CLI Permissions

Copilot CLI permissions determine which tools and commands the agent can execute.

### Permission Bypass

Permission bypass options allow the CLI to execute actions without normal approval requirements. Such options should be restricted.

## Hands-on: Configuring Sandbox and CLI Security

### Step 1: Create the Lab Workspace

```bash
mkdir -p ~/copilot-misconfig-lab/lab03
cd ~/copilot-misconfig-lab/lab03
```

### Step 2: Create a Sample VS Code Settings File

```bash
mkdir -p .vscode
nano .vscode/settings.json
```

Add the following intentionally insecure configuration:

```json
{
  "chat.agent.sandbox.enabled": "off",
  "chat.agent.sandbox.allowNetwork": true
}
```

Save the file.

### Step 3: Inspect the Insecure Settings

```bash
cat .vscode/settings.json
```

The configuration contains two weaknesses:

- The agent sandbox is disabled.
- Network access is allowed.

### Step 4: Enable the VS Code Agent Sandbox

Edit the configuration:

```bash
nano .vscode/settings.json
```

Replace the previous configuration with:

```json
{
  "chat.agent.sandbox.enabled": "on",
  "chat.agent.sandbox.allowNetwork": false,
  "chat.agent.allowedNetworkDomains": []
}
```

Save the file.

### Step 5: Configure Copilot CLI Security

Create the CLI configuration directory:

```bash
mkdir -p ~/.copilot
```

Create the settings file:

```bash
nano ~/.copilot/settings.json
```

Add:

```json
{
  "sandbox": {
    "enabled": true,
    "allowBypass": false
  },
  "permissions": {
    "disableBypassPermissionsMode": "disable"
  },
  "allowedUrls": [],
  "deniedUrls": []
}
```

Save the file.

### Step 6: Verify the Configurations

Validate the VS Code configuration:

```bash
jq . .vscode/settings.json
```

Validate the CLI configuration:

```bash
jq . ~/.copilot/settings.json
```

Check the sandbox settings:

```bash
jq '{
  sandbox: .sandbox,
  permissions: .permissions
}' ~/.copilot/settings.json
```

Expected results:

- VS Code agent sandbox is enabled.
- VS Code sandbox network access is disabled.
- Copilot CLI sandbox is enabled.
- Permission bypass mode is disabled.

**Important:** These commands create configuration files; they do not prove that the installed VS Code or CLI has activated the controls. Verify the settings in the actual application and test them in a disposable environment. On Linux, VS Code sandboxing may require `bubblewrap` and `socat`; native Windows uses a separate experimental setting.

## Conclusion

You have configured sample sandbox and CLI security settings to restrict agent execution and prevent permission bypass. Proper sandboxing and network restrictions help limit the impact of unsafe agent actions.

**Reference:** [VS Code Agent Sandboxing](https://code.visualstudio.com/docs/agents/run/agent-sandboxing) | [Copilot CLI Configuration](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-config-dir-reference)

---