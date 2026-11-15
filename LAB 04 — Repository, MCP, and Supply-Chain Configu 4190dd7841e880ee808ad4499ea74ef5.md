# LAB 04 — Repository, MCP, and Supply-Chain Configuration Security

**Type:** Hands-on

**Level:** Intermediate–Advanced

**Duration:** 75 Minutes

## **1. Objective**

Identify and secure repository-level configurations, instruction files, external integrations, and supply-chain components that may introduce security risks to GitHub Copilot.

## **2. Required Environment**

- Visual Studio Code.
- Git and GitHub.
- A test repository.
- An MCP configuration or test MCP server.
- Basic terminal knowledge.

## **3. Misconfigurations Covered**

| ID | Misconfiguration | Security Risk |
| --- | --- | --- |
| X8 | Untrusted MCP servers | Malicious external tool interactions. |
| X9 | Unreviewed instruction files | Hidden or malicious agent instructions. |
| X13 | Malicious symbolic links | Unauthorized access or modification of target files. |
| X14 | Exposed repository secrets | Credential disclosure. |
| X15 | Unreviewed hooks and plugins | Execution of untrusted code. |
| X16 | Untrusted `.git/config` files | Unexpected program execution through Git configurations. |

## **4. Practical Activities**

### **Task 1: Review Repository Instruction Files**

1. Open a test repository.
2. Locate the following files, if present:
    - `copilot-instructions.md`
    - `AGENTS.md`
    - `.instructions.md`
    - `CLAUDE.md`
3. Review their contents.
4. Look for suspicious instructions and hidden Unicode characters.
5. Identify files that require additional review protection.

**Expected Result:** Untrusted or suspicious instructions should be identified before the repository is trusted.

### **Task 2: Review Symbolic Links and Git Configuration**

1. Inspect the repository for symbolic links.
2. Identify their actual targets.
3. Inspect the `.git/config` file.
4. Review potentially dangerous configuration entries.
5. Identify repositories that should be re-cloned from trusted sources.

**Expected Result:** Suspicious symbolic links and untrusted Git configurations should be identified.

### **Task 3: Secure Repository Secrets**

1. Inspect the test repository for exposed credentials.
2. Identify sensitive files such as `.env`.
3. Review `.gitignore`.
4. Enable GitHub secret scanning where available.
5. Enable push protection.

**Expected Result:** Sensitive credentials should not be committed or exposed through the repository.

### **Task 4: Review MCP Server Configurations**

1. Locate the MCP configuration.
2. Identify configured MCP servers.
3. Review their sources and permissions.
4. Identify unnecessary tools and excessive access.
5. Retain only approved and necessary integrations.

**Expected Result:** Only trusted and necessary MCP servers should be configured.

### **Task 5: Review Hooks and Plugins**

1. Inspect repository hook configurations.
2. Review `.github/hooks/`, where present.
3. Inspect plugin configurations and marketplace sources.
4. Identify untrusted scripts or installation sources.
5. Remove unnecessary or unverified integrations.

**Expected Result:** Repository hooks and plugins should be reviewed before execution or installation.

## **5. Security Checklist**

- [ ]  Repository instruction files are reviewed.
- [ ]  Hidden Unicode characters are checked.
- [ ]  Symbolic links and targets are inspected.
- [ ]  `.git/config` is reviewed.
- [ ]  Repository secrets are protected.
- [ ]  Secret scanning and push protection are enabled where available.
- [ ]  MCP servers are approved and restricted.
- [ ]  Hooks and plugins are reviewed.