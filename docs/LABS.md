# Academia DevOps - Detailed Labs Guide

This is the step-by-step guide for the **5 practical labs** of the DevOps bootcamp.

---

## LAB 1: Git Basics (20 min)

Clone the repository, create a branch, and make your first commit.

### Steps

1. Clone: git clone https://github.com/darktanuz-collab/academia-devops-starter.git
2. Create branch: git checkout -b feature/your-name
3. Edit docs/participants.md and add your name
4. Commit: git add . && git commit -m 'feat: add my name - Lab 1'
5. View: git log --oneline

### Checkpoint: All steps completed? Lab 1 DONE!

---

## LAB 2: Move Changes in Salesforce (20 min)

Connect to Salesforce, create an Apex class, deploy via SFDX.

### Steps

1. Auth: sfdx auth:web:login --alias my-sandbox --instanceurl https://[YOUR].salesforce.com
2. Create Apex Class HelloWorld in VS Code
3. Deploy: sfdx force:source:push --targetusername my-sandbox
4. Commit: git add force-app/ && git commit -m 'feat: add HelloWorld class - Lab 2'

### Checkpoint: Apex class deployed? Lab 2 DONE!

---

## LAB 3: Multiple Environments (15 min)

Deploy to QA, simulate a bug, then revert it with Git.

### Steps

1. Connect to QA: sfdx auth:web:login --alias my-qa
2. Deploy to QA: sfdx force:source:push --targetusername my-qa
3. Simulate bug: Edit HelloWorld, change return value
4. Revert: git checkout HEAD~1 -- force-app/
5. Deploy reverted: sfdx force:source:push --targetusername my-sandbox
6. Commit: git add . && git commit -m 'revert: remove bug - Lab 3'

### Checkpoint: Bug reverted with Git? Lab 3 DONE!

---

## LAB 4: Pull Request Workflow (20 min)

Push to GitHub, create a PR, get approval, merge.

### Steps

1. Push: git push --set-upstream origin feature/your-name
2. Go to GitHub, click 'Compare & Pull Request'
3. Write description and create PR
4. Get instructor approval
5. Merge the PR
6. Sync: git checkout develop && git pull origin develop

### Checkpoint: Code merged to develop? Lab 4 DONE!

---

## LAB 5: Release Simulation (15 min)

Create a release tag, simulate a rollback.

### Steps

1. Create release branch: git checkout -b release/1.0 develop
2. Tag release: git tag -a v1.0 -m 'Release 1.0: First DevOps training release'
3. Push: git push origin release/1.0 && git push origin v1.0
4. Verify on GitHub Releases tab
5. Simulate rollback: git checkout v1.0 -- force-app/
6. Deploy old version: sfdx force:source:push --targetusername my-sandbox
7. Return to develop: git checkout develop && git pull origin develop

### Checkpoint: Release tagged and rollback simulated? Lab 5 DONE!

---

## You Completed Academia DevOps!

✓ Git fundamentals
✓ Move changes with SFDX
✓ Multi-environment strategy
✓ Pull Request workflow
✓ Release management

🚀 Good luck!
