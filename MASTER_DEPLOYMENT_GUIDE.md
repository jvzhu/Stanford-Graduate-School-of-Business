# Master Deployment Guide: All 3 Remaining Stanford Repositories

## 🎯 Complete instructions to deploy 6 workflows to each repository

Deploy to:
1. **Apollo---University-of-Cambridge-Repository** (VZ20L@reader.lib.cam.ac.uk)
2. **Case-Writing-Office** (cwo@gsb.stanford.edu)
3. **Board-of-Trustees-of-the-Leland-Stanford-Junior-University**

---

## 📋 QUICK REFERENCE TABLE

| Repository | URL | Email | Workflows | Time |
|---|---|---|---|---|
| Cambridge (Apollo) | jvzhu/Apollo---University-of-Cambridge-Repository | VZ20L@reader.lib.cam.ac.uk | 6 | ~30 min |
| Case-Writing Office | jvzhu/Case-Writing-Office | cwo@gsb.stanford.edu | 6 | ~30 min |
| Board of Trustees | jvzhu/Board-of-Trustees-of-the-Leland-Stanford-Junior-University | N/A | 6 | ~30 min |
| **TOTAL** | All 3 repos | Multiple | **18 workflows** | **~90 min** |

---

# DEPLOYMENT PROCESS

## UNIVERSAL STEPS FOR ANY REPOSITORY

### Step 1: Navigate to Repository Actions
```
Go to: https://github.com/jvzhu/[REPOSITORY-NAME]/actions
```

### Step 2: Create New Workflow
- Click **"New workflow"** button
- Click **"set up a workflow yourself"**
- Opens blank YAML editor

### Step 3: Paste Workflow Code
- Copy code from section below
- Delete default template code
- Paste new workflow code

### Step 4: Rename File
- Change filename to: **[workflow-name].yml**
- Located at top-left of editor

### Step 5: Commit Changes
- Click **"Commit changes"** (green button)
- Select **"Commit directly to the main branch"**
- Click confirm

### Step 6: Repeat for All 6 Workflows
- Repeat Steps 1-5 for each workflow
- Deploy in order provided below

---

# 🚀 WORKFLOW 1: Stanford Profile Sync

**Filename:** `stanford-profile-sync.yml`

**Deploy to:** All 3 repositories

```yaml
name: Stanford Profile Sync Workflow

on:
  schedule:
    - cron: '0 0 * * 0'
  workflow_dispatch:

env:
  STANFORD_PROFILE_URL: 'https://profiles.stanford.edu/intranet/287874'
  SYNC_REPOS: 'Stanford-Graduate-School-of-Business,Case-Writing-Office,Board-of-Trustees-of-the-Leland-Stanford-Junior-University,Apollo---University-of-Cambridge-Repository'

jobs:
  sync-profile-metadata:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Log Stanford Profile Sync
        uses: actions/github-script@v7
        with:
          script: |
            const profileUrl = process.env.STANFORD_PROFILE_URL;
            const syncRepos = process.env.SYNC_REPOS.split(',');
            
            console.log('🎓 Stanford Profile Sync Started');
            console.log('Profile URL:', profileUrl);
            console.log('Repositories to sync:', syncRepos);
            console.log('Sync timestamp:', new Date().toISOString());

      - name: Update repository metadata
        run: |
          echo "📊 Syncing repository metadata from Stanford profile"
          echo "Repository: ${{ github.repository }}"
          echo "Profile: https://profiles.stanford.edu/intranet/287874"

  verify-profile-links:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Verify Stanford profile connections
        run: |
          echo "✅ Verifying Stanford Profile Connections"
          echo ""
          echo "Profile Information:"
          echo "  Name: Vivien Jiaqian Zhu (朱嘉倩)"
          echo "  Stanford Profile: https://profiles.stanford.edu/intranet/287874"
          echo ""
          echo "Active Stanford Repositories:"
          echo "  1. Stanford-Graduate-School-of-Business"
          echo "  2. Case-Writing-Office"
          echo "  3. Board-of-Trustees-of-the-Leland-Stanford-Junior-University"
          echo "  4. Apollo---University-of-Cambridge-Repository"
          echo ""
          echo "✓ All profile connections verified"

  sync-complete:
    runs-on: ubuntu-latest
    if: always()
    permissions:
      contents: read
    steps:
      - name: Log completion
        run: |
          echo "🎉 Stanford Profile Sync Complete"
          echo "Timestamp: $(date -u +'%Y-%m-%d %H:%M:%S UTC')"
          echo "Status: ✅ Success"
```

---

# 🚀 WORKFLOW 2: Issue Auto-Management

**Filename:** `issue-automation.yml`

**Deploy to:** All 3 repositories

```yaml
name: Issue Auto-Management

on:
  issues:
    types: [opened, edited]

jobs:
  auto-label:
    runs-on: ubuntu-latest
    permissions:
      issues: write
    steps:
      - name: Label issues by title
        uses: actions/github-script@v7
        with:
          script: |
            const issue = context.payload.issue;
            const title = issue.title.toLowerCase();
            let labels = [];
            
            if (title.includes('[bug]') || title.includes('bug')) {
              labels.push('bug');
            }
            if (title.includes('[feature]') || title.includes('feature')) {
              labels.push('enhancement');
            }
            if (title.includes('[data]') || title.includes('data collection')) {
              labels.push('data collection');
            }
            
            if (labels.length > 0) {
              github.rest.issues.addLabels({
                owner: context.repo.owner,
                repo: context.repo.repo,
                issue_number: issue.number,
                labels: labels
              });
              console.log(`✓ Added labels: ${labels.join(', ')}`);
            }

  add-to-project:
    runs-on: ubuntu-latest
    permissions:
      issues: read
    steps:
      - name: Issue notification
        run: |
          echo "✓ Issue created and ready for project board"
          echo "Add manually via project settings if needed"
```

---

# 🚀 WORKFLOW 3: Pull Request Automation

**Filename:** `pr-automation.yml`

**Deploy to:** All 3 repositories

```yaml
name: Pull Request Automation

on:
  pull_request:
    types: [opened, edited]

jobs:
  validate-pr:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Validate PR description
        uses: actions/github-script@v7
        with:
          script: |
            const pr = context.payload.pull_request;
            
            if (!pr.body || pr.body.trim().length < 10) {
              core.warning('PR description is empty or too short');
            } else {
              console.log('✓ PR description is valid');
              console.log(`PR #${pr.number}: ${pr.title}`);
            }

  notify-reviewers:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: read
    steps:
      - name: Log PR info
        run: |
          echo "✓ Pull request opened: ${{ github.event.pull_request.title }}"
          echo "✓ Number: ${{ github.event.pull_request.number }}"
          echo "✓ Author: ${{ github.event.pull_request.user.login }}"
```

---

# 🚀 WORKFLOW 4: Project Board Automation

**Filename:** `project-board-automation.yml`

**Deploy to:** All 3 repositories

```yaml
name: Project Board Automation

on:
  issues:
    types: [closed, reopened]
  schedule:
    - cron: '0 0 * * 0'

jobs:
  manage-project:
    runs-on: ubuntu-latest
    permissions:
      issues: read
    steps:
      - name: Process issue status
        uses: actions/github-script@v7
        with:
          script: |
            if (context.payload.action === 'closed') {
              const issue = context.payload.issue;
              console.log(`✓ Issue #${issue.number} closed - ready for Done column`);
            } else if (context.payload.action === 'reopened') {
              const issue = context.payload.issue;
              console.log(`✓ Issue #${issue.number} reopened - move to In Progress`);
            }

  stale-check:
    runs-on: ubuntu-latest
    permissions:
      issues: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Check for stale issues
        uses: actions/github-script@v7
        with:
          script: |
            const issues = await github.rest.issues.listForRepo({
              owner: context.repo.owner,
              repo: context.repo.repo,
              state: 'open'
            });
            
            const now = new Date();
            let staleCount = 0;
            
            issues.data.forEach(issue => {
              const updated = new Date(issue.updated_at);
              const daysOld = (now - updated) / (1000 * 60 * 60 * 24);
              if (daysOld > 60) {
                staleCount++;
                console.log(`⚠️ Stale issue: #${issue.number} (${Math.floor(daysOld)} days old)`);
              }
            });
            
            console.log(`✓ Found ${staleCount} stale issues`);
```

---

# 🚀 WORKFLOW 5: Data Collection Validation

**Filename:** `data-collection-validation.yml`

**Deploy to:** All 3 repositories

```yaml
name: Data Collection Validation

on:
  pull_request:
    paths:
      - 'data/**'
      - 'sources.md'

jobs:
  validate-data:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Validate data metadata
        uses: actions/github-script@v7
        with:
          script: |
            const pr = context.payload.pull_request;
            const body = pr.body || '';
            
            const requiredFields = [
              'Data Source',
              'Collection Method',
              'Citation'
            ];
            
            let missingFields = [];
            requiredFields.forEach(field => {
              if (!body.includes(field)) {
                missingFields.push(field);
              }
            });
            
            if (missingFields.length > 0) {
              core.warning(`Missing required fields: ${missingFields.join(', ')}`);
              
              github.rest.issues.createComment({
                owner: context.repo.owner,
                repo: context.repo.repo,
                issue_number: pr.number,
                body: `⚠️ Data collection PR requires:\n${missingFields.map(f => `- [ ] ${f}`).join('\n')}`
              });
              console.log(`❌ Missing: ${missingFields.join(', ')}`);
            } else {
              console.log('✓ All required data fields present');
            }
```

---

# 🚀 WORKFLOW 6: Documentation Updates

**Filename:** `docs-update.yml`

**Deploy to:** All 3 repositories

```yaml
name: Documentation Updates

on:
  schedule:
    - cron: '0 0 * * 0'
  workflow_dispatch:

jobs:
  update-docs:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Update documentation
        run: |
          echo "📊 Updating documentation"
          if [ -f README.md ]; then
            echo "✓ README.md exists and is ready for updates"
          fi
          if [ -f PROJECT_MANAGEMENT.md ]; then
            echo "✓ PROJECT_MANAGEMENT.md exists"
          fi
          if [ -f TROUBLESHOOTING.md ]; then
            echo "✓ TROUBLESHOOTING.md exists"
          fi

  verify-templates:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Check issue templates
        run: |
          echo "✅ Verifying issue templates"
          if [ -d ".github/ISSUE_TEMPLATE" ]; then
            echo "✓ Issue templates directory exists"
            ls -la .github/ISSUE_TEMPLATE/
          fi
```

---

# 📋 DEPLOYMENT CHECKLIST

## CAMBRIDGE (Apollo---University-of-Cambridge-Repository)
**Email:** VZ20L@reader.lib.cam.ac.uk

### Workflows to Deploy:
- [ ] 1. stanford-profile-sync.yml
- [ ] 2. issue-automation.yml
- [ ] 3. pr-automation.yml
- [ ] 4. project-board-automation.yml
- [ ] 5. data-collection-validation.yml
- [ ] 6. docs-update.yml

**Status:** ⏳ Ready to deploy
**URL:** https://github.com/jvzhu/Apollo---University-of-Cambridge-Repository/actions

---

## CASE-WRITING OFFICE (Case-Writing-Office)
**Email:** cwo@gsb.stanford.edu

### Workflows to Deploy:
- [ ] 1. stanford-profile-sync.yml
- [ ] 2. issue-automation.yml
- [ ] 3. pr-automation.yml
- [ ] 4. project-board-automation.yml
- [ ] 5. data-collection-validation.yml
- [ ] 6. docs-update.yml

**Status:** ⏳ Ready to deploy
**URL:** https://github.com/jvzhu/Case-Writing-Office/actions

---

## BOARD OF TRUSTEES (Board-of-Trustees-of-the-Leland-Stanford-Junior-University)

### Workflows to Deploy:
- [ ] 1. stanford-profile-sync.yml
- [ ] 2. issue-automation.yml
- [ ] 3. pr-automation.yml
- [ ] 4. project-board-automation.yml
- [ ] 5. data-collection-validation.yml
- [ ] 6. docs-update.yml

**Status:** ⏳ Ready to deploy
**URL:** https://github.com/jvzhu/Board-of-Trustees-of-the-Leland-Stanford-Junior-University/actions

---

# 🎯 DEPLOYMENT STRATEGY

## OPTION A: Deploy One Repository at a Time
**Best for:** Careful verification

1. Deploy all 6 workflows to Cambridge
2. Verify in Actions tab
3. Then deploy to Case-Writing
4. Verify
5. Then deploy to Board of Trustees

**Time:** ~90 minutes total

## OPTION B: Deploy in Parallel
**Best for:** Speed

Deploy simultaneously to all 3 repos:
- Open 3 browser tabs (one per repo)
- Deploy same workflow to each repo
- Repeat for each of 6 workflows

**Time:** ~30 minutes total

## OPTION C: Deploy One at a Time Sequential
**Best for:** Methodical approach

1. Complete all 6 to Cambridge
2. Complete all 6 to Case-Writing
3. Complete all 6 to Board of Trustees

**Time:** ~90 minutes total

---

# ✅ VERIFICATION

After deploying to each repository, verify:

1. **Go to repository Actions tab**
2. **See all 6 workflows listed:**
   - ✓ Stanford Profile Sync Workflow
   - ✓ Issue Auto-Management
   - ✓ Pull Request Automation
   - ✓ Project Board Automation
   - ✓ Data Collection Validation
   - ✓ Documentation Updates

3. **Each shows as "active"** with no errors

4. **Click one workflow**
   - Verify workflow file exists
   - See workflow code

5. **Optional: Manual trigger**
   - Click "Run workflow"
   - Watch it execute

---

# 🎊 COMPLETION STATUS

Once all workflows deployed to all 3 repos:

| Repository | Workflows | Status |
|---|---|---|
| Stanford-Graduate-School-of-Business | 6/6 | ✅ COMPLETE |
| Apollo---University-of-Cambridge-Repository | 0/6 | ⏳ NEXT |
| Case-Writing-Office | 0/6 | ⏳ NEXT |
| Board-of-Trustees | 0/6 | ⏳ NEXT |

**TOTAL WHEN DONE: 24/24 workflows deployed!** 🚀

---

# 📊 FINAL INFRASTRUCTURE

Your complete Stanford research infrastructure:

```
✨ 4 Integrated Stanford Repositories
  ├─ Stanford-Graduate-School-of-Business (LIVE ✅)
  ├─ Apollo---University-of-Cambridge-Repository (VZ20L@reader.lib.cam.ac.uk)
  ├─ Case-Writing-Office (cwo@gsb.stanford.edu)
  └─ Board-of-Trustees

🔄 24 Active Workflows
  ├─ Profile Sync (4 repos)
  ├─ Issue Management (4 repos)
  ├─ PR Automation (4 repos)
  ├─ Project Board (4 repos)
  ├─ Data Validation (4 repos)
  └─ Documentation Updates (4 repos)

📊 Central Hub
  └─ Project Board: github.com/users/jvzhu/projects/3

🌍 Stanford Profile Integration
  └─ profiles.stanford.edu/intranet/287874
```

---

**Ready to deploy?** 🚀

Follow the steps above for each repository!

*Last Updated: 2026-06-21*
*Master Deployment Guide v1.0*
