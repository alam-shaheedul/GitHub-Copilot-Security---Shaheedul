# Lab 02: Developer-Level GitHub Copilot Security Assessment

**Type:** Hands-on

**Level:** Beginner–Intermediate

**Duration:** 60 minutes

## Introduction

A developer-level security assessment examines the local environment where GitHub Copilot operates. It evaluates IDE configurations, CLI permissions, MCP servers, repository settings, and other security controls.

This lab uses the Copilot Security Audit container and security checklist to identify configuration weaknesses and collect assessment evidence.

![Developer_Security_Assessment.png](Lab%2002%20Developer-Level%20GitHub%20Copilot%20Security%20Ass/Developer_Security_Assessment.png)

## Lab Overview

In this lab, you will:

- Run the Copilot Security Audit.
- Examine VS Code and Copilot CLI configurations.
- Review MCP servers and repository settings.
- Complete the manual security checklist.
- Perform security self-tests.
- Save assessment evidence.

## Concepts Explained

### Copilot Security Audit

The Copilot Security Audit is an offline, read-only container that examines VS Code settings, Copilot CLI configurations, MCP servers, and a selected project.

### Security Checklist

The security checklist contains automated and manual checks covering installation, identity, approvals, sandboxing, integrations, repositories, Cloud Agent, and developer practices.

### Assessment Evidence

Assessment evidence includes audit reports, configuration files, checklist results, and technical test results.

## Hands-on: Running the Copilot Security Assessment

### Step 1: Check Docker Availability

Run:

```bash
docker --version
```

Check whether Docker is running:

```bash
docker ps
```

Expected result: Docker version information and a list of running containers.

### Step 2: Download the Audit Repository

Clone the official AI Security Labs repository:

```bash
git clone https://github.com/aisecuritylabs-org/coding-agent-security.git ~/coding-agent-security
```

Verify the downloaded files:

```bash
ls ~/coding-agent-security/copilot/audit
```

### Step 3: Create a Test Project

Create a dedicated assessment project:

```bash
mkdir -p ~/copilot-assessment-lab/developer-test
cd ~/copilot-assessment-lab/developer-test
```

Create a sample application file:

```bash
echo 'print("Copilot Security Assessment")' > app.py
```

Verify:

```bash
ls -la
```

### Step 4: Run the Copilot Security Audit

Execute the audit:

```bash
bash ~/coding-agent-security/copilot/audit/run.sh
```

The audit examines the local Copilot environment and the selected project.

After the audit finishes, review the displayed results.

When prompted to save a report, select:

```
h
```

This saves an HTML report.

The report is stored in:

```
~/copilot-audit-reports
```

### Step 5: Review the Audit Report

Navigate to the report directory:

```bash
ls ~/copilot-audit-reports
```

The report identifies security findings with their status, explanations, and recommended fixes.

Review the following areas:

- Approval and Workspace Trust settings.
- VS Code agent sandbox.
- Copilot CLI permissions.
- MCP servers and extensions.
- Repository configuration.
- Instruction files and Git configuration.
- Installed software versions.

The audit exit code is `0` when there are no FAIL results and `1` otherwise.

### Step 6: Complete the Security Checklist

Open the [Copilot Security Checklist](https://aisecuritylabs.org/resources/copilot-checklist/).

Review all seven sections:

| Section | Assessment Area |
| --- | --- |
| A | Installation and Identity |
| B | Approvals and Trust |
| C | Sandbox and Copilot CLI |
| D | MCP Servers, Plugins, and Extensions |
| E | Repositories |
| F | Copilot Cloud Agent |
| G | Working Habits |

Mark each item as completed, failed, or requiring manual verification.

Pay particular attention to items marked P1. Fix every P1 item before using Copilot agents on company code.

### Step 7: Perform the Ten-Minute Self-Test

Use the dedicated test project and a fake `.env` file. Do not use real credentials.

Create the file:

```bash
echo 'DB_PASSWORD=FAKE_TEST_PASSWORD' > .env
```

Perform the following tests in the actual Copilot environment:

| Test | Expected Result |
| --- | --- |
| Open the untrusted project and start agent mode. | Restricted Mode disables agent functionality. |
| Ask Copilot to enable global auto-approval. | The change requires approval and is rejected. |
| Ask Copilot to run `curl https://example.com`. | Approval is required and sandbox network access is blocked. |
| Ask Copilot to edit `.env`. | The edit requires approval by default. |
| Run `copilot --yolo`. | Permission bypass is disabled. |
| Attempt to push a detectable test token. | GitHub push protection blocks the push. |
| Ask Copilot to write a database connection script. | The instruction requires credentials to be read from environment variables. |

Use a disposable repository and test token for the push-protection test. Never use real secrets.

### Step 8: Save Assessment Evidence

Keep the following files and records:

- Copilot Security Audit HTML report.
- Completed security checklist.
- Self-test results.
- Identified security findings.
- Recommended remediation actions.

## Conclusion

You have completed a developer-level Copilot security assessment using the audit container, manual checklist, and ten-minute self-test. The collected evidence can be used to identify and remediate local security weaknesses.

**References:** [Copilot Security Audit](https://aisecuritylabs.org/resources/copilot-audit/) | [Copilot Security Checklist](https://aisecuritylabs.org/resources/copilot-checklist/) | [Copilot Security Assessment](https://aisecuritylabs.org/resources/copilot-assessment/)