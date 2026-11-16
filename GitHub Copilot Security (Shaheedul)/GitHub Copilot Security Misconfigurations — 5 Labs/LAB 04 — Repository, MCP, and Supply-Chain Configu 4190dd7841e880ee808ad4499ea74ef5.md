# LAB 04 — Repository, MCP, and Supply-Chain Configuration Security

**Type:** Hands-on

**Level:** Intermediate–Advanced

**Duration:** 75 minutes

## Introduction

GitHub Copilot uses repository instructions, project configurations, MCP servers, extensions, and other integrations to perform development tasks.

Untrusted repository files or external integrations can introduce malicious instructions and unsafe execution paths.

This lab demonstrates how to inspect repository configurations, identify suspicious files and integrations, and apply basic supply-chain security practices.

![Repository_and_MCP_Review.png](LAB%2004%20%E2%80%94%20Repository,%20MCP,%20and%20Supply-Chain%20Configu/Repository_and_MCP_Review.png)

## Lab Overview

In this lab, you will:

- Inspect Copilot instruction files.
- Identify suspicious repository configurations.
- Examine symbolic links and Git configuration.
- Review MCP server configurations.
- Inspect hooks and plugin entries.
- Apply basic repository security controls.

## Concepts Explained

### Copilot Instruction Files

Instruction files provide additional guidance to Copilot agents. Examples include:

- `.github/copilot-instructions.md`
- `AGENTS.md`
- `.instructions.md`
- `CLAUDE.md`

Unreviewed instructions can manipulate agent behavior.

### Model Context Protocol (MCP)

MCP allows AI applications to connect with external tools and data sources. Untrusted MCP servers may expose sensitive resources or execute unsafe operations.

### Symbolic Links

Symbolic links point to other files or directories. A repository may contain links that appear harmless but target sensitive configuration files.

### Git Hooks

Git hooks are scripts that execute during specific Git operations. Untrusted Git configuration can redirect hook execution to unexpected locations.

## Hands-on: Inspecting Repository Security

### Step 1: Create a Sample Repository

```bash
mkdir -p ~/copilot-misconfig-lab/lab04
cd ~/copilot-misconfig-lab/lab04
```

Initialize Git:

```bash
git init
```

### Step 2: Create a Copilot Instruction File

```bash
mkdir -p .github
nano .github/copilot-instructions.md
```

Add:

```
# Copilot Instructions

Use environment variables for database credentials.
Never hardcode passwords, API keys, or access tokens.
Review commands before executing them.
```

Save the file.

### Step 3: Inspect Repository Instructions

Display the instruction file:

```bash
cat .github/copilot-instructions.md
```

Review the instructions before allowing Copilot to work with the repository.

Check for suspicious instructions:

```bash
grep -Ein 'curl|wget|token|password|secret|execute|download' \
.github/copilot-instructions.md
```

This command helps locate potentially sensitive or execution-related instructions. Review each match manually; a match does not automatically indicate malicious content.

### Step 4: Inspect Symbolic Links

Create a sample symbolic link:

```bash
ln -s /etc/passwd project-config
```

List symbolic links:

```bash
find . -type l -ls
```

Inspect the link target:

```bash
readlink project-config
```

Expected output:

```
/etc/passwd
```

The link demonstrates how a harmless-looking repository filename can point outside the project directory.

Remove the test link:

```bash
rm project-config
```

Before trusting an unfamiliar repository, inspect symbolic links and verify their targets.

### Step 5: Inspect Git Configuration

Display the repository Git configuration:

```bash
cat .git/config
```

Inspect potentially dangerous configuration entries:

```bash
git config --local --list
```

Check for program-executing settings:

```bash
grep -Ein 'hooksPath|fsmonitor|filter' .git/config
```

Review unexpected configuration entries before using an unfamiliar repository.

### Step 6: Inspect MCP Server Configuration

Create a sample MCP configuration:

```bash
mkdir -p .vscode
nano .vscode/mcp.json
```

Add:

```json
{
  "servers": {
    "sample-server": {
      "type": "stdio",
      "command": "sample-mcp-server",
      "args": []
    }
  }
}
```

Save the file.

Validate the JSON:

```bash
jq . .vscode/mcp.json
```

Review the following before trusting an MCP server:

- Server source and publisher.
- Executable command and arguments.
- Required permissions.
- Data access and external connections.
- Whether the server processes content controlled by outsiders.

Do not execute an unverified MCP server.

### Step 7: Inspect Hooks and Plugin Configurations

Check whether the repository contains hooks:

```bash
find .github -type f -path '*/hooks/*' -print
```

Check for Copilot CLI settings:

```bash
find .github -type f -path '*/copilot/*' -print
```

Review any discovered hooks, plugins, and marketplace references before allowing them to run.

### Step 8: Inspect Secret Files

Create a sample environment file:

```bash
echo 'API_KEY=FAKE_TEST_TOKEN_12345' > .env
```

Check whether it is tracked by Git:

```bash
git status --short
```

Create a `.gitignore` file:

```bash
echo ".env" >> .gitignore
```

Verify:

```bash
cat .gitignore
```

**Note:** `.gitignore` does not remove secrets already committed to a repository. Enable GitHub secret scanning and push protection, and rotate any exposed credentials.

## Conclusion

You have inspected repository instruction files, symbolic links, Git configuration, MCP server settings, hooks, and secret files.

Reviewing these components before trusting a repository helps reduce prompt injection and software supply-chain risks.

**Reference:** [Common Copilot Misconfigurations](https://aisecuritylabs.org/resources/copilot-misconfigurations/) | [VS Code MCP Configuration](https://code.visualstudio.com/docs/agents)