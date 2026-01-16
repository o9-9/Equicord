# GitHub Actions Workflows Guide

This repository uses GitHub Actions to automate testing and building of Equicord.

## Available Workflows

### 1. 🧪 Test Workflow (`test.yml`)
**Triggers:** 
- Push to `main` or `dev` branches
- Pull requests to `main` or `dev` branches

**What it does:**
- Lints the code
- Tests if desktop version compiles
- Tests if web version compiles  
- Validates plugin structure

**Status:** This runs automatically and helps ensure code quality.

---

### 2. 🔨 Build & Release Workflow (`build.yml`)
**Triggers:**
- Push to `main` branch
- Git tags starting with `v` (e.g., `v1.0.0`)
- Manual trigger from GitHub Actions tab

**What it does:**
1. Builds web and desktop versions
2. Generates plugin metadata files
3. Creates browser extensions
4. Uploads build artifacts
5. Creates/updates GitHub releases

**Outputs:**
- Desktop client files (`.asar`)
- Browser extensions (`.zip` for Chrome/Firefox)
- Userscript (`Equicord.user.js`)
- Plugin metadata (`.json` files)

---

## How Releases Work

### Automatic "Latest" Release
Every push to `main` will:
- Create/update a release tagged as "latest"
- Mark it as a pre-release (development build)
- Include all build artifacts

### Tagged Releases
When you create a git tag (e.g., `v1.0.0`):
```bash
git tag v1.0.0
git push origin v1.0.0
```
The workflow will:
- Create an official release with that version number
- Mark it as a stable release (not pre-release)
- Include all build artifacts

---

## Manual Triggering

You can manually trigger the build workflow:
1. Go to your repository on GitHub
2. Click "Actions" tab
3. Select "Build & Release" workflow
4. Click "Run workflow" button
5. Choose the branch and click "Run workflow"

---

## Build Artifacts

After each build, you can download artifacts from:
- **Releases page:** Permanent releases with all files
- **Actions tab:** Temporary artifacts (90 days) for each workflow run

---

## No Secrets Required

This workflow uses only the default `GITHUB_TOKEN` provided by GitHub Actions.  
No additional secrets or configuration needed! 🎉

---

## Customization

### Change When Builds Run
Edit the `on:` section in `.github/workflows/build.yml`:

```yaml
on:
    push:
        branches:
            - main
            - dev  # Add other branches
    workflow_dispatch:  # Keep for manual triggers
```

### Skip a Build
Add `[skip ci]` to your commit message:
```bash
git commit -m "Update README [skip ci]"
```

### Disable a Workflow
1. Go to Actions tab
2. Select the workflow
3. Click "⋯" (three dots)
4. Click "Disable workflow"

---

## Troubleshooting

### Build fails with "permission denied"
- Go to repo Settings → Actions → General
- Under "Workflow permissions", select "Read and write permissions"
- Click "Save"

### Release not created
- Check the Actions tab for error messages
- Ensure your repo has the "latest" release (will be auto-created on first run)

### Missing files in release
- Check the workflow logs to see which files were found
- Some files may not exist if the build didn't generate them

---

## Comparison with Original Equicord Workflows

**Removed from your fork:**
- ❌ Publishing to external repositories (Equibored)
- ❌ Browser extension store publishing (requires secrets)
- ❌ Daily NixOS builds

**Kept in your fork:**
- ✅ Testing and linting
- ✅ Building desktop and web versions
- ✅ Creating GitHub releases
- ✅ Generating plugin metadata

Your fork is now self-contained and doesn't require any external services or secrets! 🚀
