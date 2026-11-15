# Lab 02: Developer-Level GitHub Copilot Security Assessment

**Type:** Hands-on

**Level:** Beginner–Intermediate

**Duration:** 60 minutes

## **1. Objective**

Conduct a developer-level security assessment of GitHub Copilot environments. Identify configuration weaknesses, collect supporting evidence, and recommend remediation measures.

## **2. Assessment Tasks**

### **Task 1: Run the Copilot Security Audit**

1. Run the [Copilot Security Audit](https://aisecuritylabs.org/resources/copilot-audit/?utm_source=chatgpt.com) container.
2. Assess the local VS Code and Copilot CLI configurations.
3. Review detected MCP servers and the selected project.
4. Save the generated HTML report.

The audit is offline and read-only.

### **Task 2: Review the Security Checklist**

Use the [Copilot Security Checklist](https://aisecuritylabs.org/resources/copilot-checklist/?utm_source=chatgpt.com) to assess configurations that the automated audit cannot fully inspect.

Review:

- Copilot seat and account settings.
- Organization-level policies.
- Cloud Agent configuration.
- Developer security practices.

### **Task 3: Examine Developer Environments**

| Area | What to Assess |
| --- | --- |
| IDE | VS Code, Visual Studio, installation, and versions. |
| Identity | Account and Copilot seat configuration. |
| Permissions | Approval settings and automatic approvals. |
| Workspace | Workspace Trust and project-level settings. |
| Sandbox | Agent sandbox and network restrictions. |
| MCP | Configured MCP servers and their permissions. |
| Extensions | Installed extensions and their trustworthiness. |
| Repository | Secrets, instruction files, and repository security controls. |
| CLI | Copilot CLI permissions and bypass configurations. |

### **Task 4: Compare and Prioritize Findings**

1. Compare audit findings with the [Common Copilot Misconfigurations](https://aisecuritylabs.org/resources/copilot-misconfigurations/?utm_source=chatgpt.com).
2. Identify the corresponding misconfiguration IDs.
3. Prioritize Critical findings before lower-severity issues.
4. Record recommended remediation measures.

### **Task 5: Collect Assessment Evidence**

Maintain the following evidence:

- Copilot Security Audit HTML report.
- Completed security checklist.
- Configuration screenshots or files.
- Identified misconfiguration IDs.
- Recommended remediation actions.

## **3. Assessment Checklist**

- [ ]  Run the Copilot Security Audit.
- [ ]  Save the HTML report.
- [ ]  Complete the manual security checklist.
- [ ]  Review developer and project configurations.
- [ ]  Identify security exposures.
- [ ]  Prioritize Critical findings.
- [ ]  Document evidence and remediation recommendations.