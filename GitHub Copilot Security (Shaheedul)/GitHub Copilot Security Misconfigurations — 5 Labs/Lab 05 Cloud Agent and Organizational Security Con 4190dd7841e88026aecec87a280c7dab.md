# Lab 05: Cloud Agent and Organizational Security Configuration

**Type:** Theory + Hands-on

**Level:** Advanced

**Duration:** 90 minutes

## Introduction

GitHub Copilot Cloud Agent can work with repository issues, create pull requests, and execute development tasks in a cloud environment.

Insecure repository permissions, unsafe setup workflows, excessive MCP secrets, and weak organizational policies can expose enterprise resources.

This lab demonstrates how to review Cloud Agent configurations and examine organizational security controls.

![Cloud_Agent_Security.png](Lab%2005%20Cloud%20Agent%20and%20Organizational%20Security%20Con/Cloud_Agent_Security.png)

## Lab Overview

In this lab, you will:

- Understand Cloud Agent security risks.
- Review repository and issue assignment permissions.
- Inspect Cloud Agent setup workflows.
- Examine firewall and MCP secret configurations.
- Understand centralized organizational policies.
- Review audit logging requirements.

## Concepts Explained

### GitHub Copilot Cloud Agent

Cloud Agent performs coding tasks in a cloud-hosted environment. It can interact with repositories, execute setup steps, and create pull requests.

### Cloud Agent Firewall

The Cloud Agent firewall controls network access from the agent environment. It should remain enabled with an appropriately restricted allowlist.

### Organizational Policies

Organizational policies enforce security configurations across developer environments and Copilot features.

### Audit Logging

Audit logs provide records of relevant organizational activities and support security monitoring and investigation.

## Hands-on: Reviewing Cloud Agent Security

### Step 1: Create a Sample Repository Structure

```bash
mkdir -p ~/copilot-misconfig-lab/lab05/.github/workflows
cd ~/copilot-misconfig-lab/lab05
```

### Step 2: Create a Sample Cloud Agent Setup Workflow

Create the workflow file:

```bash
nano .github/workflows/copilot-setup-steps.yml
```

Add:

```yaml
name: Copilot Setup Steps

on:
  workflow_dispatch:

jobs:
  setup:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Display setup information
        run: echo "Copilot setup environment"
```

Save the file.

### Step 3: Inspect the Setup Workflow

Display the workflow:

```bash
cat .github/workflows/copilot-setup-steps.yml
```

Review the following:

- Third-party actions and their versions.
- Commands executed during setup.
- Downloaded scripts and dependencies.
- Access to secrets and external resources.

For production workflows, pin third-party actions to verified commit SHAs, review setup commands, and avoid downloading and executing untrusted code.

### Step 4: Review Cloud Agent Repository Controls

Open the repository on GitHub.

Navigate to:

**Repository → Settings → Copilot → Cloud Agent**

Review the available Cloud Agent settings and repository access.

Also examine:

**Repository → Settings → Rules → Rulesets**

Verify that:

- Cloud Agent is enabled only for approved repositories.
- Pull requests require appropriate reviews.
- Required status checks are configured.
- Rules protect `copilot/` branches.
- Sensitive workflow and configuration files receive appropriate CODEOWNERS protection.

### Step 5: Review Issue Assignment Permissions

Examine who can assign issues to Copilot Cloud Agent.

Verify that:

- Issues are reviewed before assignment.
- Only authorized users can assign issues.
- Untrusted issue content is treated as untrusted input.
- Generated pull requests receive line-by-line review.

Do not assign an unread or untrusted issue to Cloud Agent.

### Step 6: Review Firewall and MCP Secrets

In the Cloud Agent configuration, review:

- Whether the firewall is enabled.
- Whether the network allowlist is restricted.
- Whether MCP servers are approved.
- Whether MCP tools receive only the secrets they require.

Use narrowly scoped secrets with the `COPILOT_MCP_` prefix where required by the configured MCP integration.

Do not provide unnecessary repository or production credentials.

### Step 7: Examine the Organizational Policy Configuration

Create a sample VS Code enterprise policy file:

```bash
mkdir -p /tmp/copilot-policy-lab
cd /tmp/copilot-policy-lab
nano policy.json
```

Add:

```json
{
  "ChatToolsAutoApprove": false,
  "ChatAgentSandboxEnabled": true,
  "ChatMCP": "registry",
  "ChatAgentExtensionTools": false,
  "ChatAllowManagedHooksOnly": true
}
```

Save the file.

Validate the policy JSON:

```bash
jq . policy.json
```

These policies demonstrate controls for:

- Disabling global auto-approval.
- Enforcing agent sandboxing.
- Restricting MCP server configuration.
- Disabling third-party extension tools.
- Restricting hooks to managed sources.

**Note:** This is a sample policy file, not an automatically enforced configuration. Organizational administrators must deploy policies through the supported management mechanism. The MCP registry setting requires the appropriate registry configuration. Verify policy support for the installed VS Code version.

### Step 8: Review Content Exclusions and Audit Logging

Content exclusions should not be treated as a security boundary for Copilot agent mode.

Review the organization's enterprise audit log configuration.

Verify that:

- Copilot audit events are exported to the SIEM.
- Required retention policies are applied.
- Security teams can investigate relevant agent activity.
- Alerts and incident response procedures are tested.

## Conclusion

You have examined Cloud Agent workflows, repository permissions, issue assignment controls, firewall settings, MCP secrets, organizational policies, and audit logging.

These controls help organizations reduce the risks associated with cloud-based AI coding agents and maintain centralized security enforcement.

**Reference:** [GitHub Copilot Cloud Agent Risks and Mitigations](https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/risks-and-mitigations) | [VS Code Enterprise Policies](https://code.visualstudio.com/docs/enterprise/policies) | [Common Copilot Misconfigurations](https://aisecuritylabs.org/resources/copilot-misconfigurations/)