# DevOps Academy - Starter Repository

Welcome to **DevOps Academy**. This is the starter repository for the DevOps bootcamp focused on Salesforce.

## ?? Prerequisites

Before you start, make sure you have installed:

- **Git** - Version control
  - Verify: `git --version`
  - Install from: https://git-scm.com/

- **Visual Studio Code** - Code editor
  - Download from: https://code.visualstudio.com/

- **Salesforce CLI (SFDX)**
  - Verify: `sfdx --version`
  - Install from: https://developer.salesforce.com/tools/sfdxcli

- **Salesforce Extension Pack** - VS Code extension
  - Open VS Code ? Extensions ? Search "Salesforce Extension Pack" ? Install

- **Salesforce Dev Sandbox Access** - Your test organization

## ?? Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/darktanuz-collab/academia-devops-starter.git
cd academia-devops-starter
```

### 2. Verify Structure

```bash
ls -la
# You should see: force-app/, docs/, README.md, sfdx-project.json
```

### 3. Authenticate with Salesforce

```bash
sfdx auth:web:login --alias my-sandbox --instanceurl https://[your-sandbox].salesforce.com
```

Replace `[your-sandbox]` with your sandbox URL (e.g., `testorg-dev.salesforce.com`)

### 4. Open in VS Code

```bash
code .
```

---

## ?? Labs

This repository contains 5 practical labs to learn DevOps with Salesforce:

| Lab | Topic | Duration | Description |
|-----|-------|----------|-------------|
| **Lab 1** | Git Basics | 20 min | Clone repo, create branch, make commits |
| **Lab 2** | Move Changes (SFDX) | 20 min | Connect to Salesforce, make changes, deploy |
| **Lab 3** | Multiple Environments | 15 min | Validate changes in Dev and QA |
| **Lab 4** | Pull Request Workflow | 20 min | Code review, approval, merge |
| **Lab 5** | Release Simulation | 15 min | Tagging, versioning, rollback |

**See details:** [docs/LABS.md](docs/LABS.md)

---

## ?? Branch Strategy

This repository uses **Git Flow**:

```
main (production)
  ?
  +-- release/1.0 (release branch)
       ?
       +-- develop (pre-production)
            ?
            +-- feature/your-change-1
            +-- feature/your-change-2
            +-- feature/your-change-3
```

**Rules:**
- **NEVER** commit directly to `main` or `develop`
- Always create a `feature/your-name` branch from `develop`
- Make changes in your branch
- Open a Pull Request (PR)
- Wait for approval
- Merge when approved

---

## ?? How to Contribute

### Step 1: Create Your Branch

```bash
git checkout develop
git pull origin develop
git checkout -b feature/your-name
```

### Step 2: Make Changes

Edit files in `force-app/` or `docs/`

```bash
# Example: Create Apex Class
sfdx force:apex:class:create --classname MyClass --outputdir force-app/main/default/classes
```

### Step 3: Commit Your Changes

```bash
git add .
git commit -m "feat: description of your change"
# Example: "feat: add HelloWorld Apex class"
```

### Step 4: Push to GitHub

```bash
git push --set-upstream origin feature/your-name
```

### Step 5: Open a Pull Request

1. Go to https://github.com/darktanuz-collab/academia-devops-starter
2. Click "Compare & Pull Request"
3. Write a clear description of what you did and why
4. Click "Create Pull Request"
5. **Wait for approval**

### Step 6: Merge (once approved)

```bash
git checkout develop
git pull origin develop
git merge feature/your-name
git push origin develop
```

---

## ?? Protected Branches

The `main` and `develop` branches are protected:

- ? Only mergeable via Pull Request
- ? Require approval from instructor
- ? Branches auto-delete after merge

---

## ?? Repository Structure

```
academia-devops-starter/
+-- force-app/                    # Salesforce code
¦   +-- main/
¦       +-- default/
¦           +-- classes/          # Apex Classes (create yours here)
¦           +-- triggers/         # Apex Triggers
¦           +-- objects/          # Custom Objects
+-- docs/                         # Documentation
¦   +-- LABS.md                   # Detailed guide for 5 labs
¦   +-- participants.md           # Track your progress here
+-- .gitignore                    # Files Git ignores
+-- sfdx-project.json             # SFDX configuration
+-- README.md                     # This file
```

---

## ?? Troubleshooting

### Error: "sfdx: command not found"

Salesforce CLI is not in your PATH. Reinstall from:
https://developer.salesforce.com/tools/sfdxcli

### Error: "No org configured"

You haven't authenticated your org. Run:

```bash
sfdx auth:web:login --alias my-sandbox --instanceurl https://[your-sandbox].salesforce.com
```

### Error: "Permission denied" on Git

Configure your Git credentials:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Error: "Merge conflict"

If two branches modify the same file:

```bash
# See conflicts
git status

# Edit the file manually to resolve conflicts
# Then:
git add .
git commit -m "fix: resolve merge conflict"
git push
```

---

## ?? Contact

Questions? Open an **Issue** in this repository or contact the instructor.

---

## ? Good Luck

Remember:
- **Small commits** (small and frequent changes)
- **Clear commit messages** (describe WHAT and WHY)
- **Code review mindset** (write for others to understand)
- **Test before pushing** (validate locally first)

Welcome to DevOps Academy! ??
