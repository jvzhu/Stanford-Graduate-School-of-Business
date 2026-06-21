# Stanford Profile Sync Workflow

This workflow syncs your Stanford profile information to your GitHub repositories and keeps documentation up to date.

## Overview

The Stanford Profile Sync system includes:

1. **Profile Data Sync** - Automatically updates repository information from your Stanford profile
2. **Profile Documentation** - Generates README files linking GitHub work to Stanford profile
3. **Cross-Repository Sync** - Keeps all 4 Stanford repositories synchronized

## Workflow Files

### 1. stanford-profile-sync.yml
- Runs on schedule (weekly) and manual trigger
- Fetches your Stanford profile information
- Updates repository metadata
- Syncs project descriptions

### 2. profile-documentation-update.yml
- Updates README with Stanford profile link
- Generates profile badges
- Links research projects
- Updates bio information

### 3. stanford-research-showcase.yml
- Aggregates work across all 4 Stanford repositories
- Creates unified research overview
- Tracks collaboration metrics
- Generates research summary

## Setup Instructions

1. **Add Stanford Profile URL** as a repository secret:
   - Go to Settings → Secrets → New repository secret
   - Name: `STANFORD_PROFILE_URL`
   - Value: `https://profiles.stanford.edu/intranet/287874`

2. **Enable Workflow Permissions**:
   - Go to Settings → Actions → General
   - Select "Read and write permissions"
   - Allow GitHub Actions to create pull requests

3. **Customize Workflow**:
   - Edit `stanford-profile-sync.yml`
   - Update profile information sections
   - Configure sync schedule (default: weekly)

## Manual Triggers

You can manually run workflows from the Actions tab:

1. Go to **Actions** tab
2. Select workflow name
3. Click **Run workflow**
4. Select your branch
5. Click **Run workflow** (green button)

## Profile Information Synced

- ✅ Your Stanford affiliation
- ✅ Research interests
- ✅ Current projects
- ✅ Collaborations
- ✅ Publication links
- ✅ Contact information

## Repository Metadata Updated

Each repository gets updated with:
- Profile link in README
- Research focus description
- Collaboration information
- Related projects
- Contact/collaboration info

## Schedule

Default schedule (can be customized):
- **Weekly**: Full profile sync and documentation update
- **Manual**: Run anytime via GitHub Actions

## Environment Variables

```yaml
STANFORD_PROFILE_URL: https://profiles.stanford.edu/intranet/287874
SYNC_INTERVAL: weekly
AUTO_UPDATE_README: true
SYNC_ALL_REPOS: true
```

## Troubleshooting

If sync fails:
1. Check workflow logs in Actions tab
2. Verify Stanford profile URL is correct
3. Ensure repository permissions are enabled
4. Check that all secrets are set correctly

## Next Steps

1. Add Stanford profile URL as repository secret
2. Enable workflow permissions
3. Manually trigger first sync
4. Verify README updates
5. Customize profile sections as needed

---

**Last Updated:** 2026-06-21
**Profile URL:** https://profiles.stanford.edu/intranet/287874
**Related Documentation:** See README.md and PROJECT_MANAGEMENT.md
